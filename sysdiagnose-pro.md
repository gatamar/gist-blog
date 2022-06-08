[Instuctions](https://developer.apple.com/forums/thread/80811) how to trigger collecting sysdiagnose logs on iPhone:
```
VOL Up + Down + Power, succeed on iOS 14. for me, the key point is release.
press VOL Up + Down + Power
wait 1s or 1.5s
release all buttons
then I feel the vibration, and after few minutes, go to the Settings > Privacy > Analytics > Analytis Data, there be a log with sysdiagnose and the corresponding date.
```

A [nice tutorial](https://www.cellebrite.com/en/converting-unified-logs-a-great-disturbance-in-the-force/) of how to unpack the sysdiagnose downloaded from iPhone. 
```
log show ~/Downloads/path-to-sysdiagnose-date-unzipped/system_logs.logarchive --style syslog --predicate 'eventMessage contains "TADAM"'
```
