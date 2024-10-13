# Authorisation Bypass

## Look for

- Actions that require authorisation

## Think about

- How the authorisation is given
- What authorisation those actions require

## How to fix

- Ensure for every action requiring authorisation, the action fails without authorisation

## Log in as different levels of user

- Try the same actions with different levels of access
- Is it possible to do actions you shouldn't be able to
- Just one function that checks access for a level
