Delegated Authorization/access of a personal data --->>> by the Resource owner is done by Oauth. 

Resource owner giving access to the resource to the client app using token is called OAUTH.

Oauth grant flow ------------->>>>
steps taken for the access 

OKTA is the Oauth server who generates the token using RS256 algorithm . 

------------------------------------------------------------------------


Endpoint to JWKS for the Authorization server :
https://dev-64652784.okta.com/oauth2/ausnnzofxjeksvmkO5d7/v1/keys


this is the JWKS assigned to Authorization server by okta:

{
  "keys": [
    {
      "kty": "RSA",
      "alg": "RS256",
      "kid": "Ad3yA2Gj74513auUQqk7aX3cn-1aBmAE0rsCNchOo4Q",
      "use": "sig",
      "e": "AQAB",
      "n": "zxCRk4XziJh_BVrEfx1T4p17MY2BaY8CxtE5qqaNB_9s4M3jXc1EKCqOmlsYd7M5zq9B5tRx0p1T-pS4w7dX7qd252DvGmFS5YtEJdZEuuxFnO5zhrSS1t44RRBSZluB9CR8QGPeNWkM-KGkRagw3Xok8-z8DEM30aR_H1nF_b_-QrNt7vOuuMfNbUZ-E8LqY0lDNqWYReAnqfkcVKmoD6WnYu8MlpJfhxRx_M7R6n4dEV5ed0kKtY7ip28bAyhtbGNGg9GOsGVTeBm5acSOlYElkGU7KytAaBrpls1VdlxPS7sY__jh64fJvSuHdslnX9elKIycNwm1va1a8cDZKQ"
    }
  ]
}

Multiple Authorization Servers → Multiple Keys
	•	If you create multiple Authorization Servers 
	(e.g., one for internal APIs and another for external clients), each will have its own public-private key pair.


Now, let’s use this analogy for a JWT verification process:

1️⃣ Extract the “kid” (Key ID) from the JWT header
	•	The JWT contains a header, payload, and signature.
	•	The header has a "kid" field, which tells us which public key to use.

2️⃣ Fetch the Public Key Set (JWKS JSON) from Okta
	•	Okta provides a public endpoint (/keys) that lists all valid keys.
	•	This is like a database of official public keys that Okta publishes.

3️⃣ Find the Public Key that Matches the “kid”
	•	Your app checks the "kid" from the JWT against the list of keys from Okta.
	•	If it finds a match, it extracts the correct public key.

4️⃣ Use the Public Key to Verify the JWT Signature
	•	Using the public key, your app verifies the JWT hasn’t been tampered with.
	•	If the signature is valid, the JWT is trusted and can be used.
	•	If the signature is invalid, the JWT is rejected as forged or expired.



