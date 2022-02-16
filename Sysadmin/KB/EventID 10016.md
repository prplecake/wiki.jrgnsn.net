> The application-specific permission settings do not grant Local Activation permission for the COM Server application with CLSID
>
> {D63B10C5-BB46-4990-A94F-...}
>
> and APPID
>
> {9CA88EE3-ACB7-47C8-AFC4-...}
>
> to the user contoso\you_admin SID (S-1-5-21-3763...) from address LocalHost (Using LRPC) running in the application container Unavailable SID (Unavailable). This security permission can be modified using the Component Services administrative tool.

I'm trying to install a piece of software on many servers without having to manually go into each.

```powershell
Invoke-Command -ComputerName DC01 -Credential contoso\you_admin -ScriptBlock {
    Start-Process msiexec "/i \\dc01\Utilities\check_mk_agent.msi /qn /L*V 'C:\msiexec.log'"
}
```

I was able to Enter-PSSession to install the software, but that's still over-handling. I should be able to:

```powershell
$computers = @("SRV01", "SRV02", "SRV03")
foreach ($computer in $computers) {
    Invoke-Command -ComputerName $computer -ScriptBlock {
        msiexec \\dc01\Utilities\check_mk_agent.msi /qn
    }
}
```

## Resolution

Granting **NETWORK SERVICE** the following DCOM rights on the target server:

* Local Launch
* Remote Launch
* Local Activation
* Remote Activation

To resolve the issue:

1. Launch `dcomcnfg.exe`.
2. **Component Services** -> **Computers** -> **My Computer**. **Right-click** My Computer -> **Properties**
3. Click over to the **COM Security** tab, then click **Edit Default...** under **Launch and Activation Permissions**
4. Add **NETWORK SERVICE** and allow them all four permissions.
