---
layout: post
title: "The Case of Web Deploy 2.0 and the Missing MSDeploy.exe"
date: 2011-02-16 21:19
comments: false
categories: development
---
This week, I decided to install the newly released Web Deploy 2.0 on my machine at work. I already had Web Deploy 1 on my machine, so I decided to uninstall that first before installing 2.0. After the installation I begain getting the following error when trying to execute VS2010 created web deployment packages from the command line: <!-- more -->

```bat
Error:  The system was unable to find the specified registry key or value
msdeploy.exe is not found on this machine. Please install Web Deploy before exe
cute the script.
Please visit http://go.microsoft.com/?linkid=9278654
=========================================================
=========================================================
```

Of course the first thing I did was validate that MSDeploy was indeed installed with Web Deploy 2.0. It was. I then tried adding MSDeploy's location to the path environment variable. No dice. I then tried reinstalling Web Deploy 2.0. Still no luck. After trying some other things I cracked open the deployment package's cmd file and found this:

```bat
@rem ---------------------------------------------------------------------------------
@rem if user does not set MsDeployPath environment variable, we will try to retrieve it from registry.
@rem ---------------------------------------------------------------------------------
if "%MSDeployPath%" == "" (
for /F "usebackq tokens=2*" %%i  in (`reg query "HKLM\SOFTWARE\Microsoft\IISExtensions\MSDeploy\1" /v InstallPath`) do (
if "%%~dpj" == "%%j" ( 
set MSDeployPath=%%j
))
```

For whatever reason, Web Deploy 2.0 did not add either of these items during install. I ended up adding the MSDeployPath environment variable, and all was good.
