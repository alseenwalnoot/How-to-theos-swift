# An in depth and MODERN tutorial on how to make tweaks for ios using swift, theos and orion in ubuntu, this will even work with something like serotonin and bootstrap
## for this tutorial i will be using ubuntu 22.04, it is possible in wsl but its stupidly hard to get it working since you dont have an gui, other distro's may also work but the commands will be different.

## NOTE: if your tweak doesnt compile it is because THEOS doesnt like ios 16.5 so you have to install the 14.5 sdk (it still works for most things) so download [this](https://github.com/theos/sdks/archive/master.zip) repo and move the iPhoneOS14.5.sdk into $THEOS/sdks

## We will be creating this tweak: it will make almost all text what you want! ![IMG_6322](https://github.com/alseenwalnoot/How-to-theos-swift/assets/124501148/60916570-5bdb-43ad-b772-07a13e484b81)

Step 0: (Installing stuff)[https://github.com/alseenwalnoot/How-to-theos-swift/blob/main/Installing-stuff.md]
Step 1: (Creating a project)[https://github.com/alseenwalnoot/How-to-theos-swift/blob/main/Setting-up-the-project.md]

#### Now lets actually start coding
Open the IDE you installed and open the folder with the name of your project (in my case TextChangerTutorial/
You will see some stuff and some errors in the corner, dont worry about them, click them away.

Now lets take a look at the file structure THEOS has created for us and lets go over everything and change some stuff:

![image](https://github.com/alseenwalnoot/How-to-theos-swift/assets/124501148/2baaf89b-0b35-49b6-b604-c5a00d589a4b)

The first thing *.build* doesnt matter and we dont have to go over it,

The folder *Sources/* contains our actual code but then inside the folder you might think, *What is the difference between TextChangerTutorial and TextChangerTutorialC?*, well one contains the actual swift code: */Tweak.x.swift* 
and one contains objective-c: */include/module.modulemap*, */include/Tweak.h*, and */Tweak.m*, so why is there objective-c in our swift tweak? Well the hooks used to change stuff in ios are made in obj.-c and need to be translated to swift.

The *control* file is used to tell your package manager what the tweak is and how it should handle it in debian language. Here is what a debian control file does (dont try to copy it! debian wont compile with //):
```
Package: com.walnutstudios.textchangertutorial //The bundle identifier, think of it as a name for a program but more low level
Name: TextChangerTutorial //The name that your package manager will use as a name
Version: 0.0.1 //This one is obvious, its the version, each time you recompile, the version increases
Architecture: iphoneos-arm //The architecture of the device your trying to make a tweak for arm = rootfull package, arm64 = rootless package and arm64e is roothide packages
Description: An awesome Orion tweak! //The description you will read when you go to install it
Maintainer: dustin //The person who is updating the tweak/debugging it
Author: dustin //The person who initialy made the tweak
Section: Tweaks //Where you will find the tweak in a repo
Depends: ${ORION}, firmware (>= 12.2) //Dependencies for your tweak
```

The *Makefile* this is one of the most important, because your tweak cant compile without it, first lets change the first and second line to:
```
TARGET := iphone:clang:latest:16.5
THEOS_PACKAGE_SCHEME=rootless
```
This will tell theos for what it should compile.

*Package.swift* This file is only needed for swift and we dont have to do anything in it.

*TextChangerTutorial.plist* This is what your jailbreak/semi-jailbreak needs to know what to inject to, for now we can leave it as is.

#### Okay, okay now ACTUALLY start coding
First open up a terminal and cd to the root directory of you tweak (TextChangerTutorial/), then type ```make spm```, the output should be > Creating SPM config… and then nothing

Now lets open *Tweak.x.swift* in the */Sources/TextChangerTutorial* directory there are 2 things in it *import Orion* and *import TextChangerTutorialC*
The first thing imports orion from THEOS and the seconds imports your (currently none) obj.-c code

So we have to start with some obj.-c to have ways to hook into the UI that you are trying to change, so go to */Sources/TextChangerTutorialC/include/Tweak.h*. Here is the simple code to do it:
```
#import <UIKit/UIKit.h>

@interface _UIStatusBarStringView : UILabel
@end
```
Easy, save the file and go back to *Tweak.x.swift* make a class by doing:
```
class TextChangerHook: ClassHook<UILabel> {
}
```
The part ```TextChangerHook:``` is the name of the class, ```ClassHook<>``` is the thing your class is and ```UILabel``` is what you are hooking into.

Now make a function inside your class to execute:
```
    func setText(_ text: String) {
        orig.setText("Hello world!")
    }
```
The ```setText()``` part is what the function should do and the ```"Hello world!"``` part is the text that overwrites ```UILabel```.
Now your entire code should look like:
```
import Orion
import TextChangerTutorialC

class TextChangerHook: ClassHook<UILabel> {
    func setText(_ text: String) {
        orig.setText("Hello world!")
    }    
}
```
Now save everything and compile! open a terminal and cd to the root directory of the tweak again and type ```make do```, you are gonna get 1 error because you are not doing this over ssh, this does not matter because 
theos should have created a folder named *packages* with inside it a .deb file with your tweak.

You can transfer the tweak to your device either by connecting it via usb or just mailing it to yourself.

After this you can install it like normal and then respring, if springboard crashes try respring again, if it does again, check if you didnt make any mistakes 

### You just created your first ever jailbreak tweak, hopefully of many.

if you need help or if something isnt working dm me on reddit u/Anonymous_16374

### This tutorial is far from done and i am gonna update it a bit more, but this is how you create the most basic of tweaks.

####### I Gotta give some credit to sourcelocation, his tutorial is most of my inspiration for this one, but its outdated and has no tutorials on how to install the tools.
