# Yet More Vulnerabilities
## The Basics of Mapping

When you have an application to test, you need to understand it
- Where does it take user input
- What features are present
- What pages does it have
- What forms does it have
 
## Different Forms of Input

- URL Parameter - User-filled parameter that is part of the URL itself but not a GET parameter
	- e.g. /groups/studentscoutsandguides/
- GET Parameter - After the ? in the URL, a key - value pair
	- e.g. /search?q=Scouts
- POST Data - Form fields which are submitted with name - value pairs

## Manipulating EXIF

exiftool allows you to manipulate EXIF data in images
- Allows us to embed code in an image while leaving it a valid image
 
## Cross-Site Request Forgery

Tricking your browser into doing something you didn't intend to do

Your browser sends your session whenever it makes a request to that website
- Even if the request comes from another website

What you're looking for
- The absence of CSRF tokens in forms
- Insecure GET actions
- GET-based actions
- Unprotected forms

### Same Site Cookie Policy

Allows you to decide when setting a cookie whether it should be sent when the request originates from another site

But not entirely
- The Lax default still allows GET requests from following a link

Means CSRF is not a prominent threat

The new standard is that the default is restricted

Made the majority of CSRF disappear 

## Server-Side Request Forgery

The server may be on the inside of the network

The server can access internal resources

Getting the server to make a request
- Or something that connects to another site
- For example, via an API call
 
## Internal Information Exposure

Error reporting, debug information, unexpected behaviours

How does the application and framework handle error reporting?

How does the application handle unexpected errors and faults?

You are trying to create those faults, situations and errors
 
## Information leakage

Doing something unexpected can lead to details about the server or database

The attacker needs information
- The more information, the easier the attack

NVD contains all the vulnerabilities for all the different software versions
 
## Finding Leftover Files

Look for variations

Look for common files with common names
- e.g. testing, phpinfo, info, debug
 
## Parameter Manipulation

What inputs are you able to find

What types are you able to find

What happens when you give invalid types

What happens when you miss out information

What happens when you give invalid information

Client-side validation is insufficient
- A client can send any response it wants to the server, regardless of client-side validation
### Techniques

- Leaving out input all together
- Adding decimals
- Out of range
- Executing commands
- Adding new parameters
- Overflowing the input
- Injection
- Different data types

## Application Logic

Similar to Parameter manipulation

Breaking the application logic

Look for
- Multiple-step processes
- User input processing, not just queried/stored
 
## Out of Date Software

Running old software that has vulnerabilities

Look for
- Out of date components or underlying software
- Out of date software
- Signs of the software being used
- Signs of the version being used
- Vulnerabilities in the version that can be exploited remotely

### National Vulnerability Database

- Database of known vulnerabilities in software
- Searchable
- CVE Numbers - Unique identifiers for vulnerabilities
 
## File Inclusion
### Good file to aim for

passwd contains local usernames

On Linux systems calling ../ at the root directory does nothing so you can add as many as you want

Are there any places where a file is dynamically included by the URL

Looking for
- Places where files from the file system are included, based on user input

Can you change what is included to something you shouldn't

Look in 'Network' section of developer panel to find included external resources
 
## Open Redirects

Can recognise a redirect by looking for 3xx status codes

Can recognise a redirect with input by looking at the request

Look for redirects in the application which pass the redirect through the URL
 
 