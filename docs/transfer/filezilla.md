# FileZilla

## Data transfer using FileZilla with 2FA

With the FileZilla global settings ("Edit" -> "Setttings"),

* In `Connection` menu, make sure to set `Timeout in seconds` value to `0`, it will not close and recreate idle sessions.

![filezilla-0](../images/filezilla-0.png)

Then, when editing and connecting a new site for SFTP (`File` -> `Site Manager` -> `New site`),

* In `General` tab, select SFTP as Protocol and enter `tem-ui-al9.sdfarm.kr` or `tem-cs-al9.sdfarm.kr` login server as Host. 
* In `General` tab, choose the Logon Type `interactive`, and with this setting, it will ask you for your password and OTP.
* In `Transfer Settings` tab, also make sure to check `Limit number of simultaneous connections` and leave the default value of 1.

![filezilla-1](../images/filezilla-1.png)
/// caption
`New site` -> `General`
///

![filezilla-2](../images/filezilla-2.png)
/// caption
`New site` -> `Transfer Settings`
///

