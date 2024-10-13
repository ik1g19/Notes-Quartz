# Cookies and Sessions

## Cookies

- Used for 'remembering' you back to the site later
- For stuff that does matter
  - Store it properly
    - Generate a token, that corresponds to something inside your database, so that you can lookup the token and find the user in a way that is unguessable and unpredictable
- But must not be possible to construct a cookie to log in to an account you shouldn't
- Need to be enough to log you in without your username and password
- More persistent than sessions
- For stuff that doesn't matter
  - Store in the cookie directly
    - E.g.
      - What theme are you currently using
      - How are you sorting your table

## Sessions

- The session ID is all that protects your server side data and your identity to the website
- Make sure it cannot be guess, predicted or manipulated
- You have a session ID on the client, which links you to the data store on the site, on the server
- Have a limited life
- Make sure your session is handled correctly
