So you've got a corporate laptop, and everything is perfect except the fact that it has auto updates on, and you can't change that because the laptop is managed by the Admins team.
One morning you're doing a complex ticket, just commit the recent change, **Xcode closes**, and says [You can’t open the application “Xcode” because it is being updated](https://developer.apple.com/forums/thread/703098)

AppStore sucks as always - no spinning wheel. Even if you initiate an update from there, there'll be a spinning wheel without the progress value.

1. `sudo killall -9 installd`
2. delete both `DerivedData` and `/Applications/Xcode.app`
3. login to https://developer.apple.com/download/applications/, and download the latest Xcode.xip

the progress is being shown at each step of downloading XIP, extracting it, verifying it; which make this autoupdate hell more manageable 
