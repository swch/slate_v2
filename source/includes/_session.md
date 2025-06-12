# Passwords and Authorization

## Authorize cardholder

> Credential grants are very important for handing off responbility to a downstream client.  The grants must be provisioned by a user that can create grants (like a customer_agent), and the grant is one-time-use for 3 minutes.  Grants are created when cardholders are created, and can be used as part of the authorize endpoint within the client by an agent (generally a cardholder_agent).

```javascript
const { CardsavrSession } = require() "@strivve/strivve-sdk/lib/cardsavr/CardsavrJSLibrary-2.0";

//agent_session is the session of a cardholder agent.  Cardholder agents are lower 
//privileged agents that can authorize themselves using grants created upstream when cardholder are created.
const login = await agent_session.authorizeCardholder(grant);
const response = agent_session.createSingleSiteJob(job); //agent can now act on behalf of cardholder
```

```csharp
using Switch.CardSavr.Http;

CardSavrResponse<UserLogin> login = await agentSession.client.authorizeCardholder(grant);
//user can now act on behalf of cardholder
```

```java
import com.strivve.CardsavrSession

JsonObject login = agentSession.put("/cardholder/authorize", Json.createObjectBuilder().add("grant", grant).build(), null, null); 
//user can now act on behalf of cardholder
```

```shell
#session must first be started, and must have permissions to create grants
curl -iv 
  -H "Content-Type: application/json" "https://api.INSTANCE.cardsavr.io/cardholder/{{GRANT}}/authorize" 
  -H "x-cardsavr-trace: {\"key\": \"my_trace\"}" -H "x-cardsavr-session-jwt: {{JWT_TOKEN}}"
```

> Grants are always 38 characters, are one time use, and expire after 3 minutes.

```json
{
    "user_credential_grant": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9ey"
}
```

### Path
GET /cardsavr_users/:id/credential_grant

### Description
Returns a credential grant for specified user. This grant can be included with an authorize endpoint call ONCE within three minutes of being created.  Grants can also be hydrated into a cardholder response.  Frequently grants are issued immediately following the creation of a cardholder, so this is a common workflow.

## Update user password

> Password updates for non-agents must supply the old_password

```javascript
const { CardsavrSession } = require() "@strivve/strivve-sdk/lib/cardsavr/CardsavrJSLibrary-2.0";

await session.updatePassword(user_id, { password : new_password, password_copy : new_password});
```

```csharp
using Switch.CardSavr.Http;

PropertyBag bag = new PropertyBag();
bag["old_password"] = old_password;
bag["password"] = new_password;
bag["password_copy"] = new_password;

CardSavrResponse<PropertyBag> result = await http.UpdateUserPasswordAsync(user_id, bag);
```

```java
JsonObject body = Json.createObjectBuilder()
  .add("old_password", old_password)
  .add("password", password)
  .add("password_copy", password_copy)
  .build();

String url = String.format("/users/%d/update_password", userId);
JsonObject response = (JsonObject) session.put(url, body, null, null);
```

```shell
#old_pass is not required for privileged admins.  Users must provide their old password
curl -iv  -d "{\"password\": \"3ysXPhntmPDU7xUFYKbc/4Aq=WVrhExdjHQsx5FgV2pZ\", 
  \"password_copy\": \"3ysXPhntmPDU7xUFYKbc/4Aq=WVrhExdjHQsx5FgV2pZ\"}" 
  -H "Content-Type: application/json" "https://api.INSTANCE.cardsavr.io/cardsavr_users/:id/credential_grant" 
  -H "x-cardsavr-trace: {\"key\": \"my_trace\"}"  -H "x-cardsavr-session-jwt: {{JWT_TOKEN}}"
```

```json
{
    "success": true
}
```

### Path
PUT /cardsavr_users/:id/update_password

### Description
Updates CardSavr user password key. Partners are responsible for rotating their agent role password keys every 90 days. Cardholder roles cannot have passwords and must log in using credential grants.

<aside class="notice">
Most password updates can be done via the [Partner Portal](https://developers.strivve.com/resources/partner-portal/), however customer_agent and cardholder_agent password are the responsibility of the partner to rotate.
</aside>

### Body parameters

Parameter | Type | Required | Desription
--------- | ---- | -------- | ----------
password | string | yes | New password key
password_copy | string | yes | Copy of new password key
old_password | string | not always | Privileged accounts can reset users' passwords without the old key

# Session

Session endpoints are used for session login, and termination.

## User login

> To create a new session and authorize a login call is required:

```javascript
const { CardsavrSession } = require() "@strivve/strivve-sdk/lib/cardsavr/CardsavrJSLibrary-2.0";

const session = new CardsavrSession(cardsavr_server, 
    app_key, app_name, username, password);
const login_data = await session.init();
```

```csharp
using Switch.CardSavr.Http;

CardSavrHttpClient session = new CardSavrHttpClient(_cardsavrServer, 
  _appKey, _appName, userName, password);
CardSavrResponse<LoginResult> login = await session.Init();
```

```java
import com.strivve.CardsavrSession;

this.session = CardsavrSession.createSession(integratorName, integratorKey, apiServer);
JsonObject obj = (JsonObject) session.login(username, password, null);
//throws CardsavrRESTException
```

```shell
curl -iv -d "{\"password\": \"PASSWORD\", \"userName\": \"USERNAME\"}" 
  -H "Content-Type: application/json" "https://api.INSTANCE.cardsavr.io/session/login" 
  -H "x-cardsavr-trace: {\"key\": \"my_trace\"}"  -H "x-cardsavr-session-jwt: {{JWT_TOKEN}}"
```

> The login call both starts and authorizes a new session and returns the user, along with a public key to be used in generating a new API  Session Key to sign and encrypt future requests on the session. See [API Session Keys](https://developers.strivve.com/resources/cryptography/) for information on using Server's public key. Return a session token to be used with all subsequent calls on the session.  This value is sent with the "x-cardsavr-session-jwt" header. If you are debugging with cURL or Postman, cookies are used in lieu of session tokens.

```json
{
  "server_public_key": "sample_public_key",
  "session_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiI4ZjJkYjQ1OS1kODMzLTQ2NmItOGE0MS1mYzcwMzA1M2QwZGIiLCJpc3MiOiJhcGkuZ3RvbWxpbnNvbi5jYXJkc2F2ci5pbyIsImF1ZCI6ImFwaS5ndG9tbGluc29uLmNhcmRzYXZyLmlvIiwiaWF0IjoxNTk5NzY5NDQ2fQ.slI13GGNot8SU_hPdzXzZrjcv90G43etofgh9HotNj0",
  "user_id": 123,
  "user": 
  {
    "id": 123,
    "username": "john_smith_123",
    "first_name": "John",
    "last_name": "Smith",
    "email": "jsmith@email.com",
    "is_locked": true,
    "role": "dev",
    "created_on": "2018-04-19T23:10:36.657Z",
    "last_updated_on": null,
    "financial_institution": {
      "id": 1,
      "name": "Acme Credit Union",
      "description": "Users in this FI can view and perform actions on users in all other FIs.",
      "lookup_key": "acmecu",
      "alternate_lookup_key": null,
      "config": null,
      "last_activity": null,
      "created_on": "2023-09-07T18:49:54.859Z",
      "last_updated_on": null
    }
  }
}
```

### Path
POST /session/login

### Description

Login user into a CardSavr session

### Body parameters

Parameter | Type | Required | Desription
-------- | ---- | --------- | ----------
client_public_key | string | yes | The base 64 encoded NIST point 256 (P256) elliptic curve public key  from the key pair generated by the calling application. See [Curve Private Key](https://developers.strivve.com/resources/cryptography/)
username | string | yes | user name for this user
password_proof | string | no | The base 64 encoded HMAC-256 signature zero-knowledge-proof of the password. See [zero-knowedge-proof] for more information. This parameter is mutually exclusive of the 'password' and 'userCredentialGrant' parameters.
password | string | no | User's plain text password when using Postman or Curl on a development environment. This parameter is mutually exclusive of the 'passwordProof' and 'userCredentialGrant' parameters.

</a=zero-knowledge-proof></a>
### Zero Knowledge Proof Password 

The CardSavr service uses a zero-knowledge-proof mechanism with passwords during login.  The proof is done by producing a key derivation from the username/password and producing a HMAC-256 signature that can be verified by the CardSavr server.  This is done to prevent the server from ever knowing the password. See [zero knowledge proof](https://developers.strivve.com/resources/cryptography/) for more information.

## End session

```javascript
const { CardsavrSession } = require() "@strivve/strivve-sdk/lib/cardsavr/CardsavrJSLibrary-2.0";

await session.end();
//or if using the CardsavrHelper, the cache must be cleaned up
//await helper.endSession(username);
```

```csharp
using Switch.CardSavr.Http;

await client.EndAsync();
//or if using CardSavrHelper, you need to release the session from the cache
//await helper.CloseSession(userName);
```

```java
import com.strivve.CardsavrSession;

JsonObject response = session.end();
```

```shell
#session must first be started
curl -iv -d -H "Content-Type: application/json" "https://api.INSTANCE.cardsavr.io/session/end" 
  -H "x-cardsavr-trace: {\"key\": \"my_trace\"}"  -H "x-cardsavr-session-jwt: {{JWT_TOKEN}}"
```

> Session end returns a 200 with no body

### Path

GET /session/end/

### Description

Ends the current user session.



