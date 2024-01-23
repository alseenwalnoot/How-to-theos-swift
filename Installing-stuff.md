### First things first, swift make sure you have swift installed (specificaly [5.8.1 RELEASE](https://download.swift.org/swift-5.8.1-release/ubuntu2204/swift-5.8.1-RELEASE/swift-5.8.1-RELEASE-ubuntu22.04.tar.gz), that works for me!).
### The swift website is REALLY unclear on how to install it so here is the guide to it:

Step 1: get the swift tarball from above

Step 2: Get the dependencies with ```sudo apt-get install \
          binutils \
          git \
          gnupg2 \
          libc6-dev \
          libcurl4-openssl-dev \
          libedit2 \
          libgcc-9-dev \
          libpython3.8 \
          libsqlite3-0 \
          libstdc++-9-dev \
          libxml2-dev \
          libz3-dev \
          pkg-config \
          tzdata \
          unzip \
          zlib1g-dev```

Step 3: Extract the tarball (you can do this with the ubuntu file manager or ```tar xzf swift-5.8.1-RELEASE-ubuntu22.04.tar.gz```)

Step 4: Add /home/YOURUSERNAME/Downloads/swift-5.8.1-RELEASE-ubuntu22.04/usr/bin to path (you can also mv the swift directory to something easier if you dont want swift in your downloads, to do this do 

```mv /home/YOURUSERNAME/Downloads/swift-5.8.1-RELEASE-ubuntu22.04 /home/YOURUSERNAME/Documents/swift``` 

where /home/YOURUSERNAME/Documents/swift is any place you want) to add it to your path do 

```sudo nano .bashrc``` 

and at the end add ```export PATH=/YOUR/SWIFT/PATH/usr/bin:$PATH``` at the end, click CTRL+X, then y, then enter to save the .bashrc file. make sure after the swift path you have /usr/bin, because this is where the swift binaries are.

Step 5: Reboot your computer to make swift added to your path.

Step 6: ***"SANITY CHECK"*** to check if swift is installed run ```swift --version```, the output should be "Swift version 5.8.1 (swift-5.8.1-RELEASE)
Target: x86_64-unknown-linux-gnu".

### Next, you need THEOS, here is how to install it:

Step 1: Get the dependencies with ```sudo apt install bash curl```.

Step 2: Install THEOS with ```bash -c "$(curl -fsSL https://raw.githubusercontent.com/theos/theos/master/bin/install-theos)"```, if it ask for some toolchain of sorts say y or yes.

Step 3: After it is done, reboot.

Step 4: ***"SANITY CHECK, again"*** do ```echo $THEOS``` the output should be "/home/YOURUSERNAME/theos"

Step 5: Select the orion branch by first going to theos directory, ```cd $THEOS``` then do ```git fetch && git checkout orion && git submodule update --init```.

### You would also need the Orion tweak from chariz repo (or roothide repo if you are on bootstrap) installed on the device where you are gonna put your tweak
