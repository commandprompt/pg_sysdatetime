pg_sysdatetime
==============

PostgreSQL SYSDATETIME() functions with support for higher precision timer
capture on Windows

This module may be compiled using Visual Studio on Windows, or using PGXS with
MinGW.

The timestamps returned are those provided by GetSystemTimeAsFileTime, which
can return up to 100ns precision, but may return much coarser timestamps
depending on hardware and operating system/version. Use `clockres.exe` from
SysInternals to check your system's clock resolution (see link below).

This functionality is equivalent to changing `src/port/gettimeofday.c` to use
`GetSystemTimeAsFileTime` directly, rather than reading `GetSystemTime` and
converting to `FileTime` with `SystemTimeToFileTime`, but doesn't require a
core server patch.

Future work could permit the use of GetSystemTimePreciseAsFiletime where 
running on Windows Server 2012 or Windows 8.

See:

* GetSystemTimeAsFileTime: http://msdn.microsoft.com/en-us/library/windows/desktop/ms724397(v=vs.85).aspx
* GetSystemTimePreciseAsFileTime: http://msdn.microsoft.com/en-us/library/windows/desktop/hh706895(v=vs.85).aspx
* clockres.exe: http://technet.microsoft.com/en-us/sysinternals/bb897568.aspx
* GetSystemTimeAdjustment: http://msdn.microsoft.com/en-us/library/windows/desktop/ms724394(v=vs.85).aspx
* Windows Timer Project: http://www.windowstimestamp.com/description