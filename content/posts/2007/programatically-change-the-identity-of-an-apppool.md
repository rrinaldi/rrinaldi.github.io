---
title: Programatically change the identity of an AppPool
date: 2007-08-28
---
A couple weeks ago we were making some changes to our web servers that
required all the Application Pools to be running as a known domain
user.  While it’s not hard to change it by hand, I figured it would be
smarter for me to have 2 scripts, one to make the changes and the other
to roll them back.  So in the interests of the greater good, here they
are:

Change to a domain account -

```vb
Dim locatorObj, ProviderObj, Pools, strQuery, appPool

Set locatorObj = CreateObject("WbemScripting.SWbemLocator")\
Set ProviderObj = locatorObj.ConnectServer(".", "root/MicrosoftIISv2")

strQuery = "Select \* from IIsApplicationPool"\
For Each Item In ProviderObj.ExecQuery(strQuery)\
    WScript.Echo Replace(Item.Name, "W3SVC/AppPools/", "")\
    WScript.Echo "IIS://localhost/" & Item.Name\
    Set appPool = GetObject("IIS://localhost/" & Item.Name)\
    appPool.AppPoolIdentityType = 3\
    appPool.WAMUserName = "UserNameGoesHere"\
    appPool.WAMUserPass = "PasswordGoesHere"\
    appPool.SetInfo()\
Next\
WScript.Echo "Done!"

Change to Network Service -

Dim locatorObj, ProviderObj, Pools, strQuery, appPool

Set locatorObj = CreateObject("WbemScripting.SWbemLocator")\
Set ProviderObj = locatorObj.ConnectServer(".", "root/MicrosoftIISv2")

strQuery = "Select \* from IIsApplicationPool"\
For Each Item In ProviderObj.ExecQuery(strQuery)\
    WScript.Echo Replace(Item.Name, "W3SVC/AppPools/", "")\
    WScript.Echo "IIS://localhost/" & Item.Name\
    Set appPool = GetObject("IIS://localhost/" & Item.Name)\
    appPool.AppPoolIdentityType = 2\
    appPool.SetInfo()\
Next\
WScript.Echo "Done!"
```
 
