
# 📱 Build Android APKs Entirely on Your Android Device Using Termux (No PC, No Android Studio!)

Develop, compile, and build full-featured Android apps **directly on your Android phone** using **Termux**, **Gradle**, and the **Android SDK command-line tools** — no need for a PC or Android Studio.

---

## 🚀 Features

- Write and build Android apps fully inside Termux  
- Use OpenJDK 17 and Gradle 8.5 for fast builds  
- Manage Android SDK tools from command line  
- Lightweight, portable, and runs entirely on-device  
- Supports all Android APIs (compileSdk 30 and above)  
- Perfect for developers on the go or with low-resource setups  

---

## ⚙️ Setup Guide

### 1️⃣ Install Termux & Basic Tools

> **Important:**  
> Install Termux from the [official F-Droid release](https://f-droid.org/en/packages/com.termux/) — **do NOT use the Play Store version**.  
> The Play Store version lacks the `openjdk-17` package and other key components.

```bash
pkg update && pkg upgrade -y
pkg install openjdk-17 wget unzip zip git aapt aapt2 -y
````

---

### 2️⃣ Download and Configure Android SDK Command-line Tools

```bash
mkdir -p $HOME/android-sdk
cd $HOME/android-sdk

wget https://dl.google.com/android/repository/commandlinetools-linux-11076708_latest.zip -O cmdline-tools.zip
unzip cmdline-tools.zip
mkdir -p cmdline-tools/latest
mv cmdline-tools/* cmdline-tools/latest/
```

---


### 3️⃣ Download and Setup Gradle

```bash
cd
wget https://services.gradle.org/distributions/gradle-8.5-bin.zip
unzip gradle-8.5-bin.zip -d $HOME/.gradle
```
---
### 4️⃣ Set Environment Variables

Add the following lines to your `~/.bashrc`, `~/.zshrc`, or `~/.profile`:

```bash
export ANDROID_HOME=$HOME/android-sdk
export PATH=$ANDROID_HOME/cmdline-tools/latest/bin:$ANDROID_HOME/platform-tools:$PATH
export PATH=$HOME/.gradle/gradle-8.5/bin:$PATH
```

Apply them immediately with:

```bash
source ~/.bashrc
```

---

### 5️⃣ Accept Licenses and Install Required SDK Packages

```bash
yes | sdkmanager --licenses
sdkmanager "platform-tools" "platforms;android-30" "build-tools;30.0.3"
```


---

### 6️⃣ Override AAPT2 to Use Termux's Native Version

```bash
echo 'android.aapt2FromMavenOverride=/data/data/com.termux/files/usr/bin/aapt2' >> ~/.gradle/gradle.properties
```

---

### 7️⃣ Enable Storage Access for Termux

```bash
termux-setup-storage
```

> Accept the Android permission prompt to grant storage access.

---

## 📦 Build Your Android App

Navigate to your project folder and build:

```bash
cd ~/AndroidIDEProjects/MyApp
gradle assembleDebug
```

---

## 📲 Install APK

After building your app, the APK file is located at:

```

app/build/outputs/apk/debug/app-debug.apk

````

To install the APK on your device:

1. Copy the APK to shared storage:

```bash
cp app/build/outputs/apk/debug/app-debug.apk /sdcard/
````

2. Open your device’s **File Manager** app.

3. Navigate to the **/storage/emulated/0/** folder.

4. Tap the `app-debug.apk` file to start the installation process.

> **Note:** Using a file manager to install the APK is recommended, as some command-line methods like `termux-open` may not work reliably on all devices.



---

## 🧰 Helpful Tools for Development

| Tool        | Purpose                        |
| ----------- | ------------------------------ |
| `logcat`    | View app logs and debug output |
| `git`       | Version control                |
| `apksigner` | Sign release APKs              |
| `zipalign`  | Optimize APKs                  |

---

## 🤖 Why Use Termux for Android Development?

* Complete Android development environment right on your phone
* No need for PC or heavy IDEs — just Termux and a code editor
* Perfect for hacking, learning, or coding on-the-go
* Lightweight and efficient for low-resource devices

---

## 💬 Credits

Created and tested by Arif Chowdhury
Built on Termux with OpenJDK 17, Gradle 8.5, and Android SDK cmdline-tools.

---

## 🛡️ License

MIT License

---

## ⭐ Star This Repo if You Find It Useful!

Help others discover how to build Android apps fully on their devices!
