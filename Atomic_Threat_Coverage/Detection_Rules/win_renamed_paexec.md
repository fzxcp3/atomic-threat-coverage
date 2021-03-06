| Title                | Execution of Renamed PaExec                                                                                                                                                 |
|:---------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Description          | Detects execution of renamed paexec via imphash and executable product string                                                                                                                                           |
| ATT&amp;CK Tactic    | <ul><li>[TA0005: Defense Evasion](https://attack.mitre.org/tactics/TA0005)</li></ul>  |
| ATT&amp;CK Technique | <ul><li>[T1036: Masquerading](https://attack.mitre.org/techniques/T1036)</li></ul>                             |
| Data Needed          | <ul></ul>                                                         |
| Trigger              | <ul><li>[T1036: Masquerading](../Triggers/T1036.md)</li></ul>  |
| Severity Level       | medium                                                                                                                                                 |
| False Positives      | <ul><li>Unknown imphashes</li></ul>                                                                  |
| Development Status   | experimental                                                                                                                                                |
| References           | <ul><li>[{'sha256': '01a461ad68d11b5b5096f45eb54df9ba62c5af413fa9eb544eacb598373a26bc'}]({'sha256': '01a461ad68d11b5b5096f45eb54df9ba62c5af413fa9eb544eacb598373a26bc'})</li><li>[https://summit.fireeye.com/content/dam/fireeye-www/summit/cds-2018/presentations/cds18-technical-s05-att&cking-fin7.pdf](https://summit.fireeye.com/content/dam/fireeye-www/summit/cds-2018/presentations/cds18-technical-s05-att&cking-fin7.pdf)</li></ul>                                                          |
| Author               | Jason Lynch                                                                                                                                                |
| Other Tags           | <ul><li>FIN7</li><li>FIN7</li></ul> | 

## Detection Rules

### Sigma rule

```
title: Execution of Renamed PaExec 
status: experimental
description: Detects execution of renamed paexec via imphash and executable product string 
references:
    - sha256: 01a461ad68d11b5b5096f45eb54df9ba62c5af413fa9eb544eacb598373a26bc 
    - https://summit.fireeye.com/content/dam/fireeye-www/summit/cds-2018/presentations/cds18-technical-s05-att&cking-fin7.pdf
tags:
    - attack.defense_evasion
    - attack.t1036
    - FIN7
date: 2019/04/17
author: Jason Lynch 
falsepositives:
    - Unknown imphashes
level: medium
logsource:
    category: process_creation
    product: windows
detection:
    selection1:
        Product:
            - '*PAExec*'
    selection2:
        Imphash:
            - 11D40A7B7876288F919AB819CC2D9802
            - 6444f8a34e99b8f7d9647de66aabe516
            - dfd6aa3f7b2b1035b76b718f1ddc689f
            - 1a6cca4d5460b1710a12dea39e4a592c
    filter1:
        Image: '*paexec*'
    condition: (selection1 and selection2) and not filter1

```





### es-qs
    
```

```


### xpack-watcher
    
```

```


### graylog
    
```
((Product:("*PAExec*") AND Imphash:("11D40A7B7876288F919AB819CC2D9802" "6444f8a34e99b8f7d9647de66aabe516" "dfd6aa3f7b2b1035b76b718f1ddc689f" "1a6cca4d5460b1710a12dea39e4a592c")) AND NOT (Image:"*paexec*"))
```


### splunk
    
```

```


### logpoint
    
```

```


### grep
    
```
grep -P '^(?:.*(?=.*(?:.*(?=.*(?:.*.*PAExec.*))(?=.*(?:.*11D40A7B7876288F919AB819CC2D9802|.*6444f8a34e99b8f7d9647de66aabe516|.*dfd6aa3f7b2b1035b76b718f1ddc689f|.*1a6cca4d5460b1710a12dea39e4a592c))))(?=.*(?!.*(?:.*(?=.*.*paexec.*)))))'
```



