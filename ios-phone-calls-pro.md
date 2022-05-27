**Problem**: add a button to some view, such that by pressing on it the user can make a call, e.g. to a support.

Domain: there's a relatively low-level CoreTelephony/[CallKit](https://www.raywenderlich.com/1276414-callkit-tutorial-for-ios) etc SDK solution. There's also a VoIP protocol. 
Both of them are a huge overkill and are needed, if I understand correctly, only if the app pretends to be a messenger like GMeets/Zoom/Signal/Telegram/Viber etc.

**Solution**: the simplest way is 
```
let url = URL(string: "telprompt:+{country}{your_phonenumber}")!
UIApplication.shared.open(url)
```

or `"telprompt:+{country}{your_phonenumber},{your_accessnumber}"` pattern can be used to specify the digits which will be autodialed after the connection established (the callee answers).

**Details**:

+ telprompt should be added to `LSApplicationQueriesSchemes`
+ telprompt vs tel: [apple dev forum thread](https://developer.apple.com/forums/thread/30215)
+ [Using telprompt instead of tel in the openURL method will not only prompt the user if they wish to call the number, but after the call is finished the user will be directed back to the app instead of the Apple’s phone app](https://www.rightpoint.com/rplabs/phone-call-requests-using-tel-in-an-ios-teleprompt-app)
+ [old good SO "tutorial"](https://stackoverflow.com/a/20427527) 

**Product**:
+ iPad/iPhome: iPad can't make phone calls, right?
+ the url scheme are very "flaky", apple deprecates/messes with them each few years; we should either send a non-fatal or show an alert, because force unwrap is definitely a bad approach :) 
+ accessibility support - no visual support, I guess, only sound if the app is that accessible
