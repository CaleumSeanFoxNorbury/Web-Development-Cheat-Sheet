# Google sign-in

## Init 

```
<script src="https://accounts.google.com/gsi/client" onload="googleSignedIn()" async defer></script>
```

### Command for backend (CLI installation)

```
composer require google/apiclient
```

## Implmentation 

### catching intialisation of google sign-in

```
      let googleAuth;
      let hasGoogleInit;
      let googleSignInLoaded;

			let googleSignedIn = function(){
				googleSignInLoaded = true;
				hasGoogleInit = false;

				googleAuth = google.accounts;
			}
```

### Gathering JWT from frontend (signing in with google and btn implementation)

```
 try {
                    // initalize the google sign in button
                    // rendering googles style
                    if (googleSignInLoaded) {
                        if (!hasGoogleInit) {
                            googleAuth.id.initialize({
                                // This needs to be hidden
                                client_id: "'.OAUTH_GOOGLE_CLIENT_ID.'",
                                callback: async (googleRes) => {
                                    // set web token for revoking privs
                                    googlesJWT = googleRes.credential;

                                    const responsePayload = parseJWT(googleRes.credential);

                                    $.ajax({
                                        type: "POST",
                                        url: "'.AJAX_URL.'auth/ajax-google-auth.php",
                                        data: {
                                            "action" : "authenticationWithGoogle",
                                            "token": googleRes.credential,
                                            "userID": responsePayload.sub,
											"email": responsePayload.email
                                        },
                                        success: function(data){
											data = JSON.parse(data);

											// revoke google priv so that they have to sign-in again
											revokeGoogleAuth(parseJWT(googlesJWT)["sub"]);

											if(data.status == "success"){
												$.smallBox({title:"Success:",content: data.message,color:"#739E73",timeout:8000,iconSmall:"fal fa-check shake animated"});
												if(data.redirectURI){
													window.location = data.redirectURI;
												}
											} else if(data.status == "info"){
												if(redirectURI){
													$.smallBox({title:"Info:",content: data.message ,color:"#3276B1",timeout:8000,iconSmall:"fal fa-info shake animated"});
													if(data.redirectURI){
														window.location = data.redirectURI;
													}
												}
											} else if(data.status == "danger"){
												$.smallBox({title:"Error:",content: data.message, color:"#C46A69",timeout:8000,iconSmall:"fal fa-check shake animated"});
											}
                                        }
                                    });
                                }
                            });

                            window.hasGoogleInit = true;
                        }

                        googleAuth.id.renderButton(
                            document.getElementById("googleSignIn"), {
                                scope: "profile",
                                shape: "rectangular",
                                size: "large",
                                text: "signin",
                                theme: "light"
                            }
                        );
                    }
                } catch (e) {
                    console.log("Error: GOOGLE_SIGN_IN");
                }
```

### Revoking sign in

```
			function revokeGoogleAuth(hint){
				try{
					googleAuth.id.revoke(hint, (done) => {
						if (done.successful) {
							console.log("Google authentication has been revoked.");
						} else {
							console.log("Google revoke authentication failed. Please try again.");
						}
					});
				} catch (e) {
					console.log("Google revoke authentication failed. Please try again.");
				}
			}
```

### Parsing any JWT

```
            // todo :: this can be made generic
            function parseJWT(token) {
                var base64Url = token.split(".")[1];
                var base64 = base64Url.replace(/-/g, "+").replace(/_/g, "/");
                var jsonPayload = decodeURIComponent(
                    window.atob(base64)
                        .split("")
                        .map(function(c) {
                          return "%" + ("00" + c.charCodeAt(0).toString(16)).slice(-2);
                        })
                        .join(""));

                return JSON.parse(jsonPayload);
            };
```

### Validating JWT from backend 

```
 $client = new Google_Client(['client_id' => OAUTH_GOOGLE_CLIENT_ID]);
            $payload = $client->verifyIdToken($_POST['token']);

			// if we get a payload, then we have successfully authed with google
            if ($payload) {
                $userid = $payload['sub'];
```
