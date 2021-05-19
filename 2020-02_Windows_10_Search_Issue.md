---
title: 2020-02 Windows 10 Search Issue
---

Sometime during the night before 2020-02-05, Microsoft seemed to push an update to Windows 10 devices breaking search.[^1]

[^1]:<https://www.computerworld.com/article/3519708/has-your-win10-search-box-gone-black-does-search-even-work.html>

Here's a potential fix[^2]:

[^2]:<https://answers.microsoft.com/en-us/windows/forum/windows_10-win_cortana/cortana-not-working-search-just-showing-empty/d208fa6e-9524-4cce-991a-fc9c9cca7f55>

This process requires the involvement of a domain administrator, or second local administrator account.

1. Log out of the main user account. Log in with an administrator account.
2. Navigate to **C:\Users\<ProblemUserAccount>\AppData\Local\Packages**.<br>**Note:** You may need to grant yourself permission to access the <ProblemUserAccount>'s folder.
3. Find the folder that being with **Microsoft.Windows.Cortana_...**
4. **Rename** that folder, appending `.old`
5. Logout of your administrator account and the <ProblemUserAccount> should be able to use search again.