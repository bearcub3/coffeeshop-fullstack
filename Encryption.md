# Encryption

## what is symmetric encryption?

**Simple substitution cipher**    
The longer the ciphers are the easier to crack it as we can look at letter frequency and be able to basically figure out our cipher.

**Polyalphabetic cipher**

**Encryption in the Digital World**    

![encryption](https://github.com/bearcub3/coffeeshop-fullstack/blob/master/encryptionInDigital.png)

- 3DES / Data Encryption Standard
- Blowfish
- AES : Advanced Enccryption Standard

- Feistel Block Cipher    

Initial plaintext block will be splitted into two parts; A and B and the A block will pass through a function which uses one of our keys to jumble that text and it is concatenated with the other half of our original plain text which is B.
This process will be repeated as many as we want and then we will have more complicated and difficult ciphertext block to unscramble at the end.
![FBC](https://github.com/bearcub3/coffeeshop-fullstack/blob/master/FBC.png)

## Using encryption for user tables

Having the values of the columns such as, username and plain text password in the table makes our database Vulnertable.

* Bad Actors
* Bad Database Passwords
* Bad Backup Security
* SQL Injection

However, Encryption can minimize risk if data is compromised, that is to have the encrypted password in the table.
In this case, we need a key to decrypt the password on the API server, compare the password ahdn then return response to the client side.

```
f = Fernet(key)
decrypted_pass = f.decrypt(dbuser.password)
postuser.password == decrypted_pass
```


