---
layout: post
title: "Practical Persistence Ignorant Lazy Loading For Your Hand-Rolled DAL"
date: 2010-01-31 12:45
comments: false
categories: development 
---
## Introduction – A Word Of Warning

First off - I **do not** recommend you write your own hand-rolled data
access solution for an OO .NET application. Ayende has a [great post](http://ayende.com/Blog/archive/2006/05/12/25ReasonsNotToWriteYourOwnObjectRelationalMapper.aspx) 
that should convince you to use something like
[NHibernate](http://nhforge.org/), [LLBLGen](http://www.llblgen.com/),
[Entity Framework](http://en.wikipedia.org/wiki/ADO.NET_Entity_Framework), or
[Linq2Sql](http://en.wikipedia.org/wiki/LINQ_to_SQL#LINQ_to_SQL). I
strongly agree with him. I’ve worked on several projects which had a
hand rolled, stored procedure based DAL. All of the DALs that were of a
medium-to-large-size eventually turned into a huge mess, or something
with tons of friction and poor performance. That being said, I am not
allowed to use an ORM at my current employer, and I know that many
others are not as well. That being the case, I think this post may be of
use for other people in the same situation. <!-- more --> 

Secondly – I specifically used the word “practical” to describe this strategy. Although there are
ways to do this sort of thing with code gen and/or reflection, I am
going to assume that most places that don’t use ORMs will find those
techniques to be too complex. 

Thirdly – This article is focused on the
lazy loading aspect of the sample code. The implementation /
organization of the data access layer is not to be taken as best
practices. It is organized in a way to be easily understood, and so it
does not get in the way of the topic at hand. I am also ignoring many
other features of a robust data access layer (change tracking,
transactions, etc…) as I think they do not need to be understood in
order to put this concept in action. However, there is nothing about
this implementation that would exclude it from being used with other ORM
concepts.

## Terminology

As far as this article is concerned, here are the operational
definitions of the core terms:
 
**Entity:** An object that is persisted to
the database that has business related behaviors. 

**Data Access Object (DAO):** A DAO is a data access layer (DAL) object that has the
responsibility of calling the database and mapping the results to
entities. The Repository Pattern is a relative of the DAO pattern.

**Persistence Awareness (PA):** An entity that is persistence aware is
one that is responsible for its own persistence. 

Examples:

```csharp
var myClass = MyClass.LoadByID(id);
myClass.Save();
```

A PA entity is either directly or indirectly aware of its data store and
is responsible for coordinating the persistence of its children. When
the persistence methods are called, it news up the appropriate DAO and
gets the results back. 

**Persistence Ignorance (PI):** An entity that is
persistence ignorant relies on other classes to handle the
responsibility of persisting it. 

Example:

```csharp
var myClassDAO = new MyClassDAO();
var myClass = myClassDAO.GetByID(id);
myClassDAO.Save(myClass);
```

The coordination of persisting and retrieving child entities is also
handled by the external class. 

**Lazy Loading:** Lazy loading is a term
that refers to delaying the retrieval of a child collection until it is
accessed. This is done to save trips to the database and to reduce
application memory consumption. 

Consider the following code:

```csharp
var userDAO = new UserDAO();
var company = userDAO.GetByName("Hardees");

Console.WriteLine(company.Name);

foreach(var employee in Company.Employees)
{
    Console.WriteLine(employee.Name);
}
```

If we are using lazy loading, the employee collection would not be
loaded until we hit the body of the foreach loop. If we were using eager
loading, the employee collection would have been loaded when the company
was loaded.

### Why should PI be preferred to PA?

There are two reasons which are a bit related. First off, persistence
code tends to be tricky and long winded. Often times there is more
persistence code in a PA class than business logic. Secondly, you always
want to give your class as few responsibilities / reasons to change as
possible. The code in your entities should focus on business behavior
rather than infrastructure concerns such as persistence.

### If PI is preferred, why do most hand rolled data access layers use PA?

In my experience, people usually prefer PA because it makes lazy loading
extremely easy. The typical pattern is to hit the database when a
property is accessed and its backing field is null. This is a very easy
pattern to understand, but unfortunately it sticks our entities with all
of the overhead and complexity of persistence concerns.

### Less Talk, More Rock!

Now that we have all the background out of the way, let’s take a look at
an implementation I’ve tried recently that seems to work well and is
very easy to understand. It comes down to two classes which are
coordinated by the application's DAO classes. These two classes are:

**LazyLoadingList\<T\>** - This is a wrapper around List\<T\> which triggers a load whenever one of its methods is called.

**LoadDelegate\<T\>** - This is the delegate that is executed when a LazyLoadingList\<T\>’s load method is triggered.

Here is the code for the LazyLoadingList\<T\>:

```csharp
public class LazyLoadingList<t> : IList<t>
{
    private List<t> _list;
    private LoadDelegate<t> _loadDelegate;

    public LazyLoadingList(LoadDelegate<t> loadDelegate)
    {
        _loadDelegate = loadDelegate;
    }

    public void Load()
    {
        _list = _loadDelegate().ToList();
        Loaded = true;
    }

    private bool Loaded { get; set; }

    private void LoadIfNotLoaded()
    {
        if (!Loaded)
        {
            Load();
        }
    }

    #region Implementation of IEnumerable

    public IEnumerator<t> GetEnumerator()
    {
        LoadIfNotLoaded();
        return _list.GetEnumerator();
    }

    IEnumerator IEnumerable.GetEnumerator()
    {
        LoadIfNotLoaded();
        return _list.GetEnumerator();
    }

    #endregion

    #region Implementation of ICollection<t>

    public void Add(T item)
    {
        LoadIfNotLoaded();
        _list.Add(item);
    }

    public void Clear()
    {
        LoadIfNotLoaded();
        _list.Clear();
    }

    public bool Contains(T item)
    {
        LoadIfNotLoaded();
        return _list.Contains(item);
    }

    public void CopyTo(T[] array, int arrayIndex)
    {
        LoadIfNotLoaded();
        _list.CopyTo(array, arrayIndex);
    }

    public bool Remove(T item)
    {
        LoadIfNotLoaded();
        return _list.Remove(item);
    }

    public int Count
    {
        get
        {
            LoadIfNotLoaded();
            return _list.Count;
        }
    }

    public bool IsReadOnly
    {
        get
        {
            LoadIfNotLoaded();
            return ((ICollection<t>)_list).IsReadOnly;
        }
    }

    #endregion

    #region Implementation of IList<t>

    public int IndexOf(T item)
    {
        LoadIfNotLoaded();
        return _list.IndexOf(item);
    }

    public void Insert(int index, T item)
    {
        LoadIfNotLoaded();
        _list.Insert(index, item);
    }

    public void RemoveAt(int index)
    {
        LoadIfNotLoaded();
        _list.RemoveAt(index);
    }

    public T this[int index]
    {
        get
        {
            LoadIfNotLoaded();
            return _list[index];
        }
        set
        {
            LoadIfNotLoaded();
            _list[index] = value;
        }
    }

    #endregion
}
```

Here is the code for the LoadDelegate

```csharp
public delegate IEnumerable<t> LoadDelegate<t>();
```

## The Demo

I’ve put a [demo up on Github](https://github.com/dauger/BlogSamples/tree/master/2010_01_31_LazyLoadingCollections)
that ties this altogether. The project is organized as follows:

{% img center /images/postimages/LazyLoadingCollectionsProject.jpg %}

The Employee load delegate gets wired up in the Company DAO like so:

```csharp
public class FakeCompanyDAO : ICompanyDAO
{
    List<company> _companiesInDatabase = new List<company>
    {
        new Company(){Name = "ACME"},
        new Company(){Name = "Hardees"}
    };

    #region Implementation of ICompanyDAO

    public Company GetByName(string name)
    {
        // Pretend we are calling / mapping from a store procedure
        var company = _companiesInDatabase.Where(x => x.Name == name).First();

        if(company != null)
        {
            company.Employees = new LazyLoadingList<employee>(
            () =>
                {
                    var employeeDAL = new FakeEmployeeDAO();

                    // To demonstrate when loading is happening
                    Console.WriteLine("Loading Employees");

                    return employeeDAL.GetByCompanyName(name);
                }
            );
        }

        return company;
    }

#endregion
}
```

The Demo program code:

```csharp
class Program
{
    static void Main(string[] args)
    {
        ICompanyDAO db = new FakeCompanyDAO();

        var company = db.GetByName("Hardees");

        Console.WriteLine("Company Loaded: " + company.Name);
        Console.WriteLine("About to iterate Employees");

        foreach(var emp in company.Employees)
        {
            Console.WriteLine(emp.Name);
        }
    }
}
```

The output:

```text
Company Loaded: Hardees
About to iterate Employees
Loading Employees
Jon
Kim
Suzi
```

## Possible Improvements

There are many possible improvements to this strategy depending on how
far one is willing to go. It would be very easy to auto wire up
everything with one generic delegate if DAO semantics were uniform
across DAOs etc… 

[Source Code](https://github.com/dauger/BlogSamples/tree/master/2010_01_31_LazyLoadingCollections)

## UDPATE 
This technique has been reworked for .NET 4.0 [here](/blog/2010/04/26/persistence-ignorant-lazy-loading-for-your-hand-rolled-dal-in-net-4-dot-0-using-lazy).
