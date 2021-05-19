---
title: Make TextEdit open with a blank file by default
---

# Enable
```sh
$ defaults write com.apple.TextEdit NSShowAppCentricOpenPanelInsteadOfUntitledFile -bool false
```


# Disable
```sh
$ defaults write com.apple.TextEdit NSShowAppCentricOpenPanelInsteadOfUntitledFile -bool true
```