# Continued Vulnerabilities

## Insecure Upload

- Techniques:
  - Filename: Does it change the file name you give it?
  - MIME types: The browser sends this.
  - File extensions: Can you confuse it?
    - Double extensions
    - Zip files
  - Content - a valid image:
    - Embedding what you want in it, e.g. EXIF headers.
    - If you upload a php file as a jpg, it won't get sent to the PHP processor to execute unless you have the ability to run things on the server in another way.

- Insecure upload functionality
- File Upload Vulnerabilities:
  - Server commonly checks the MIME type of the file. The browser is not trusted. The MIME type is sent by the browser.
  - Look for upload forms, send unexpected content.
  - Users could upload arbitrary content to your website. They could execute code on your server. They could set up their own phishing site on your domain.
