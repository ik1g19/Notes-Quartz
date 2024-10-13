# Cross-Site Request Forgery

## Look for

- Unprotected forms
- Insecure GET actions

## Think about

- Does this need to be CSRF protected
  - Any actions which change state

## How to fix

- Make forms unique so they can't be copied
  - Use a token
- You want global CSRF protection
  - You don't want to have to do it on every form

![|800](https://remnote-user-data.s3.amazonaws.com/RXyqvlXfChselJSpXHwRS-_4WwZ7cCb8BkLVX3jYvSVVqnyOSPnA1hv-l9SWRJHEgX_jxl2HzfmkQWcE-_yPunzdR2kyrC8hyXNgS3i2t1jTOGGlu0aL8Vql4xsdvo0x.png)

- Then add global code to verify the tokens
- `start` is called every time a form is created, is a good place to add a token to a form

## GET

- Look for GET requests that perform an action
- Are there URLs you can go to directly which change state
- GET should never change state
- Can you perform actions where you shouldn't be able to
