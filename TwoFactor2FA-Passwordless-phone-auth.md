# Password-less and Two Factor (2FA) authentication

Overview of using apps such  DUO Mobile, Google Authenticator, Authy, 1Password, and Windows Authenticator for password-less or 2FA authentication.

- [Password-less and Two Factor (2FA) authentication](#password-less-and-two-factor-2fa-authentication)
  - [Password-less](#password-less)
    - [Proprietary](#proprietary)
    - [WebAuthN password-less](#webauthn-password-less)
  - [2FA](#2fa)
    - [WebAuthN 2FA](#webauthn-2fa)
    - [Push notifications in app](#push-notifications-in-app)
    - [Software Tokens - Time based one time password (TOTP)](#software-tokens---time-based-one-time-password-totp)
  - [Links](#links)

## Password-less

### Proprietary 
Companies like Microsoft ([Microsoft Authenticator](https://support.microsoft.com/en-us/account-billing/sign-in-to-your-accounts-using-the-microsoft-authenticator-app-582bdc07-4566-4c97-a7aa-56058122714c)) and Google ([Google Prompt](https://support.google.com/accounts/answer/6361026?hl=en&co=GENIE.Platform%3DiOS&oco=0)) allow you to login to a website or app on your computer by sending a message to their proprietary app on the users device. The user clicks "yes it's me" and is then logged into the website or app.

### WebAuthN password-less
Allows user to login using a hardware key, on-device biometrics, such as fingerprint readers, Face ID, Windows Hello etc. without needing a password (but still a PIN in some cases).
[Here](https://sec.okta.com/articles/2020/04/webauthn-great-and-it-sucks) is a great summary of the current state of WebAuthN (as of 4/1010. May be different now). Summary, it's not well supported yet and still has a lot of friction for regular users.

## 2FA 

### WebAuthN 2FA
In addition to [WebAuthN Password-less](#webauthn-password-less) above, WebAuthN can be used for the 2nd factor of password authentication. Instead of an email or text message, the user is prompted to scan their fingerprint or insert their hardware key. This is slightly more common than the password-less model above. 

### Push notifications in app
The user logs into a site with a password and then then a notification is sent ot the phone asking "is this you?". This  is similar to the [proprietary apps from Microsoft and google](#proprietary) except you do need to enter a 1st factor password before being prompted by the app. See example in [this](https://youtu.be/kFQfA50FSmg?t=219) video.

Apps such as [Authy](https://www.twilio.com/authy/features/push) and [Duo Moble](https://duo.com/product/multi-factor-authentication-mfa/authentication-methods/duo-push) offer paid services to allow the push notification for the 2nd factor.

### Software Tokens - Time based one time password (TOTP)
This is the most popular way to use an app for 2FA. Many apps such as DUO Mobile, Google Authenticator, Authy, 1Password, and Windows Authenticator have support for TOTP.

The site shares a seed with the app to synchronize the algorithm (usually with a QR code). When the user logs into the site, the site asks for a code. The user gets the code from the app and uses it to login. 

[Here](https://authy.com/guides/slack/) is an example of the flow for setting up a software token app.

## Links

- [WebAuthn Is Great and It Sucks](https://sec.okta.com/articles/2020/04/webauthn-great-and-it-sucks)
- [Microsoft Authenticator](https://support.microsoft.com/en-us/account-billing/sign-in-to-your-accounts-using-the-microsoft-authenticator-app-582bdc07-4566-4c97-a7aa-56058122714c)
- Okta
  - [Okta Passwordless Authentication](https://www.okta.com/passwordless-authentication/)
- [Enable QR Code generation for TOTP authenticator apps in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/security/authentication/identity-enable-qrcodes?view=aspnetcore-5.0)
- [Password-less FIDO2 vs FIDO U2F](https://www.reddit.com/r/1Password/comments/epbp2t/does_1password_make_use_of_fido2_resident_keys/)
- [FIDO2](https://hideez.com/blogs/news/fido2-explained)
- [FIDO2 .NET Library (WebAuthn)](https://github.com/passwordless-lib/fido2-net-lib)
  - [Info about using the library](https://docs.passwordless.dev/guide/getting-started.html#introduction)
- Authy
  - [See Authy push in action](https://www.youtube.com/watch?v=kFQfA50FSmg&t=220s)
  - [Setup TOTP in Slack](https://authy.com/guides/slack/)