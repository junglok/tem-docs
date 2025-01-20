# SSH Login

!!! note "Enabling OTP"

    When you first connect to the login servers, you can log-in using only your password (or initial password), but you MUST immediately receive OTP (One-Time-Password)s for two-factor authentication. After the sucessful login, at ssh terminal, please follow the [GSDC OTP GUIDE](./otp.md) to enable it. 

## Linux/Mac Users

```bash

$> ssh -Y -o Port=<port> <userID>@tem-ui-al9.sdfarm.kr
    
```

```bash

$> ssh -Y -o Port=<port> <userID>@tem-cs-al9.sdfarm.kr
    
```

## Windows Users