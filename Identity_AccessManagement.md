# Identity and Access Management

## The building blocks of a secure system

### HTTP Status Codes    

Two status codes which are important throughout this course are:
* 401 Unauthorized    

The client must pass authentication before access to this resource is granted.
The server cannot validate the identity of the requested party.

* 403 Forbidden    

The client does not have permission to access the resource.
Unlike 401, the server knows who is making the request, but that requesting party has no authorization to access the resource.
flask run —reload

### Identity and Authentication

Authentication in the Digital World
Let's look at a brief overview of the concepts we'll be covering.
If you don't understand all of the details given in this video at this stage, don't worry—we're going to go over all of this in much greater detail throughout the lesson!


`token = temporary credential`

As we discussed in the video, some issues with passwords are outside of our control as developers. Many issues come from user behavior that we cannot directly influence, such as:
* Users forget their passwords
* Users use simple passwords
* Users use common passwords
* Users repeat passwords
* Users share passwords

In contrast, some issues are within our control as developers:
* Passwords can be compromised
* Developers can incorrectly check
* Developers can cut corners


#### Alternative Authentication Methods

1. Single Sign-On (SSO)

2. Multi-Factor Authentication

![MultiFactorAuthentication](https://github.com/bearcub3/coffeeshop-fullstack/blob/master/multi-factor-authentication.png)

An alternative to generating the code on our server and having it sent to our user would be to generate the code on the device itself. This is often done with something called a **decaying temporal algorithm**. 
This is a code that uses some kind of cryptography to generate a random number that corresponds to a specific time. Only the device and the service knows that code at any given instance in time. ex) RSA SecureID, Titan security key

3. Passwordless


4. Biometric Authentication

[Oath2](https://oauth.net/2/)
[Autho0 Identity Providers](https://auth0.com/docs/identityproviders)
[Google Identity Platform](https://developers.google.com/identity/)
[Magic Links](https://hackernoon.com/magic-links-d680d410f8f7)
[iOS Biometrics](https://developer.apple.com/documentation/localauthentication)
[Google Authenticator](https://play.google.com/store/apps/details?id=com.google.android.apps.authenticator2&hl=en_US)


#### Third-Party Auth Systems

Why Delegate the Responsibility?

**Technical debt**    
something we cannot change quickly and effectively, it may lead to vulnerability and mistakes and the two areas that need tremendous amounts of work defects.

[Auth0 Authorize Link (Implementing Auth0)](https://auth0.com/docs/api/authentication#authorize-application)

The complete documentation for the authorization code flow can be found in Auth0's Documentation.
It may help to fill in the url in the textbox below before copying it into your browser:

```
https://{{YOUR_DOMAIN}}/authorize?audience={{API_IDENTIFIER}}&response_type=token&client_id={{YOUR_CLIENT_ID}}&redirect_uri={{YOUR_CALLBACK_URI}}
```


Integrating Auth0 With Your Frontend
To integrate Auth0 with your frontend you simply need to redirect your user to your Auth0 hosted login page and include a url to redirect them to upon completion. This can be done using a simple html anchor link:

<a href="{{AUTH0_AUTHORIZE_URL}}">Login</a>

For a more seamless user experience, you can (and should) set up a custom domain on Auth0 by following the instructions in their docs.
This is also a good idea to minimize the risk of Phishing Attacks by ensuring that your users do not accidentally enter their credentials into a login form that just looks like yours.


### JSON Web Tokens (JWTs)

- the benefits of JWTs

  1. stateless
  2. difficult to fake
  3. popular and easily implemented across platforms
  4. flexible

Parts of a JSON Web Token

`header.payload.signature`

* JWT - Datastructure

Payload is responsible for containing information specific to the currently authenticated user.

* JWT - Validation

https://jwt.io/introduction/

https://en.wikipedia.org/wiki/HMAC
HMAC keyed-hash message authentication code

https://en.wikipedia.org/wiki/Base64



### Storing Tokens in Web Browsers

- Using Local Storage
Local Storage is an implementation of a key-value store which is accessible through a javascript interface in most modern browsers. It is a general purpose interface to store strings which will persist in memory from session to session. It is designed for smaller strings and alternative opensource systems like localForage exist for large amounts of data.

key-value store is a data storage paradigm 


- Storing JWTs

Using Javascript to Store JWTs
Security Considerations of Local Storage
How Cross-Site Scripting Attacks (XSS) are Performed and Mitigated Techniques

We discuss Input Sanitation.
To clarify this concept, imagine a user submits HTML as part of their name in a form.
When you later pull this information from your database and insert it into the HTML template for the website, the browser engine will render this text on the page.
However, if the text contains HTML like <b>Gabe</b> this would be interpreted in the browser as HTML and render as Gabe.
This becomes a problem if malicious code, such as javascript, is saved in place of a valid string.
In other words, this malicious text will be interpreted by the browser as code and executed on the client.
Input Sanitation transforms characters like < to &lt; which will not be interpreted as code and print as text (<).
This step should always be performed on the server to prevent someone from sending the malicious text directly to your server using curl or Postman.

https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.md


- Alternatives to LocalStorage
* localForage javascript library capable of more complex storage tasks.
* HttpOnly Cookies so javascript can't access the token at all.

- Sending Tokens with Requests

Accessing Authorization Headers in Flask

use the authorisation headers to send JWT from client to server
￼

the authenticated headers include prepended keyword “Bearer”

Within Flask, the headers parameter is just a dictionary object containing all of the headers.

```
requestion.headers[‘Authorization’]
header_parts = auth_header.split(‘ ‘)[1]
```

Validating Auth Header Formats and Defining our Decorator

Sending Tokens from Popular Frontend Frameworks
* React + Redux - JWT Tutorial There are many ways to include JWTs in requests from frontend frameworks. Jason Watmore has many tutorials for your frontend flavor of choice.
* Angular Interceptors for Authorization Headers


Authentication Tokens(specifically JWTs) are used to 
1. carry claims in the forms of a verifiable payload
2. perform authentication on requests after login
