Charles Proxy is cool, but not so easy to learn.
Even if Charles is set up and some kind of commercial license is added, is't not enough (I lived a few month thinking that I intercept requests from Xcode Simulator, but that was only half true).

## Setup 
+ In `Proxy > SSL Proxy Settings` "\*" should be added to "Location".
+ `Help > SSL Proxying > Install Charles Root Certificate in iOS Simulators` should be checked to install certificate to Simulator
+ Install Charles Certificate to a physical iPhone by visiting https://chls.pro/ssl from that iPhone. If that sucking page shows some plain HTML text with some untappable checkbox, swipe that page from top to down. Get some dialog like "do really want to install this certificate?". Then go to `General > VPN DNS and Device Management`, approve that certificate. AND ONLY THEN go to `General > About > Certificate Trust Settings`.

## Questions

1. How to monitor only the specific endpoints, not all that noise?
2. How to make MacOS browsers work??
3. Is it possible to autotest such stuff like "count of requests to some endpoint" in Charles?
