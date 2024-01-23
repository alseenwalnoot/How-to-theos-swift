#### To start a theos project run ```$THEOS/bin/nic.pl```
you will see something along the lines off:
```
NIC 2.0 - New Instance Creator
------------------------------
  [1.] iphone/activator_event
  [2.] iphone/activator_listener
  [3.] iphone/application
  [4.] iphone/application_swift
  [5.] iphone/control_center_module-11up
  [6.] iphone/cydget
  [7.] iphone/flipswitch_switch
  [8.] iphone/framework
  [9.] iphone/library
  [10.] iphone/notification_center_widget
  [11.] iphone/notification_center_widget-7up
  [12.] iphone/preference_bundle
  [13.] iphone/preference_bundle_swift
  [14.] iphone/theme
  [15.] iphone/tool
  [16.] iphone/tool_swift
  [17.] iphone/tweak
  [18.] iphone/tweak_swift
  [19.] iphone/tweak_with_simple_preferences
  [20.] iphone/xpc_service
  [21.] iphone/xpc_service_modern
Choose a Template (required):
```
for our tutorial we will select iphone/tweak_swift, so in this case 18, then you will get: 
```
Project Name (required):
```
this is what you get to see in your package manager, i will do TextChangerTutorial
```
Package Name [com.yourcompany.textchangertutorial]:
```
this is what the .deb will be named, i will choose ```com.walnutstudios.textchangertutorial```
```
Author/Maintainer Name [YOURUSERNAME]:
```
do something that people would call you on the internet (eg, your discord username)
```
[iphone/tweak_swift] MobileSubstrate Bundle filter [com.apple.springboard]:
```
this is what your tweak injects into, for this tutorial we can skip it and click enter.
```
[iphone/tweak_swift] List of applications to terminate upon installation (space-separated, '-' for none) [SpringBoard]: 
```
if your tweak needs to reload an app/deamon after installing it, it should be specified here, we can just do - and click enter, thats it, you set up your first theos project! For me all of it is:
```
Choose a Template (required): 18
Project Name (required): TextChangerTutorial
Package Name [com.yourcompany.textchangertutorial]: com.walnutstudios.textchangertutorial
Author/Maintainer Name [dustin]: 
[iphone/tweak_swift] MobileSubstrate Bundle filter [com.apple.springboard]: 
[iphone/tweak_swift] List of applications to terminate upon installation (space-separated, '-' for none) [SpringBoard]: -
Instantiating iphone/tweak_swift in textchangertutorial/...
Done.
```
