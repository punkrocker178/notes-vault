# JWT (JSON Web Token)
Is a compact, self-contained JSON object to securely transmit information between parties.  
This information can be **verified** and **trusted** because it is digitally signed. JWTs can also be signed using a secret (with **HMAC** algorithm) or a public/private key pair using **RSA** or **ECDSA**.
[See more](https://www.jwt.io/introduction)

## Use cases
- **Authorization**: This is the most common scenario for using JWT. Once the user is logged in, each subsequent request will include the JWT, allowing the user to access resources that are permitted with that token. **SSO** is a feature that widely uses JWT nowadays because of its small overhead and its ability to be easily used across different domains.
- **Information Exchange**: JSON Web Tokens are a good way of securely transmitting information between parties. Because JWTs can be signed—for example, using public/private key pairs—you can be sure the senders are who they say they are.  

# Oauth (Open Authentication)
Is a standard designed to allow a website or application to access resources hosted by other web apps on behalf of a user.  
OAuth 2.0 provides **consented access** and restricts actions of what the client app can perform on resources on behalf of the user, **without ever sharing the user's credentials**.

## How Does OAuth 2.0 Work?
The Client must acquire its own credentials, a **_client id _** and **_client secret_**, from the Authorization Server in order to identify and authenticate itself when requesting an Access Token.

### General flow:
1. The Client requests authorization (authorization request) from the Authorization server, supplying the client id and secret to as identification; it also provides the scopes and an endpoint URI (redirect URI) to send the Access Token or the Authorization Code to.
2. The Authorization server authenticates the Client and verifies that the requested scopes are permitted.
3. The Resource owner interacts with the Authorization server to grant access.
4. The Authorization server redirects back to the Client with either an Authorization Code or Access Token, depending on the grant type. A Refresh Token may also be returned.
5. With the Access Token, the Client requests access to the resource from the Resource server.

### Example flow:
Suppose a web app integrates Reddit authentication to get Reddit data such as Posts and Subreddits. The user from the web app will authenticate to their Reddit account. The Reddit Oauth integration of the web app will authenticate and authorize to Reddit on the user behalf.

**Prerequisite:**
The web app has registered its information on Reddit to acquire `client_id` and `client_secret`

**Flow:**
1. The web app requests authorization from Reddit server and supplying `client_id`, `client_secret`, the scopes of this authorization and `redirectURI`.
2. The user (Resource owner) now authenticates with Reddit.
3. After successful authentication, the user (Resource owner) interacts with Reddit to grant access to the provided scope (Reddit will consent with the user that the web app are going to have the specified permissions to access Reddit resources).
4. After user granting access, Reddit will redirect back to the Client (web app) with the authorization `code`. Depending on the `grant` type, `access_token` and `refresh_token` can also be returned.
5. With the `code` provided, the Client (web app) can perform api call to retreive `acess_token`
6. With the `access_token`, the Client can access to Reddit's resources.

## Grant type
In OAuth 2.0, **grants** are the set of steps a Client has to perform to get resource access authorization. The authorization framework provides several grant types to address different scenarios:

- [Authorization Code](https://auth0.com/docs/api-auth/tutorials/authorization-code-grant) grant: The Authorization server returns a single-use Authorization Code to the Client, which is then exchanged for an Access Token. This is the best option for traditional web apps where the exchange can securely happen on the server side. The Authorization Code flow might be used by Single Page Apps (SPA) and mobile/native apps. 
- [Implicit](https://auth0.com/docs/api-auth/tutorials/implicit-grant) Grant: A simplified flow where the Access Token is returned directly to the Client. In the Implicit flow, the authorization server may return the Access Token as a parameter in the callback URI or as a response to a form post. The first option is now deprecated due to potential token leakage.
- [Authorization Code Grant with Proof Key for Code Exchange (PKCE)](https://auth0.com/docs/flows/concepts/auth-code-pkce): This authorization flow is similar to the _Authorization Code_ grant, but with additional steps that make it more secure for mobile/native apps and SPAs.
- [Resource Owner Credentials Grant Type](https://auth0.com/docs/api-auth/tutorials/password-grant): This grant requires the Client first to acquire the resource owner’s credentials, which are passed to the Authorization server. It is, therefore, limited to Clients that are completely trusted. It has the advantage that no redirect to the Authorization server is involved, so it is applicable in the use cases where a redirect is infeasible.
- [Client Credentials Grant Type](https://auth0.com/docs/api-auth/tutorials/client-credentials): Used for non-interactive applications e.g., automated processes, microservices, etc. In this case, the application is authenticated per se by using its client id and secret.
- [Device Authorization Flow](https://auth0.com/docs/flows/concepts/device-auth): A grant that enables use by apps on input-constrained devices, such as smart TVs.
- [Refresh Token Grant](https://auth0.com/blog/refresh-tokens-what-are-they-and-when-to-use-them/): The flow that involves the exchange of a Refresh Token for a new Access Token.