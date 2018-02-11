## How to use Android and NDK without Android Studio under Linux

Since 2016, the recommended way to install the Android SDK and the NDK is to install [Android Studio](https://developer.android.com/studio/index.html). For some of us, this can be very cumbersome having to install an IDE to have access to a SDK.
The purpose of that page is to give you the steps (as in 2018) to compile and run an apk from the command line. Hopefully those steps will not change too much in the future.
I will cover the Linux case usage only, but this should be extensible.

### Installation
First, create a place where you will install the libraries:
```markdown
mkdir ~/usr
cd ~/usr
```

You will need download both the:
- [Android SDK](https://developer.android.com/studio/index.html) at the bottom of the page.
```markdown
unzip ~/downloads/sdk-tools-windows-3859397.zip
```
- [Android NDK](https://developer.android.com/ndk/downloads/index.html)
```markdown
unzip ~/downloads/android-ndk-r16b-linux-x86_64.zip
```

### Setup
In your `~/.bashrc` or `~/.zshrc`, add the following environment variables:

```markdown
export ANDROID_NDK_ROOT=$HOME'/usr/android-ndk-r16b'
export ANDROID_NDK_HOME=$HOME'/usr/android-ndk-r16b'
export ANDROID_HOME=$HOME'/usr/android-sdk/sdk'
```
Source your `~/.bashrc`/`~/.zshrc`

(I recommend using something like tmux to scroll and copy strings easily at that stage)
Now, it is time to download the SDK version you want to work with:
-- First, list all the available SDK:
```markdown
${ANDROID_HOME}/tools/android list sdk --all --extended
```
-- Then install the SDK/tools you want, as:
```markdown
${ANDROID_HOME}/tools/android update sdk --filter tools,platform-tools,build-tools-26.0.1
```

For the NDK, we need to grab the CMake plugin. Unfortunately, the previous android command seems to not fully support tools installation.
Thanksfully there is a workaround for that as decribed [here](https://github.com/Commit451/android-cmake-installer). Providing you have correctly sourced your `.*rc`, you can just type the following in:

```markdown
$ wget https://github.com/Commit451/android-cmake-installer/releases/download/1.1.0/install-cmake.sh
chmod +x install-cmake.sh
./install-cmake.sh
```
### Build
Grab the google samples:

```markdown
cd ~/projects
git clone https://github.com/googlesamples/android-ndk 
```

Let's go to one famous example:
```markdown
cd ~/projects/android-ndk/hello-jni
```

Just type in the following and enjoy :-)
```markdown
./gradlew assemble
```
