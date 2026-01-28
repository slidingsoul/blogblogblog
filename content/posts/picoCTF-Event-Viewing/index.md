---
date: '2026-01-27T09:23:35+07:00'
title: 'picoCTF Event-Viewing'
tags: ["ctf"]
---

- URL: https://play.picoctf.org/practice/challenge/456
- Title: Event-Viewing
- Tags: Medium, Forensics, picoCTF 2025, browser_webshell_solvable
- Author: Venax
- _Started: 16 July 2025_
- _Solved: 16 July 2025_
- Description: 

> One of the employees at your company has their computer infected by malware! Turns out every time they try to switch on the computer, it shuts down right after they log in. The story given by the employee is as follows:

> 1.  They installed software using an installer they downloaded online
> 2.  They ran the installed software but it seemed to do nothing
> 3.  Now every time they bootup and login to their computer, a black command prompt screen quickly opens and closes and their computer shuts down instantly.

> See if you can find evidence for the each of these events and retrieve the flag (split into 3 pieces) from the correct logs! Download the Windows Log file [here](https://challenge-files.picoctf.net/c_verbal_sleep/123d9b79cadb6b44ab6ae912f25bf9cc18498e8addee851e7d349416c7ffc1e1/Windows_Logs.evtx)

Okay after I downloaded the `.evtx` file, I used [this tool](https://github.com/omerbenamram/evtx/releases/tag/v0.11.0) to convert it to .xml file

```
./evtx_dump-v0.11.0-x86_64-unknown-linux-gnu Windows_Logs.evtx > parsed.xml
```

According to the description, there were 3 flags and the incident happened after software installation. After a bit of browsing, I found that the event id of software installation is [11707](https://learn.microsoft.com/en-us/answers/questions/983008/eventid-that-logs-software-installation-on-worksta)

```
Record 74
<?xml version="1.0" encoding="utf-8"?>
<Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event">
  <System>
    <Provider Name="MsiInstaller">
    </Provider>
    <EventID Qualifiers="0">11707</EventID>
    <Version>0</Version>
    <Level>4</Level>
    <Task>0</Task>
    <Opcode>0</Opcode>
    <Keywords>0x80000000000000</Keywords>
    <TimeCreated SystemTime="2024-07-15T15:55:57.729798Z">
    </TimeCreated>
    <EventRecordID>2372</EventRecordID>
    <Correlation>
    </Correlation>
    <Execution ProcessID="0" ThreadID="0">
    </Execution>
    <Channel>Application</Channel>
    <Computer>DESKTOP-EKVR84B</Computer>
    <Security UserID="S-1-5-21-3576963320-1344788273-4164204335-1001">
    </Security>
  </System>
  <EventData>
    <Data>Product: Totally_Legit_Software -- Installation completed successfully.</Data>
    <Data>(NULL)</Data>
    <Data>(NULL)</Data>
    <Data>(NULL)</Data>
    <Data>(NULL)</Data>
    <Data>(NULL)</Data>
    <Data>
    </Data>
    <Binary>7B33443343333833332D444544362D343032322D423541312D4537463337373839433339307D</Binary>
  </EventData>
</Event>
```

Here's the record 74, it didn't have anything to do but on the record 78

```
Record 75
<?xml version="1.0" encoding="utf-8"?>
<Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event">
  <System>
    <Provider Name="MsiInstaller">
    </Provider>
    <EventID Qualifiers="0">1033</EventID>
    <Version>0</Version>
    <Level>4</Level>
    <Task>0</Task>
    <Opcode>0</Opcode>
    <Keywords>0x80000000000000</Keywords>
    <TimeCreated SystemTime="2024-07-15T15:55:57.729798Z">
    </TimeCreated>
    <EventRecordID>2373</EventRecordID>
    <Correlation>
    </Correlation>
    <Execution ProcessID="0" ThreadID="0">
    </Execution>
    <Channel>Application</Channel>
    <Computer>DESKTOP-EKVR84B</Computer>
    <Security UserID="S-1-5-21-3576963320-1344788273-4164204335-1001">
    </Security>
  </System>
  <EventData>
    <Data>Totally_Legit_Software</Data>
    <Data>1.3.3.7</Data>
    <Data>0</Data>
    <Data>0</Data>
    <Data>cGljb0NURntFdjNudF92aTN3djNyXw==</Data>
    <Data>(NULL)</Data>
    <Data>
    </Data>
    <Binary>7B33443343333833332D444544362D343032322D423541312D4537463337373839433339307D3030303037363533376239373032333966396130373530633431623838363466646163393030303030303030</Binary>
  </EventData>
</Event>
```

I had found a part of the flag `cGljb0NURntFdjNudF92aTN3djNyXw==` and it seemed to be encoded in base64

I changed the search keyword to `Totally_Legit_Software` and on the record 186, I found another part

```
Record 186
<?xml version="1.0" encoding="utf-8"?>
<Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event">
  <System>
    <Provider Name="Microsoft-Windows-Security-Auditing" Guid="54849625-5478-4994-A5BA-3E3B0328C30D">
    </Provider>
    <EventID>4657</EventID>
    <Version>0</Version>
    <Level>0</Level>
    <Task>12801</Task>
    <Opcode>0</Opcode>
    <Keywords>0x8020000000000000</Keywords>
    <TimeCreated SystemTime="2024-07-15T15:56:19.103196Z">
    </TimeCreated>
    <EventRecordID>168656</EventRecordID>
    <Correlation>
    </Correlation>
    <Execution ProcessID="4" ThreadID="1084">
    </Execution>
    <Channel>Security</Channel>
    <Computer>DESKTOP-EKVR84B</Computer>
    <Security>
    </Security>
  </System>
  <EventData>
    <Data Name="SubjectUserSid">S-1-5-21-3576963320-1344788273-4164204335-1001</Data>
    <Data Name="SubjectUserName">user</Data>
    <Data Name="SubjectDomainName">DESKTOP-EKVR84B</Data>
    <Data Name="SubjectLogonId">0x5a428</Data>
    <Data Name="ObjectName">\REGISTRY\MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run</Data>
    <Data Name="ObjectValueName">Immediate Shutdown (MXNfYV9wcjN0dHlfdXMzZnVsXw==)</Data>
    <Data Name="HandleId">0x208</Data>
    <Data Name="OperationType">%%1904</Data>
    <Data Name="OldValueType">-</Data>
    <Data Name="OldValue">-</Data>
    <Data Name="NewValueType">%%1873</Data>
    <Data Name="NewValue">C:\Program Files (x86)\Totally_Legit_Software\custom_shutdown.exe</Data>
    <Data Name="ProcessId">0x1bd0</Data>
    <Data Name="ProcessName">C:\Program Files (x86)\Totally_Legit_Software\Totally_Legit_Software.exe</Data>
  </EventData>
</Event>
```

That part was `MXNfYV9wcjN0dHlfdXMzZnVsXw==`

Lastly, I changed the search keyword to `shutdown` and found another part on record 5575

```
Record 5575
<?xml version="1.0" encoding="utf-8"?>
<Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event">
  <System>
    <Provider Name="User32" Guid="{b0aa8734-56f7-41cc-b2f4-de228e98b946}" EventSourceName="User32">
    </Provider>
    <EventID Qualifiers="32768">1074</EventID>
    <Version>0</Version>
    <Level>4</Level>
    <Task>0</Task>
    <Opcode>0</Opcode>
    <Keywords>0x8080000000000000</Keywords>
    <TimeCreated SystemTime="2024-07-15T17:01:05.393583Z">
    </TimeCreated>
    <EventRecordID>3801</EventRecordID>
    <Correlation>
    </Correlation>
    <Execution ProcessID="432" ThreadID="3496">
    </Execution>
    <Channel>System</Channel>
    <Computer>DESKTOP-EKVR84B</Computer>
    <Security UserID="S-1-5-21-3576963320-1344788273-4164204335-1001">
    </Security>
  </System>
  <EventData>
    <Data Name="param1">C:\Windows\system32\shutdown.exe (DESKTOP-EKVR84B)</Data>
    <Data Name="param2">DESKTOP-EKVR84B</Data>
    <Data Name="param3">No title for this reason could be found</Data>
    <Data Name="param4">0x800000ff</Data>
    <Data Name="param5">shutdown</Data>
    <Data Name="param6">dDAwbF84MWJhM2ZlOX0=</Data>
    <Data Name="param7">DESKTOP-EKVR84B\user</Data>
  </EventData>
</Event>
```

That part was `dDAwbF84MWJhM2ZlOX0=`. Okay so the full base64 encoded flag is `cGljb0NURntFdjNudF92aTN3djNyXw==MXNfYV9wcjN0dHlfdXMzZnVsXw==dDAwbF84MWJhM2ZlOX0=`. Here's the result after decoding

```
strikingsoul@ramones:~/Downloads$ echo cGljb0NURntFdjNudF92aTN3djNyXw==MXNfYV9wcjN0dHlfdXMzZnVsXw==dDAwbF84MWJhM2ZlOX0= | base64 --decode
picoCTF{Ev3nt_vi3wv3r_1s_a_pr3tty_us3ful_t00l_81ba3fe9}
```

`picoCTF{Ev3nt_vi3wv3r_1s_a_pr3tty_us3ful_t00l_81ba3fe9}`