---
layout: post
title: "Persistence Ignorant Lazy Loading for Your Hand-Rolled DAL in .NET 4.0 Using Lazy<T>"
date: 2010-04-26 13:54
comments: false
categories: development
---
This post is a brief update to the .NET 3.5 article I posted about [P.I. lazy loading](/blog/2010/01/31/practical-persistence-ignorant-lazy-loading-for-your-hand-rolled-dal/). The only major change I have made to the code is to use the new  [Lazy\<T\>](http://msdn.microsoft.com/en-us/library/dd642331.aspx) class that was introduced in .NET 4.0. This considerably cleans up the LazyLoadingList\<T\> class from the previous post. <!-- more -->

Here is the new LazyLoadingList\<T\>:  
```csharp
public class LazyLoadingList<T> : IList<T>
{
     private Lazy<IList<T>> _lazyList;

     public LazyLoadingList(Lazy<IList<T>> lazyList)
     {
        _lazyList = lazyList;
     }

     #region Implementation of IEnumerable

     public IEnumerator<T> GetEnumerator()
     {
        return _lazyList.Value.GetEnumerator();
     }

     IEnumerator IEnumerable.GetEnumerator()
     {
        return _lazyList.Value.GetEnumerator();
     }

     #endregion

     #region Implementation of ICollection<T>

     public void Add(T item)
     {
        _lazyList.Value.Add(item);
     }

     public void Clear()
     {
        _lazyList.Value.Clear();
     }

     public bool Contains(T item)
     {
        return _lazyList.Value.Contains(item);
     }

     public void CopyTo(T[] array, int arrayIndex)
     {
        _lazyList.Value.CopyTo(array, arrayIndex);
     }

     public bool Remove(T item)
     {
        return _lazyList.Value.Remove(item);
     }

     public int Count
     {
        get
        {
           return _lazyList.Value.Count;
        }
     }

     public bool IsReadOnly
     {
        get
        {
           return ((ICollection<T>)_lazyList.Value).IsReadOnly;
        }
     }

     #endregion

     #region Implementation of IList<T>

     public int IndexOf(T item)
     {
        return _lazyList.Value.IndexOf(item);
     }

     public void Insert(int index, T item)
     {
        _lazyList.Value.Insert(index, item);
     }

     public void RemoveAt(int index)
     {
        _lazyList.Value.RemoveAt(index);
     }

     public T this[int index]
     {
        get
        {
           return _lazyList.Value[index];
        }
        set
        {
           _lazyList.Value[index] = value;
        }
     }

     #endregion
}
```
Here are the changes to the invoking code:
```csharp
public class CompanyDAO : ICompanyDAO
{
   List<Company> _companiesInDatabase = new List<Company>
         {
             new Company(){Name = "ACME"},
             new Company(){Name = "Hardees"}
         };

   #region Implementation of ICompanyDAO

   public Company GetByName(string name)
   {
      // Write to console to demonstrate when loading is happening
      Console.WriteLine("---Loading Company---");

      // Pretend we are calling / mapping from a store procedure
      var company = _companiesInDatabase.Where(x => x.Name == name).First();

      
      // Create / add the lazily loaded collection
      if (company != null)
      {
         var lazyLoader = new Lazy<IList<Employee>>(
               () =>
                     {
                        var employeeDAO = new EmployeeDAO();
                        return employeeDAO.GetByCompanyName(name).ToList();
                     }
            );

         company.Employees = new LazyLoadingList<Employee>(lazyLoader);
      }

      return company;
   }

   #endregion
}
```
[Source Code](https://github.com/dauger/BlogSamples/tree/master/2010_04_26_LazyLoadingCollectionsWithLazyT)
