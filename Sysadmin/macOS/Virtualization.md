# Links to Previous Versions of macOS

**Versions available on the Mac App Store:**
* [macOS Catalina](https://itunes.apple.com/us/app/macos-catalina/id1466841314?ls=1&mt=12)
* [macOS Mojave](https://itunes.apple.com/us/app/macos-mojave/id1398502828?ls=1&mt=12)
* [macOS High Sierra](https://itunes.apple.com/us/app/macos-high-sierra/id1246284741?ls=1&mt=12)

**Versions available from Apple's website:**
* [macOS Sierra](https://support.apple.com/en-us/HT208202) - [InstallOS.dmg](http://updates-http.cdn-apple.com/2019/cert/061-39476-20191023-48f365f4-0015-4c41-9f44-39d3d2aca067/InstallOS.dmg)
* [OS X El Capitan](https://support.apple.com/en-us/HT206886) - [InstallMacOSX.dmg](http://updates-http.cdn-apple.com/2019/cert/061-41424-20191024-218af9ec-cf50-4516-9011-228c78eda3d2/InstallMacOSX.dmg)
* [OS X Yosemite](https://support.apple.com/en-us/HT210717) - [InstallMacOSX.dmg](http://updates-http.cdn-apple.com/2019/cert/061-41343-20191023-02465f92-3ab5-4c92-bfe2-b725447a070d/InstallMacOSX.dmg)

# VMware Fusion "Failed to Create Installation Media"
Upon digging you may come across these lines in the Console:
```
FILE: FileLockCreateEntryDirectory creation failure on '/Applications/VMware Fusion.app/Contents/Resources/preformattedHFSVolume.vmdk.lck': Permission denied
FILE: FileLockIntrinsicPortable implicit S lock succeeded on '/Applications/VMware Fusion.app/Contents/Resources/preformattedHFSVolume.vmdk'.
FILE: FileLockCreateEntryDirectory creation failure on '/Applications/VMware Fusion.app/Contents/Resources/preformattedHFSVolume.vmdk.lck': Permission denied
FILE: FileLockIntrinsicPortable implicit S lock succeeded on '/Applications/VMware Fusion.app/Contents/Resources/preformattedHFSVolume.vmdk'.
```

I found [this script by rtrouton](https://github.com/rtrouton/create_os_x_vm_install_dmg) to help prepare a DMG that VMware Fusion would accept.