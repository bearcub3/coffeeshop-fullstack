# Passwords

## Problems with Plain Text

**User Table Vulnerability: SQL Injection**    


Mitigation of SQL injection
* always validate inputs
* always sanitize inputs
* use object relational maps(ORMs)
* use prepared SQL statements
` SELECT * FROM 'users' WHERE 'username' == %S`


What are some steps we might take to minimize the risk of compromising our user tables?
1. choose complex admin passwords for our database
2. user ORMs
3. user input validation and saitize any user submitted data
4. use prepared or parameterized SQL statements
5. store our backups as securely as our production databases


## Simple Problems with Passwords

- Brute Force Attacks
```
for attempt in random_strings:
  user = { 'username' : 'target', 'password' : attemp }
  r = requests.post('{{host}}/login', data = user)
```

- Mitigation
* prevent or ratelimit multiple incorrect login attempts
* do not allow common passwords
* enforce a reasonable password policy
* log and monitor for the attack


## An Alternative to Rate-Limiting: CAPTCHAs

[reference from google](https://developers.google.com/recaptcha/docs/v3)

Some techniques to reduce **the risk of brute force attack**    

- Require sufficiently long passwords
- Prevent commonly used passwords from being used
- Log invalid login request attempts
- Rate limit the number of incorrect attempts


## Problems - Data Handling and Logging

- Serialization of Models    

Serialization is the process of transforming a data model into a more easily shared format.
For example, this is commonly performed when sending information as a response from a server to the requesting client in the form of a JSON object.

- Logging Best Practices

Information that leaves an audit trail

- Login Attempts (ids)
- Login Sources
- Requested Resources

- Encryption

What is Symmetric Encryption?

- Simple Substitution
- Polyalphabetic Cipher

