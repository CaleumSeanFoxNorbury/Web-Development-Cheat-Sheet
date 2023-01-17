# Implementation of Apple Sign In

Full-stack implementation of apple pay. 

## Project API Schema

**Auth with Apple**

`POST`

**Example:** `/api/oauth/apple`

```
{
    "userid": "asdsfdgdsgf",
    "email": "test@test.com",
    "forename": "firstname",   
    "surname": "secondname",
    "token": "ldkjfgjkdfsgjldfglk"
}
```

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

This btn will send all authorization information to apple and apple will return HTTP POST request back will all processes info and the auth results. This information will be sent to the URL provided within redirectURI which should be a local endpoint ready to process the results our side.

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

### Authorization endpoint

When a request has been made from the client-side, the frontend will catch success or fail apple auth requests and send the containing auth request results to be processed within a desired endpoint. This includes:

```
    code
    id_token
    state
    user
```

### Validate the authorization code 

A `POST` request should be made to apples following endpoint for validating the `code` gathered from the frontend:

```
https://appleid.apple.com/auth/token
```

**Params:**

```
{
  client_id
  client_secret
  code
  grant_type
  redirect_uri 
}
```

### Validate an existing refresh token

When validating an existing refresh token, include the following params within the `POST` request:

`"https://appleid.apple.com/auth/token"`

```
{
  client_id
  client_secret  
  grant_type
  redirect_uri 
}
```

## Referances 

Apple Sign-in (Client-Side) [2022] - https://developer.apple.com/documentation/sign_in_with_apple/sign_in_with_apple_js/configuring_your_webpage_for_sign_in_with_apple

Apple Sign-in (Server-Side) [2022] - https://developer.apple.com/documentation/sign_in_with_apple/generate_and_validate_tokens
