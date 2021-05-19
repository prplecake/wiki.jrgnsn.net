---
title: Your CLT does not support macOS 11
---

```
Error: Your CLT does not support macOS 11.
It is either outdated or was modified.
Please update your CLT or delete it if no updates are available.
Update them from Software Update in System Preferences or run:
  softwareupdate --all --install --force

If that doesn't show you an update run:
  sudo rm -rf /Library/Developer/CommandLineTools
  sudo xcode-select --install

Alternatively, manually download them from:
  https://developer.apple.com/download/more/.
```

Follow Homebrew's instructions:

```sh
$ sudo rm -rf /Library/Developer/CommandLineTools; sudo xcode-select --install
```

# See also
* <https://apple.stackexchange.com/questions/401899/homebrew-your-clt-does-not-support-macos-11-0>
