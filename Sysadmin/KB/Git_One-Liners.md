---
title: Git One-Liners
---

# Create tag with list of commits by author since last tag

```sh
git shortlog "$(git describe --tags --abbrev=0)..HEAD" | git tag -a -F - "TAG_NAME"
```

Pipe it through `vipe` if you need to edit the text:

```sh
git shortlog "$(git describe --tags --abbrev=0)..HEAD" | vipe | git tag -a -F - "TAG_NAME"
```