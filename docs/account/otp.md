# OTP (One-Time-Password)

## **Two-factor Authentication (2FA) with OTP**

GSDC accounts use Two-Factor Authentication (2FA): your password is the first factor and a
6-digit One-Time-Password (OTP) from an authenticator app is the second. You register OTP on the
__[GSDC DigitalHub Portal](https://portal.gsdc.kr)__ during your first login, right after you set
a new password ([Requesting Accounts — Step 2](account.md#step-2-first-login-change-password-and-register-otp)).

!!! note "Download the step-by-step guide with screenshots (Korean)"

    [:octicons-download-24: Portal Sign-up & Research Group Guide](../GSDC-TEM-PORTAL-SIGNUP-GUIDE.pdf){ .md-button}

## **Before you start**

- [x] Your account has been approved and you received the e-mail with your __initial password__.
- [x] An authenticator app is installed on your smartphone — for example Google Authenticator.

## **Registering OTP**

1. __Log in with the initial password__ — on [https://portal.gsdc.kr](https://portal.gsdc.kr), enter only your ID and the initial password from the approval e-mail, then click __Log in__ (로그인).

    !!! tip "Leave the OTP field empty"

        You have no OTP yet when you log in with the initial password.

2. __Reset your password__ — enter a new password twice and click __Set password__ (비밀번호 설정). The password must be at least 9 characters and contain letters, numbers and special characters. You will see "비밀번호가 설정되었습니다. 새로운 OTP를 발급해주세요."
3. __Issue OTP__ — click __Issue OTP__ (OTP 발급) to show the QR code.
4. __Register it in your app__ — scan the QR code with your authenticator app.
5. __Confirm__ — enter the 6-digit number shown in the app and click __Confirm and finish__ (확인하고 완료). You will see "OTP 설정이 완료되었습니다. 비밀번호와 OTP로 다시 로그인해주세요."

!!! danger "Do not share the QR code"

    The QR code is the OTP key for your account. Do not take a screenshot of it or send it to anyone.

## **Logging in with OTP**

From now on, every login needs your password __and__ the current 6-digit number from your app.

- __Portal__ — enter your ID, password and the 6-digit OTP, then click __Log in__ (로그인).
- __Login nodes (SSH)__ — enter your password at `First Factor` and the 6-digit OTP at `Second Factor`. See [SSH Login](ssh.md).

!!! tip "Lost your phone or changed your app?"

    Use __OTP 초기화__ (reset OTP) or __비밀번호 및 OTP 초기화__ (reset password and OTP) under the login button on the portal.
