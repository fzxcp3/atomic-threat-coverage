| Title                | Regsvr32 Anomaly                                                                                                                                                 |
|:---------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Description          | Detects various anomalies in relation to regsvr32.exe                                                                                                                                           |
| ATT&amp;CK Tactic    | <ul><li>[TA0005: Defense Evasion](https://attack.mitre.org/tactics/TA0005)</li><li>[TA0002: Execution](https://attack.mitre.org/tactics/TA0002)</li></ul>  |
| ATT&amp;CK Technique | <ul><li>[T1117: Regsvr32](https://attack.mitre.org/techniques/T1117)</li></ul>                             |
| Data Needed          | <ul><li>[DN_0002_4688_windows_process_creation_with_commandline](../Data_Needed/DN_0002_4688_windows_process_creation_with_commandline.md)</li><li>[DN_0003_1_windows_sysmon_process_creation](../Data_Needed/DN_0003_1_windows_sysmon_process_creation.md)</li></ul>                                                         |
| Trigger              | <ul><li>[T1117: Regsvr32](../Triggers/T1117.md)</li></ul>  |
| Severity Level       | high                                                                                                                                                 |
| False Positives      | <ul><li>Unknown</li></ul>                                                                  |
| Development Status   | experimental                                                                                                                                                |
| References           | <ul><li>[https://subt0x10.blogspot.de/2017/04/bypass-application-whitelisting-script.html](https://subt0x10.blogspot.de/2017/04/bypass-application-whitelisting-script.html)</li></ul>                                                          |
| Author               | Florian Roth                                                                                                                                                |


## Detection Rules

### Sigma rule

```
title: Regsvr32 Anomaly
status: experimental
description: Detects various anomalies in relation to regsvr32.exe
author: Florian Roth
references:
    - https://subt0x10.blogspot.de/2017/04/bypass-application-whitelisting-script.html
tags:
    - attack.t1117
    - attack.defense_evasion
    - attack.execution
logsource:
    category: process_creation
    product: windows
detection:
    selection1:
        Image: '*\regsvr32.exe'
        CommandLine: '*\Temp\\*'
    selection2:
        Image: '*\regsvr32.exe'
        ParentImage: '*\powershell.exe'
    selection3:
        Image: '*\regsvr32.exe'
        CommandLine:
            - '*/i:http* scrobj.dll'
            - '*/i:ftp* scrobj.dll'
    selection4:
        Image: '*\wscript.exe'
        ParentImage: '*\regsvr32.exe'
    selection5:
        Image: '*\EXCEL.EXE'
        CommandLine: '*..\..\..\Windows\System32\regsvr32.exe *'
    condition: 1 of them
fields:
    - CommandLine
    - ParentCommandLine
falsepositives:
    - Unknown
level: high

```





### es-qs
    
```

```


### xpack-watcher
    
```

```


### graylog
    
```
((Image:"*\\\\regsvr32.exe" AND CommandLine:"*\\\\Temp\\\\*") OR (Image:"*\\\\regsvr32.exe" AND ParentImage:"*\\\\powershell.exe") OR (Image:"*\\\\regsvr32.exe" AND CommandLine:("*\\/i\\:http* scrobj.dll" "*\\/i\\:ftp* scrobj.dll")) OR (Image:"*\\\\wscript.exe" AND ParentImage:"*\\\\regsvr32.exe") OR (Image:"*\\\\EXCEL.EXE" AND CommandLine:"*..\\\\..\\\\..\\\\Windows\\\\System32\\\\regsvr32.exe *"))
```


### splunk
    
```

```


### logpoint
    
```

```


### grep
    
```
grep -P '^(?:.*(?:.*(?:.*(?=.*.*\\regsvr32\\.exe)(?=.*.*\\Temp\\\\.*))|.*(?:.*(?=.*.*\\regsvr32\\.exe)(?=.*.*\\powershell\\.exe))|.*(?:.*(?=.*.*\\regsvr32\\.exe)(?=.*(?:.*.*/i:http.* scrobj\\.dll|.*.*/i:ftp.* scrobj\\.dll)))|.*(?:.*(?=.*.*\\wscript\\.exe)(?=.*.*\\regsvr32\\.exe))|.*(?:.*(?=.*.*\\EXCEL\\.EXE)(?=.*.*\\.\\.\\\\.\\.\\\\.\\.\\Windows\\System32\\regsvr32\\.exe .*))))'
```



