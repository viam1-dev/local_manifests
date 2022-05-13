# Local Manifest for Samsung Galaxy J1 ace DUOS (j1pop3g)

## Notes

- You need Ubuntu version 18.04 or higher.
- This will create 2 directories in your `~` *(home)* directory:
  - `~/android`
  - `~/.jdk_6`


## Downloading Source

```sh
cd ~/android
repo init --depth=1 -u https://github.com/LineageOS/android.git -b cm-11.0 # Initialize LineageOS source code
git clone --depth=1 --single-branch -b cm-11.0 https://github.com/J110H-Android/local_manifests.git .repo/local_manifests # Download local manifest
repo sync -c --force-sync --optimized-fetch -j$(nproc --all) # Start syncing
```

## Setting Up Enviroment

Install required dependencies and set Python 2 as default:

```sh
sudo apt-get install git-core gnupg flex bison build-essential \
    zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 \
    libncurses5 lib32ncurses5-dev x11proto-core-dev libx11-dev \
    lib32z1-dev libgl1-mesa-dev libxml2-utils xsltproc unzip \
    fontconfig schedtool axel gperf file

sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.7 10
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python2.7 3
sudo update-alternatives --set python3 /usr/bin/python2.7
```

## Installing JDK 6

```sh
mkdir ~/.jdk_6
cd ~/.jdk_6
axel -q -n $(nproc --all) https://repo.huaweicloud.com/java/jdk/6u45-b06/jdk-6u45-linux-x64.bin
chmod +x jdk-6u45-linux-x64.bin
./jdk-6u45-linux-x64.bin
sudo update-alternatives --install /usr/bin/javac javac  $PWD/jdk1.6.0_45/bin/javac 1
sudo update-alternatives --set javac $PWD/jdk1.6.0_45/bin/javac
sudo update-alternatives --install /usr/bin/java java  $PWD/jdk1.6.0_45/bin/java 1
sudo update-alternatives --set java $PWD/jdk1.6.0_45/bin/java
sudo update-alternatives --install /usr/bin/javaws javaws  $PWD/jdk1.6.0_45/bin/javaws 1
sudo update-alternatives --set javaws $PWD/jdk1.6.0_45/bin/javaws
sudo update-alternatives --install /usr/bin/javadoc javadoc  $PWD/jdk1.6.0_45/bin/javadoc 1
sudo update-alternatives --set javadoc $PWD/jdk1.6.0_45/bin/javadoc
sudo update-alternatives --install /usr/bin/javah javah  $PWD/jdk1.6.0_45/bin/javah 1
sudo update-alternatives --set javah $PWD/jdk1.6.0_45/bin/javah
sudo update-alternatives --install /usr/bin/javap javap  $PWD/jdk1.6.0_45/bin/javap 1
sudo update-alternatives --set javap $PWD/jdk1.6.0_45/bin/javap
sudo update-alternatives --install /usr/bin/jar jar  $PWD/jdk1.6.0_45/bin/jar 1
sudo update-alternatives --set jar $PWD/jdk1.6.0_45/bin/jar
```

## Building LineageOS

```sh
cd ~/android
source build/envsetup.sh
export ALLOW_MISSING_DEPENDENCIES=true
export LC_ALL=C
lunch lineage_j1pop3g-eng
mka
```
