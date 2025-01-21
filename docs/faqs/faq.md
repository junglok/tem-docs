# Frequently Asked Questions (FAQs)

## Accounts / Password / One-Time-Password

??? question "How can I resolve the IPA command error when getting OTP?"

    This error occurs when the credentials issued by your authentication system, which are valid for one day, expire or become invalid. Here are the steps to resolve this problem. Open your terminal and execute the following command to obtain new credentials.
    
    ''' yaml
    $> kinit
    Password for (UserID)@SDFARM.KR: (Enter your password)
    '''

    Enter your password and press Enter to generate new credentials. Now, re-run the “ipa otptoken-add” command. It should execute without errors, using the newly generated credentials.

## SSH login, SSH teminal

## SFTP (Data transfer)

## X11 forwarding

