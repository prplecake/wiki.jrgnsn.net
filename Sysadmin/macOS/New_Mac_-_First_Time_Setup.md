---
title: New Mac - First Time Setup
---

This assumes you've already gone through the main on-boarding process and have signed into iCloud, et al.

**Install [Homebrew](https://brew.sh/):**

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

**Get [dotfiles](https://git.sr.ht/~mjorgensen/dotfiles):**

```
git clone https://git.sr.ht/~mjorgensen/dotfiles ~/.dotfiles
cd ~/.dotfiles; git submodule update --init
./scripts/install.sh
```

# Change Default Behaviors
## TextEdit: Open with a blank document by default
### Enable

```
defaults write com.apple.TextEdit NSShowAppCentricOpenPanelInsteadOfUntitledFile -bool false
```

### Disable

```
defaults write com.apple.TextEdit NSShowAppCentricOpenPanelInsteadOfUntitledFile -bool true
```
