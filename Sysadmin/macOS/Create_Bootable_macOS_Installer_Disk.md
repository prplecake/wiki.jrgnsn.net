1. Connect an USB drive to your Mac. In these examples I'll use _UNTITLED_ as the name of the USB drive. Take note if your drive is named something else.
2. Launch a terminal.
3. Run the following command:
```
sudo /Applications/Install\ macOS\ Catalina.app/Contents/Resources/createinstallmedia --volume /Volumes/UNTITLED -- /Applications/Install\ macOS\ Catalina.app
```

You'll be warned that the drive will be erased. Enter `Y` to allow it.

To boot from the USB drive, hold down the Option key while the Mac boots.

# Notes

* macOS Catalina requires a minimum 16 GB USB drive. All other previous versions only required an 8 GB drive.