# More Web Vulnerabilities

## Phishing

- Type of Phishing:
  - Server Hijacking: Manipulating the legitimate website to steal information.
  - Client Hijacking: Manipulating your computer to steal information.
  - Impersonation:
    - Setting up false websites to steal information.
    - Sending false emails/messages.
    - Using phishing kits/reverse proxy sites.
  - Take HTML from a good site, modify it to make it malicious.


## Impersonation

- Set up a website that looks like the legitimate website.
- Add forms to collect login information or other personal information, in the same manner as the legitimate site.
- Trick the user into visiting the website.
- Techniques:
  - Modify the downloaded website to point to the phishing collector.
  - Write an email linking to the website.
  - Send the email to as many people as possible.
  - Set up a phishing collector.
  - Download the legitimate website.
  - Upload the website onto the internet.
  - Try to disguise the website to make it look like the legitimate website.
- Phishing Collector:
  - Stores it for the person running the phish to collect later.
  - Retrieves the username, password or any confidential information entered on the site.
  - Redirects the user back to a legitimate page so they don't realize they've been phished.

## Server Hijacking

- Cross-site Scripting and Phishing:
  - Typically:
    - Add a new form to the page that we control and hide everything else.
    - Change the form on the page to point to the phishing collector or
  - We can use HTML code to change what the browser displays, even after the page has loaded.
  - This JavaScript code gets all forms on the page and redirects all their actions to the phishing collector.

![Server Hijacking](https://remnote-user-data.s3.amazonaws.com/npzyHLk4JNMWy-pqNzygiK7a1FKrR5aMNnMERVD0306vm3mXck6dNkN10cwu1srpQnM1pmJ3zziq_-AySyVhH5v9jkFsnKqt98VQMv6t42dz4kO_mIYHcf3Mdk_Pruql.png)

- Typically involves changing the forms on a website to point to the phishing collector instead of where they should.
  - Techniques:
    - Create code to modify the website to point to the phishing collector.
    - Find an exploit somewhere on the website.
    - Create and send out an email pointing to the exploited legitimate website.
    - Set up a phishing collector.
  - Three major forms of server hijacking:
    - Direct compromise: Gaining access to the server and being able to rewrite files and manipulate them directly.
    - Cross-site scripting: Allows us to "reprogram" the website by injecting additional code.
    - Open redirects: Being able to "bounce" through a legitimate website to the phishing website, so it looks legitimate.
  - Exploiting a legitimate website to turn it into a phish.

## Information Exposure

- When sensitive information is accidentally exposed by an application:
  - May be application data: Leaked resources, version information, configuration details.
  - May be user data: User information.
  - May be deployment information: URLs or structure.
- As a black box tester, you need to scrutinize all outputs from the application for any information you can use:
  - Headers.
  - Testing files.
  - HTML source code.
  - Other directories.
  - Backup files.

## Authorisation Bypass

- Sometimes it is possible to bypass the authorization checks:
  - Missing authorization throughout the process: Some applications check authorization at the start of the process but not all the way through - sometimes you can jump in by bypassing the initial check.
  - "Safe" areas: Some applications have safe areas where it is presumed everything inside has already passed authorization checks, but this isn't always the case.
  - Authorization by omission: Some applications hide administrative controls from non-administrative users but do not enforce the check.
- Techniques:
  - Can guess a URL to gain access to something you shouldn't.
  - Use the URLs you've seen so far to guess.
- When authorization is not implemented properly.

## Insecure Cookies

- Cookies are used by applications to store client-side information:
  - Typically a session or user key.
  - Required so the application continues to know who you are after you've logged in.
  - When you log in, you typically get set a cookie containing some form of key which identifies you.
- Cookies are sent in the headers with every request you make.
- Cookies can be insecure:
  - If someone can forge or steal a cookie, they can become another user without ever needing their password.
- Techniques:
  - How do they change with different user accounts?
  - Can you manipulate or change them?
  - What values do they have?
  - What cookies are being set?
- Cookies ⇒ View Cookie Information (Web Developer Toolbar).
- Application ⇒ Cookies in the DevTools.
