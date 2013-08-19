It's extremely important to update the packages repos right after fresh Knoppix install and before installing packages:

- apt-get update

#### Misc utilities

- apt-get install unrar

#### Developing mobile apps with Cordova (aka PhoneGap)

- install NodeJS as described [here](https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager#debian-lmde)

- download [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) and extract to `~/bin/jdk*`

- download [Ant](http://ant.apache.org/bindownload.cgi) and extract to `~/bin/apache-ant-*`

- download [Android ADT bundle with SDK](http://developer.android.com/sdk/) and extract. Move `sdk` directory to `~/dev/mobile/sdks/android-sdk` and `eclipse` directory to `~/bin/eclipse`

- now let's setup `PATH`. Create `~/.bashrc` with following contents (assuming jdk's version is 1.7.0_25 and ant's version is 1.9.2, change accordingly for your versions/directory names):

```
export JAVA_HOME=/home/knoppix/bin/jdk1.7.0_25
export ANT_HOME=/home/knoppix/bin/apache-ant-1.9.2
export PATH=$PATH:$JAVA_HOME/bin:$ANT_HOME/bin:/home/knoppix/bin/eclipse:/home/knoppix/dev/mobile/sdks/sdk-android/platform-tools:/home/knoppix/dev/mobile/sdks/sdk-android/tools
```

- either rerun terminal/relogin or run `source ~/.bashrc` to apply new `PATH`

- install *cordova*: `sudo npm install -g cordova`

- create first project: `mkdir -p ~/dev/mobile/workspace-android && cd $_ && cordova create hello com.example.hello HelloWorld`

- try to add `android` platform: `cordova platform add android` If you get an Error regarding missing SDK, then follow the instructions on the screen. Usually it's just a matter of launching `android` (SDK Manager) and installing missing SDK components. If getting SSLPeer error there, then go to `Tools` -> `Options` and select `Force https://...  http://` which will not use SSL to download components

- create an emulator in Android SDK Manager (launch with `android`) by clicking on `Tools` -> `Manage AVDs`

- launch app in emulator - `codrova emulate android` If emulator crashes with error that contains something like `munmap_chunk() invalid pointer` make sure to create localtime file every time you login (otherwise it will be overwritten after next reboot), so add following to your `~/.bashrc`: `sudo ln -sf /usr/share/zoneinfo/US/Eastern /etc/localtime`. Instead of `cordova emulate android` you could run commands manually:
  - `cordova prepare android`
  - `cordova compile android`
  - `./platforms/android/cordova/lib/list-emulator-images to list all available images (let's say there is image called `GalaxyS4` and we want to use that one)
  - `./platforms/android/cordova/lib/start-emulator GalaxyS4` to launch emulator. Wait some minutes here
  - `./platforms/android/cordova/lib/install-emulator` to install package in the emulator. You may get an error on auto-launch here, just try to launch an app manually and most likely it will launch if all was correct on your end

- connect real Android device and execute `cordova run android` to prepare, compile and install on device or alternatively you could go run everything manually:
  - `cordova prepare android` to pack cordova project source files
  - `cordova compile android` to compile cordova project files using Android SDK into a package
  - `./platforms/android/cordova/lib/list-devices` to verify device is in the list
  - `./platforms/android/cordova/lib/install-device` to install app on device. You may get an error on app auto-launch here, just try to launch an app manually and most likely it will launch if all was correct on your end