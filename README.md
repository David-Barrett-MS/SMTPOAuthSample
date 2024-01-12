# SMTPOAuthSample

This is a sample console application written in .Net Core that demonstrates how to obtain an OAuth token for sending a message using SMTP.  Note that SMTP is a public protocol and as such it is up to the developer to correctly implement it in their code. The example here is basic, and only intended to show how OAuth fits in to the log-in process. This sample also demonstrates how to implement STARTTLS (required for Office 365, and recommended everywhere).

You must register the application in Azure AD as per [this guide](https://docs.microsoft.com/en-us/exchange/client-developer/legacy-protocols/how-to-authenticate-an-imap-pop-smtp-application-by-using-oauth#get-an-access-token "Authenticate an IMAP application using OAuth").  You must add a redirect URL of http://localhost (that requirement is specific to this example; if required you can update the redirect URL in the source code).

Once the application is registered, the application can be run from a command prompt (or PowerShell console).  The syntax is:

Delegate flow:
`SMTPOAuthSample TenantId ApplicationId <EmailFile>`

App (client credential) flow:
`SMTPOAuthSample TenantId ApplicationId SecretKey Mailbox <EmailFile>`

`<EmailFile>` is optional, but if specified it will be sent as the DATA part of the SMTP conversation (it should be a standard MIME file in .eml format).  This can be useful for replaying/testing messages.  If this parameter is missing, a simple test message is created instead.

If using delegate flow, you will be prompted to log-in via a browser.  If successful, the mail is sent from the mailbox of the authenticated user.  For client credential flow, the mailbox is specified in the parameters with the secret key, and no user input is required.

A successful test (delegate flow) looks like this:

![SMTPOAuthSample Successful Test Screenshot](https://github.com/David-Barrett-MS/SMTPOAuthSample/blob/master/SMTPOAuthSampleScreenshot.png?raw=true "SMTPOAuthSample Successful Test Screenshot")
