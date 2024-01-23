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
