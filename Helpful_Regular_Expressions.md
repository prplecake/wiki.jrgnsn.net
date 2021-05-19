---
title: Helpful Regular Expressions
---

* [RegExr](https://regexr.com)

# IP Address RegEx

**Perl:**
```perl
(?:(?:25[0-5]|2[0-4]\d|1\d\d|[1-9]?\d)\.){3}(?:25[0-5]|2[0-4]\d|1\d\d|[1-9]?\d)
```
Source: <http://ipregex.com/>

If you're scanning an INI file, this regex will ignore commented lines[^1]
```perl
^(?:\w+=)(?:(?:25[0-5]|2[0-4]\d|1\d\d|[1-9]?\d)\.){3}(?:25[0-5]|2[0-4]\d|1\d\d|[1-9]?\d)$
```
This regex will match as long as the line begins with a word.

[^1]:Line comments in INI files begin with a semicolon (`;`)