## Examining what theos made for us and making changes
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
