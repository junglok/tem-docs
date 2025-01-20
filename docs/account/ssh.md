# SSH Login

!!! note "Enabling OTP"

    When you first connect to the login servers, you can log-in using only your password (or initial password), but you MUST immediately receive OTP (One-Time-Password)s for two-factor authentication. After the sucessful login, at ssh terminal, please follow the [GSDC OTP GUIDE](./otp.md) to enable it. 

## Linux/Mac Users

=== "tem-ui-al9.sdfarm.kr"
    ``` yaml linenums="1"
    $> ssh -Y -o Port=<port> <userID>@tem-ui-al9.sdfarm.kr
    First Factor:
    Second Factor(optional):
    ```

=== "tem-cs-al9.sdfarm.kr"
    ``` yaml linenums="1"
    $> ssh -Y -o Port=<port> <userID>@tem-cs-al9.sdfarm.kr
    First Factor:
    Second Factor(optional):
    ```

!!! note

    * line 1: `-Y (-X)` means enabling trused (or untrusted) X11 forwarding. `port` is designated port number informed by administrator.
    * line 2: `First Factor` means your own password string.
    * line 3: `Second Factor` means six digits OTP code. You can input just `enter` if you have not enabled OTP yet.


## Windows Users

``` yaml
theme:
  features:
    - content.code.annotate # (1)
```

1. :man_raising_hand: I'm a code annotation! I can contain `code`, __formatted
    text__, images, ... basically anything that can be written in Markdown.