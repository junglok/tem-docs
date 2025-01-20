# SSH Login

!!! note "Enabling OTP"

    When you first connect to the login servers, you can log-in using only your password (or initial password), but you MUST immediately receive OTP (One-Time-Password)s for two-factor authentication. After the sucessful login, at ssh terminal, please follow the [GSDC OTP GUIDE](./otp.md) to enable it. 

## Linux/Mac Users

=== "tem-ui-al9.sdfarm.kr"
    ```bash

    $> ssh -Y -o Port=<port> <userID>@tem-ui-al9.sdfarm.kr # (1)
    First Factor: # (2)
    Second Factor(optional): # (3)    
    ```
=== "tem-cs-al9.sdfarm.kr"
    ```bash

    $> ssh -Y -o Port=<port> <userID>@tem-cs-al9.sdfarm.kr
    First Factor:
    Second Factor(optional):

    ```
1.  :man_raising_hand: `-Y (-X)` means enabling trused (or untrusted) X11 forwarding. __<port>__ is designated port informed by administrator.
2.  :man_raising_hand: `First Factor` means your own password.
3.  :man_raising_hand: `Second Factor` means 6 digits OTP code (You can input just <enter> if you have not enabled OTP yet)

## Windows Users