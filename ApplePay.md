# Implmentation of Apple Pay

Full-stack implemntation of apple pay. 

## Client Side 

### Embedded script tag

Within the root file of the application or website, include a script tag which will import Apple JS framework into your project and will enable you to use Apples authoriation features.

```
<script type="text/javascript" src="https://appleid.cdn-apple.com/appleauth/static/jsapi/appleid/1/en_US/appleid.auth.js"></script>
```

### Configure Auth object

To configure our auth object, we need to match details from out developer account. This also needs to be placed within the root file of the project and assigned globally if required to be used around the code base.

```
 <script type="text/javascript">
   AppleID.auth.init({
     clientId : '[CLIENT_ID]',
     scope : '[SCOPES]',
     redirectURI : '[REDIRECT_URI]',
     state : '[STATE]',
     nonce : '[NONCE]',
     usePopup : true
   });
 </script>
```

***Important:*** Use space separation when requesting multiple scopes; for example, "scope=name email".

### Sign-In 

Inlcude a sign in button like below:

```
<div id="appleid-signin" data-color="black" data-border="true" data-type="sign in"></div>
```

This btn will send all authorization information to apple and apple will return HTTP POST request back will all processes info and the auth results. This information will be sent to the URL provided within redirectURI which should be a server side endpoint ready to process the results our side.

### Response 

Indluded within the authorization response success:

```
    code
    id_token
    state
    user
```

`code`: a single-use auth code that expires within five minutes. Used to validate the response.

`id_token`: a JSON web token containing user identification information.

`state`: a string passed by the init function, mirroring the state of the auth request.

`user`: a JSON string containing the data requested in the scope property of the framework auth object.

Indluded within the authorization response fail:

```
    error
    state
```

`error`: the returned error code to be matched by apple giving a reason to the failure.

`state`: a string passed by the init function, mirroring the state of the auth request.

### If using the popup option?

After processing the auth request we sent, apple will process and send back `DOM` event containg the results of the auth request.These events can be catpured by the event watchers below:

```
// Listen for authorization success.
document.addEventListener('AppleIDSignInOnSuccess', (event) => {
    // Handle successful response.
    console.log(event.detail.data);
});

// Listen for authorization failures.
document.addEventListener('AppleIDSignInOnFailure', (event) => {
     // Handle error.
     console.log(event.detail.error);
});
```

## Server Side 

```
// todo
```

## Referances 

Apple Pay [2022] - https://developer.apple.com/documentation/sign_in_with_apple/sign_in_with_apple_js/configuring_your_webpage_for_sign_in_with_apple
