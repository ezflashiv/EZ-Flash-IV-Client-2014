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
export PATH=$PATH:$JAVA_HOME/bin:$ANT_HOME/bin:/home/knoppix/bin/eclipse:/home/knoppix/dev/mobile/sdks/sdk-android/build-tools:/home/knoppix/dev/mobile/sdks/sdk-android/tools
```

- either rerun terminal/relogin or run `source ~/.bashrc` to apply new `PATH`

- install *cordova*: `sudo npm install -g cordova`

- create first project: `mkdir -p ~/dev/mobile/workspace-android && cd $_ && cordova create hello com.example.hello HelloWorld`

- try to add `android` platform: `cordova platform add android` If you get an Error regarding missing SDK, then follow the instructions on the screen. Usually it's just a matter of launching `android` (SDK Manager) and installing missing SDK components. If getting SSLPeer error there, then go to `Tools` -> `Options` and select `Force https://...  http://` which will not use SSL to download components