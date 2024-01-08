.. |newi| image:: images/new-24.png

********************************************************************
Two-factor Authentication (2FA) with One-Time-Password (OTP) |newi|
********************************************************************

2FA with One-Time-Passowrd (OTP) Guide
======================================

We have introduced a Two-Factor Authentication (2FA) using One-Time-Password (OTP) to enhance the security environment. Please follow the GSDC OTP guide (written in both Korean and English) through the link below 
to enable it on your TEM account. Note that you must follow the guide when you are already logged in. 

* `GSDC OTP Guide <https://gsdc-farm.gitbook.io/gsdc-otp/>`_

You are strongly recommended to do so as soon as possible because once all TEM user accounts are OTP enabled, then we plan to suspend the policy requiring source IPs. 

We hope your cooperation and please do not hesitate to contact us if you have any questions.


2FA Tips and Tricks
===================

How can I use SSH/SFTP GUI with 2FA?
------------------------------------

Your client (e.g., Linux/Mac GUI terminal) programs may natively support interactive or multi-factor authentication methods. However, many GUI programs do not have this functionality built in.

Known GUI applications for SSH that support 2FA natively:

    * GUI terminal programs (for Linux or Mac) : `SSH via GUI teminals <https://tem-docs.readthedocs.io/en/latest/guide.html#for-linux-mac-users>`_  
    * MobaXterm (for Windows only) : `SSH via MobaXterm <https://gsdc-farm.gitbook.io/gsdc-otp/login-with-otp#mobaxterm-connecting-via-mobaxterm-on-windows>`_
    * XShell (for Windows only) : `SSH using Xshell <https://gsdc-farm.gitbook.io/gsdc-otp/login-with-otp#xshell-connecting-using-xshell>`_
    * Putty

Known GUI applications for SFTP that support 2FA natively:

    * FileZilla (for both Windows and Linux/Mac) : see :ref:`filezilla_with_2fa`
    * WinSCP (for only Windows) : see :ref:`winscp_with_2fa`


.. _filezilla_with_2fa:
How can I use FileZilla with 2FA?
---------------------------------

Choose the Logon Type “interactive” and it will ask you for your password and OTP. Also make sure to check “Limit number of simultaneous connections” under “Transfer Settings” and leave the default value of 1.

.. _winscp_with_2fa:
How can I use WinSCP with 2FA?
------------------------------

TBD

