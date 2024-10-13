# Tools and Techniques

## The Process of Penetration Testing

1. Scoping
   - Agree on what is being tested
   - Define boundaries
2. Gather information
3. Identify vulnerabilities
4. Exploit
5. Post-Exploit
6. Report

## Burp Suite

- Burp Suite is an intercepting proxy.
- As you browse, everything passes through it. It:
  - Collects information
  - Allows you to track what you have done
  - Allows you to review previous requests and responses
  - Allows you to manipulate everything

![Burp Suite Image](https://remnote-user-data.s3.amazonaws.com/0jUBwszGgDyBaXmAEuT2x6myuX7PfAUQuYtc87ZRns79u6avCpne6aM9Spxd9nhEdip6BLbxTO6wcqP82tCHr3WAqBzxKYYGd40bDHdqZEJQLiQQBAWNht-vao1c6asV.png)

- Set up:
  - Set up Burp Suite as the proxy
  - Install the certificate
- Sending a page to intruder allows you to run attacks:
  - Insert \$\$ around fields you want to run the attack on
  - Fuzzing - Long lists of inputs which are known to lead to potential vulnerabilities
- SQLMap:
  - Provides access to the whole database once an injection hole has been found
