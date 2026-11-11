# Requesting accounts

User accounts and research groups for the GSDC TEM cluster are requested on the
__[GSDC DigitalHub Portal](https://portal.gsdc.kr)__. The principal investigator (PI) signs up
first, then requests a research group. A service manager must approve each request, and you
get an e-mail when it is approved.

!!! note "Download the step-by-step guide with screenshots (Korean)"

    [:octicons-download-24: Portal Sign-up & Research Group Guide](../GSDC-TEM-PORTAL-SIGNUP-GUIDE.pdf){ .md-button}

## **Overview**

| Step | What you do | Approval |
|---|---|---|
| 1. Sign up | Request an account on the portal | Service manager approves |
| 2. First login | Log in with the initial password from the approval e-mail, then set a new password and register OTP | — |
| 3. Research group | Request a new research group with the group name you were given | Service manager approves |
| 4. Start analysis | Use your group's scratch directory and submit jobs | — |

## **Before you start**

Have the following ready:

- [x] __Your institutional or university e-mail address__ — use the PI's own address. The account created with it becomes the representative of the research group.
- [x] __The account name (ID) you were given__ — entered as the ID when you sign up.
- [x] __The group name you were given__ — for example `gOOOO`, entered when you request the research group.
- [x] __Contact details of the practical contact person__ — name, e-mail and phone number. These are required in the group description.
- [x] __An authenticator app on your smartphone__ — for example Google Authenticator, used to register OTP.

## **Step 1. Sign up (create an account)**

1. Open [https://portal.gsdc.kr](https://portal.gsdc.kr) and click __Sign up__ ("아직 계정이 없으신가요? 회원가입") at the bottom of the login screen.
2. __Consent to personal information collection__ — review the items, purpose and retention period, then click __Agree and continue__ (동의하고 계속하기).
3. __Select a community__ — choose __TEM__ and click __Next__ (다음). Accounts in the TEM community are added to the `tem_users` group by default.
4. __Verify your e-mail__ — enter your e-mail, click __Send verification e-mail__ (인증메일 보내기), then enter the 6-digit code from the e-mail and click __Verify__ (인증하기).

    !!! warning "Use the PI's institutional or university e-mail"

        The account created with this e-mail becomes the representative of the research group.

5. __Enter account details__
    1. __ID__ — enter the account name you were given and click __Check availability__ (중복확인).
    2. Enter your __last name / first name__.
    3. Enter your __institution__ and __department__.
    4. __PI name__ is optional. Fill it in or leave it blank as the screen instructs.
    5. Click __Sign up__ (회원가입). You will see "회원가입 요청이 성공적으로 접수되었습니다."

!!! info "Waiting for approval"

    When a service manager approves the request, you get an e-mail with your __initial password__. Continue with Step 2 after it arrives.

## **Step 2. First login — change password and register OTP**

1. __Log in with the initial password__ — enter only your ID and the initial password from the approval e-mail, then click __Log in__ (로그인).

    !!! tip "Leave the OTP field empty"

        You have no OTP yet when you log in with the initial password.

2. __Reset your password__ — enter a new password twice and click __Set password__ (비밀번호 설정). The password must be at least 9 characters and contain letters, numbers and special characters.
3. __Issue OTP and register it in your app__
    1. Click __Issue OTP__ (OTP 발급) to show the QR code.
    2. Scan the QR code with your authenticator app.
    3. Enter the 6-digit number shown in the app and click __Confirm and finish__ (확인하고 완료).
    4. Log in again with your new password and OTP.

!!! danger "Do not share the QR code"

    The QR code is the OTP key for your account. Do not take a screenshot of it or send it to anyone.

## **Step 3. Request a new research group**

You can use a scratch directory and submit analysis jobs only after your research group is approved.

1. Log in with your __ID, new password and the 6-digit OTP__ from your app.
2. In the left menu, go to __Research Group__ (연구그룹) → __Group List__ (그룹 목록), then click __+ New Group__ (+ 신규 그룹 생성) at the top right. The `tem_users` group in the list is the default group of the TEM community.
3. Fill in the request form:
    1. __Group name__ — the group name you were given (for example `gOOOO`).
    2. __Group description (required)__ — the name, e-mail and phone number of the practical contact person, in addition to the PI. For example:

        ```text
        실무담당자: 홍길동 / gildong@university.ac.kr / 010-0000-0000
        ```

        We use this contact for questions about accounts, jobs and data migration.

    3. Click __Submit request__ (요청 제출) and then __OK__ (확인) in the confirmation dialog. You will see "그룹 생성 요청이 성공적으로 제출되었습니다."

!!! info "Waiting for approval"

    When a service manager approves the group, you get an e-mail.

## **After approval**

Once approved, you can use the cluster from the GSDC TEM login nodes over [SSH](ssh.md).

| Approval | What you can do on the login nodes |
|---|---|
| Account approved | Access your home directory. You __cannot__ submit analysis jobs yet. |
| Research group approved | Use your group's scratch directory, upload data and submit analysis jobs. |

Your group's scratch directory:

| Project | Path | Available |
|---|---|---|
| New project | `/tem/scratch/sOOOO` | Right after the research group is approved |
| Existing project | `/tem/scratch/<GroupDir>` | After the data in your existing scratch directory has been migrated |

Useful commands:

- [`cluster.quota`](../service/util.md#clusterquota) — shows the home and scratch directories you can access, with their quota and usage.
- [`cluster.monitor`](../service/util.md#clustermonitor) — monitors the analysis jobs you submitted.
