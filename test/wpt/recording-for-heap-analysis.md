---
title: Recording for Heap Analysis
description: Recording for Heap Analysis
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: 9acc8558-67ef-471a-af69-1173cb49bdb4
ms.mktglfcycl: operate
ms.sitesec: msdn
ms.author: eliotgra
ms.date: 05/05/2017
ms.topic: article


---

# Recording for Heap Analysis


Windows Performance Recorder (WPR) enables heap analysis for all processes on the system.

**To enable heap tracing for a desktop app**

(Using WPRUI.exe)
1.  From the **More options** dropdown menu, select the **Heap usage** profile.

2.  Add a registry entry for the process by running the following command from an elevated command prompt window, replacing `*&lt;process\_name&gt;*` with the name of the process to be traced:

    **reg add "HKLM\\Software\\Microsoft\\Windows NT\\CurrentVersion\\Image File Execution Options\\&lt;process\_name&gt;" /v TracingFlags /t REG\_DWORD /d 1 /f**

(Using Wpr.exe)
1.  Enable Heap tracking by setting the IFEO registry
      `wpr.exe -HeapTracingConfig *&lt;process\_name&gt;* enable`

2.  Start the tracing session:
      `wpr.exe -start Heap \[-filemode\]`

3.  test the scenario.

4.  Stop the tracing session: 
      `wpr.exe -stop *&lt;file\_name&gt;*`

5.  Disable Heap tracking
      `wpr.exe -HeapTracingConfig *&lt;process\_name&gt;* disable`

**To enable heap tracing for a Microsoft Store app**

1.  From the **More options** dropdown menu, select the **Heap usage** profile.

2.  If you want to trace a packaged application that is hosted in a process (such as WWAHost.exe), add a registry entry for the process by running the following command from an elevated command prompt window, replacing *&lt;process\_name&gt;*, *&lt;package full name&gt;*, and *&lt;package-relative app ID&gt;* with your app information:

    **reg add "HKLM\\Software\\Microsoft\\Windows NT\\CurrentVersion\\Image File Execution Options\\&lt;process\_name&gt;\\&lt;package full name&gt;!&lt;package-relative app ID&gt;" /v TracingFlags /t REG\_DWORD /d 1 /f**

    **Note**  
    This combination (package full name + app ID) is not an app user model ID (package family name + app ID). The IFEO processing routines use the full name so that they can apply different behavior to different versions of a single package/app.

     

## Related topics


[WPR Common Scenarios](windows-performance-recorder-common-scenarios.md)

[Image File Execution Options](http://go.microsoft.com/fwlink/p/?LinkId=268419)

 

 







