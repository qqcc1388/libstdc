Xcode10中删除了libstdc++库，这也导致老一点的项目，运行时报错缺少libstdc++库
解决办法就是网上找libstdc++并依次复制到对应的文件夹中
```
//MacOSX
/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX.sdk/usr/lib/
iPhone真机
/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/usr/lib/
iPhone模拟器
/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/SDKs/iPhoneSimulator.sdk/usr/lib/
```
每次复制都要去找文件夹，有时候还容易搞错，这里就用脚本解决一下复制的问题
将对应的libstdc++库分别存放在MacOSX  iPhoneOS  iPhoneSimulator等文件夹中 执行cp命令
```
#!/bin/bash

# Asking sudo
if [ $EUID != 0 ]; then
    sudo "$0" "$@"
    exit $?
fi

sudo cp MacOSX/* /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX.sdk/usr/lib/
sudo cp iPhoneOS/* /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/usr/lib/
sudo cp iPhoneSimulator/* /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/SDKs/iPhoneSimulator.sdk/usr/lib/
```
执行即可运行脚本
```
sh install.sh

或者执行
./install.sh

```
