---
title: Linux - Basic Tips and Tricks
---

# Repeating Commands

* `!!` repeats the last command entered.
  * Can be used with `sudo`, i.e.: `sudo !!` to run the last command with superuser privileges.
* `!string` - Type an exclamation point followed by a string of letters that begin a command. The last command that begins with the letters is repeated. 
* `!n` - Type an exclamation point followed by a number. The command shown on that line number in command history is repeated.

# Editing previous command

You can edit the previous command and reenter it using `^old^new`. The following command will replace `string1` with `string2` in the first command that just executed:

```
srot test.txt
^ro^or
```