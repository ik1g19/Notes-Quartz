# Insecure Upload

## Look for

- Parts of code that handle uploading

## Think about

- What do you want to allow
- What does the user have control over
- How could the tests be bypassed
- How to reject what you don't allow

## How to fix

- Perform tests on every uploaded file to ensure they are exactly what you want

Uploads in PHP involved the move_uploaded_file function

Find instances of use

![|400](https://remnote-user-data.s3.amazonaws.com/snIydDBQB5i47OIVMyME-VOHtroDaCcV9bZdDvejwBCaPGaJtie0ESWDAJGp9-BF96Un0xpEGIqXjaEJKR750a2wkxIpQRbvCV4jOvCEsSrbqNMnBt_nMA8fcKAYN-Bw.png)

Add functions to test for files being valid

- Check extension
  - Use pathinfo
- Use .htaccess to restrict what happens to uploads
- Check file type
- Check MIME
  - Its in the array
- Use a whitelist
- Add function to handle saving correctly
  - Generating a new name for the file
