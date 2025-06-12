---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript
  - csharp
  - java

toc_footers:
  - <a href='#'>Email us for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - session
  - rest
  - messages
  - errors

search: true
---

# Introduction

The CardSavr REST API is a service for managing payment card circulation on merchant websites. It uses REST principles and standard HTTP features, such as HTTP verbs, as well as several layers of security to protect sensitive data.

CardSavr responses and requests support JSON-formatted bodies only.

# Authentication

> To authorize, an init or login call (differs per SDK) is required:

```javascript
const { CardsavrHelper } = require("@strivve/strivve-sdk/lib/cardsavr/CardsavrJSLibrary-2.0");

const session = new CardsavrSession(cardsavr_server, app_key, app_name);
const login_data = await session.init(username, password);
//await session.getCards({}); //session can now be used to make api calls
```

```csharp
using Switch.CardSavr.Http;

CardSavrHttpClient session = new CardSavrHttpClient(_cardsavrServer, 
  _appKey, _appName, userName, password);
CardSavrResponse<LoginResult> login = await session.Init();

//await session.getCardsAsync(); //session can now be used to make api calls
```

```java
import com.strivve.CardsavrSession;

this.session = CardsavrSession.createSession(integratorName, integratorKey, apiServer);
JsonObject obj = (JsonObject) session.login(username, password, null);
```

```shell
# With a shell, you must first establish a session, followed by 
# a login command.  Keep in mind, this ONLY works 
# with a development server that supports unsigned body requests. 
curl "https://api.INSTANCE.cardsavr.io/session/start" 
  -H "x-cardsavr-trace: {\"key\": \"my_trace\"}" 

curl -iv -d "{\"password\": \"PASSWORD\", \"userName\": \"USERNAME\"}" 
  -H "Content-Type: application/json" "https://api.INSTANCE.cardsavr.io/session/login" 
  -H "x-cardsavr-trace: {\"key\": \"my_trace\"}" 
  
```

> The SDK calls hide the implementation of the login.  Login includes an ECDH key exchange, password signing, and the establishment of a session secret key, which will be used for all future encryptions.  It also leverages a session token which enables the client to access their session on the server.

```json
{
  "server_public_key": "sample_public_key",
  "session_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiI4ZjJkYjQ1OS1kODMzLTQ2NmItOGE0MS1mYzcwMzA1M2QwZGIiLCJpc3MiOiJhcGkuZ3RvbWxpbnNvbi5jYXJkc2F2ci5pbyIsImF1ZCI6ImFwaS5ndG9tbGluc29uLmNhcmRzYXZyLmlvIiwiaWF0IjoxNTk5NzY5NDQ2fQ.slI13GGNot8SU_hPdzXzZrjcv90G43etofgh9HotNj0",
  "user_id": 321,
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
    "last_updated_on": null
  }
}
```

There is more information in the [session endpoint](#session) documentation. If you decide not to use one of the Strivve SDKs, you are responsible for encryption of all bodies passed into the REST API.  

<aside class="notice">
The cardsavr server, app key, app name, and the application username/password must be attained from developers@strivve.com.  See the definitions of these settings [link to app key definitions] here.
</aside>

# Headers

There is a set of required and optional headers.  The SDKs abstract most of these settings, but it's important to understand how they are used when making REST calls. 

REST calls support and/or require the following headers once the session is established.  

Header | Default | Type | Description
------ | ------- | ---- | -----------
x-cardsavr-trace | required | stringified JSON object | [See trace](#trace)
x-cardsavr-client-application | integrator name | string | unique per application, integrator name provided as default when using an SDK
x-cardsavr-authorization | required | string | contains the [integrator name and a prefix](https://developers.strivve.com/resources/encryption), populated by SDK libraries.
x-cardsavr-nonce | required | string (milliseconds) | contains the current UTC time in milliseconds, and therefore provides protection against [replay attacks](https://developers.strivve.com/resources/encryption).
x-cardsavr-signature | required | string | The [string-to-sign format](https://developers.strivve.com/resources/encryption) requires the URL-Path (decoded), the authorization header, and the nonce header.  Also part of the [SDK Libraries](https://developers.strivve.com/api-sdk/).
x-cardsavr-hydration | (none) | stringified JSON object | [See hydration](#hydration) 
x-cardsavr-paging | {"page": 1, "page_length": 25, "is_descending" : true} | stringified JSON object | Only supported with GET calls. [See paging](#paging)
x-cardsavr-session-jwt | required | string | [See session tokens] (#session-tokens)

## session-tokens

CardSavr needs to maintain an API session for state management including authentication, session key, replay prevention, etc.  Standard RFC-7519 JWT tokens are used for client sessions. The x-cardsavr-session-jwt header is used with token based sessions. The x-cardsavr-session-jwt header is managed transparently within the Strivve SDK.  It is the responsibility of applications directly using the direct REST protocol to set this header for each request.

With POST /session/login to begin a new session, this header is not required and will be ignored.

With all subsequent requests on a session

  `"x-cardsavr-session-jwt": value-returned-from-session-login`

## Trace 

> Setting a sample trace header

```javascript
//initialize as part of the session initialization; if not set 
//explicitly, the trace header defaults to the unique username of  //the client user.  If an agent user is operating on behalf of a 
//cardholder, the cardholder cid is the default.  The example      //specifies how to change it.

await session.init(username, password, JSON.stringify({key: "NlOFNNlKabi7Fn26CLw="}));

session.setTrace("NlOFNNlKabi7Fn26CLw=");

//or per request
await session.getUsers({}, {}, {"x-cardsavr-trace": JSON.stringify({key: "NlOFNNlKabi7Fn26CLw="})}); 
```

```csharp
//Add a trace at the start of the session
CardSavrHttpClient session = new CardSavrHttpClient(_cardsavrServer, 
  _appKey, _appName, userName, password, null, "{\"key\": \"my_trace\"}");

//or per request
HttpRequestHeaders headers = new HttpRequestMessage().Headers;

headers.Add("x-cardsavr-trace", "{\"key\": \"my_trace\"}");
CardSavrResponse<List<User>> result = await http.GetUsersAsync(null, null, headers);
```

```java
CardsavrSession session = CardsavrSession.createSession(integratorName, integratorKey, apiServer);

//Add a trace at the start of the session
JsonObject trace = createObjectBuilder().add("key", "my_trace").build();
(JsonObject) session.login(username, password, trace);

//or per request
Headers headers = session.createHeaders();
headers.trace = trace;
session.post("/cardsavr_cards", body, headers);

```


```shell
curl "https://api.INSTANCE.cardsavr.io/cardsavr_users" 
  -H "x-cardsavr-trace: {\"key\": \"NlOFNNlKabi7Fn26CLw==\", \"bid\": \"hEOF26sbi7FCNNlLw==\"}" 
  -H "x-cardsavr-session-jwt: {{JWT_TOKEN}}"
```

`"x-cardsavr-trace": JSON-stringified trace object`

CardSavr uses trace headers to trace all request-related activity within the CardSavr infrastructure. When a request is made to CardSavr, any ID included in the trace header will appear in all logging associated with that request. This allows for quick troubleshooting and monitoring. .  

The trace header takes a JSON-stringified object, which can be as simple or as complex as necessary for the given application.  The trace is a **required header**, and must contain at least a trace "key".  Within the SDKs, the trace key defaults to the username of the session.

Type | Description | Example
--------- | ---------- | -----------
key | unique key that identifies a request or set of requests | `trace: '{ "key": "hEOFNKapn26sbi7FCNNlLw==" }'

A trace header can contain multiple trace IDs. It is up to the developer to mint trace IDs in a way that best categorizes their app's requests. If a backend server is used, adding the trace IDs into the backend server logs can yield additional tracing efficacy.

## Hydration

> Setting a sample Hydration Header

```javascript
await session.getCards(123, {}, { "x-cardsavr-hydration": JSON.stringify(["address"]) });
```

```csharp
HttpRequestHeaders headers = new HttpRequestMessage().Headers;
headers.Add("x-cardsavr-hydration", "[\"address\"]");
    
CardSavrResponse<List<Card>> result = await 
  http.GetCardsAsync(123);
```

```java
CardsavrSession header = session.createHeaders();
headers.hydration = Json.createArrayBuilder().add("address").build();

session.get("/cardsavr_cards", 1, headers);
```

```shell
curl "https://api.INSTANCE.cardsavr.io/cardsavr_cards/123" 
  -H "x-cardsavr-trace: {\"key\": \"NlOFNNlKabi7Fn26CLw==\"}" 
  -H "x-cardsavr-hydration: [\"address\"]" 
  -H "x-cardsavr-session-jwt: {{JWT_TOKEN}}"
```

```json
{
  "id": 123,
  "cardholder_id": 3,
  "bin_id": 5,
  "address_id": 7,
  "par": "Q1J4AwSWD4Dx6q1DTo0MB21XDAV76",
  "expiration_month": "03",
  "expiration_year": "20",
  "name_on_card": "Joe Smith",
  "first_name": "Joe",
  "last_name": "Smith",
  "created_on": "2019-02-06T20:33:23.094Z",
  "last_updated_on": "2019-03-13T22:32:30.897Z",
  "address": 
    { "cardholder_id": 3,
      "is_primary": false,
      "address1": "12345 Harris Ave",
      "address2": "STE. 601",
      "city": "Seattle",
      "subnational": "WA",
      "country": "USA",
      "postal_code": "98133",
      "postal_other": 98133-1234,
      "created_on": "2019-02-02T10:12:51.081Z",
      "last_updated_on": "2019-02-06T20:33:23.094Z"
  }
}
```

`{"x-cardsavr-hydration": {JSON-stringified array of resources to be hydrated}}`

For requests against a resource type that contains foreign key references (e.g. 'address_id' for 'cardsavr_cards'), a hydration header will "hydrate" (i.e. fill out) any of the resources indicated. Therefore, any objects returned in the response body will contain additional key-value pairs for each of the resources listed, where the key is the resource name (e.g. "address" in the previous example) and the value is the full object.

For example, including the header {hydration: '["address"]'} in a successful PUT request to '/cardsavr_cards/123' would return the updated card with an additional 'address' property containing the full address object associated with that card.

**Nested hydration** can also be used. For example, the following header:

`{"x-cardsavr-hydration": '["card.cardholder"]'}`

for the endpoint '/place_card_on_multiple_sites_jobs' would hydrate the associated card AND cardholder (i.e. user) associated with the card. Hydration headers can be used with any endpoint for any resource that contains foreign key references.

## Financial Institution

A financial-institution header is required on many calls that require FI specfic context.  For example, all cardholders must belong to a financial insitution, and thus the header is required upon creation.  The header is preferred over applying to the body to avoid the unnecessary extra lookup call.  The SDK functions that require the fi have a required parameter in the corresponding function.

## Client Application

> Setting a custom application header (defaults to app name)

```javascript
session.setSessionHeaders( {'client-application': 'my-client-app' });
```

```csharp
http.SetIdentificationHeader('my-client-app');
```

```java
//Not implemented, must pass as a header
```

```shell
curl "https://api.INSTANCE.cardsavr.io/cardsavr_cards/123" 
  -H "x-cardsavr-trace: {\"key\": \"NlOFNNlKabi7Fn26CLw==\"}" 
  -H "client-application: \"my-client-app\"" 
  -H "x-cardsavr-session-jwt: {{JWT_TOKEN}}"
```

`{'client-application': {client application name}}`

Your client application name will appear in the CardSavr logs alongside each request and response for your app, making troubleshooting and any other information retrieval much easier. Choose a name that clearly identifies your specific app for improved log searching (e.g. "acmebank-web-app").  When using the SDKs, the client-application defaults to the integrator name, and this is generally acceptable for most use cases.  This is an optional header, but recommended when not using the SDK.

## Paging

> Paging headers give you the flexibility to modify the number of results returned, and how they should be sorted.

```javascript
//javascript SDK supports a json object as a paging header
await session.getCards(123, {"sort":"id","is_descending":true,"page":1,"page_length":25});
```

```csharp
Paging paging = new Paging() { PageLength = 100, IsDescending = true, Page = 1, Sort = “id” };
CardSavrResponse<List<Card>> list = await http.getCardsAsync(null, paging);
```

```java
Headers headers = session.createHeaders();
headers.paging = Json.createObjectBuilder().add("page", 1).add("page_length", 5).add("is_descending", true).add("sort", "id").build();
session.post("/cardsavr_cards", body, headers);
```

```shell
curl "https://api.INSTANCE.cardsavr.io/cardsavr_cards/123" 
  -H "x-cardsavr-trace: {\"key\": \"NlOFNNlKabi7Fn26CLw==\"}" 
  -H "x-cardsavr-paging: \"{\"page\": \"1\"}\"" 
  -H "x-cardsavr-session-jwt: {{JWT_TOKEN}}"
```

`{'paging': 'JSON-stringified paging object'}`

CardSavr uses paging headers in both requests to and responses from batch GET endpoints. When sent with a batch GET request, a paging header specifies the length, sorting criterion, page number, and order of the data returned. Since each batch GET request can only return one page of data at a time, paging headers give users more control over the data they receive back.

If no paging header is submitted with the request, default values are applied (see table).

**Note**: CardSavr sends a paging header with each batch GET response to provide details about the page returned.

In the example header at right sent to '/cardsavr_cards', the second page of 25 results would be returned, sorted in descending order by PAR.

### Parameters
The paging header takes a JSON stringified object with the following properties. If a paging header is not included, the page of results will use the default values. Results are returned as an array.

Property name | Type | Description | Default value
------------- | -----| ----------- | -------------
page | integer | The page to be returned | 1
page_length | integer | Length of each page | 25
sort* | string | Property to sort results by | "id"
descending | boolean | If true, sorts results in descending order; if false, sorts in ascending order | false

*Check GET endpoint documentation to see which properties are sort-able

## Safe key

> Safe keys are required to encrypt PII data (email address, address, name) and PCI data (PAN, CVV)  Customers are encouraged to store their own safe keys outside the cardsavr environment.  This prevents the API from examining sensitive data.  If safe key storage is deemed unnecessary (espeically for short lived cardholders), Strivve has the ability to store the safe key on behalf of the customer.  By omitting the safe key when adding cardholders, Strive will generate a safe key and store it along with the cardholder, so there is no need to send a safe key header.  It is strongly encouraged not to use a Strivve managed safe key if cardholders are going to persist for long periods of time.

Although safe keys are stored with the cardholder, callers cannot persist a safe key on the body of the cardholder.  

```javascript
const body = { email : "foo@foo.com", cuid : "samplecuid"};
const res = await my_session.createCardholder(body, cardholder_safe_key);
```

```csharp
HttpRequestHeaders headers = new HttpRequestMessage().Headers;
AddSafeKeyHeader(headers, safeKey);

PropertyBag bag = new PropertyBag();
bag["id"] = 1;
bag["email"] = "foo@foo.com";
await http.UpdateUserAsync(bag.GetString("id"), bag, null, headers); //no paging
```

```java
Headers headers = session.createHeaders();
headers.safeKey = SAFE_KEY;
headers.newSafeKey = NEW_SAFE_KEY;

JsonObject obj = Json.createJsonBuilder().add("id", 1).build();
JsonObject response = session.update("/cardsavr_users", obj, headers);
```

```shell
curl "https://api.INSTANCE.cardsavr.io/cardsavr_users/1" 
  -X PUT
  -H "x-cardsavr-trace: {\"key\": \"NlOFNNlKabi7Fn26CLw==\"}" 
  -H "x-cardsavr-new-cardholder-safe-key: +h+W0c9EsgvFLufWnu87iV6ErDF7dpyT5YUEbb/oOIw=}" 
  -H "x-cardsavr-cardholder-safe-key: rttYqkGPHLk2KeK6OD8612gSurKXu0X8W6BTWF3hhGM=}" 
  -H "x-cardsavr-session-jwt: {{JWT_TOKEN}}"
  -B "{ \"id\": 1, \"cardholder_safe_key\": \"+h+W0c9EsgvFLufWnu87iV6ErDF7dpyT5YUEbb/oOIw=\" }" 
```

`{'cardholder-safe-key': 'rttYqkGPHLk2KeK6OD8612gSurKXu0X8W6BTWF3hhGM='}`
`{'new-cardholder-safe-key': '+h+W0c9EsgvFLufWnu87iV6ErDF7dpyT5YUEbb/oOIw='}`

You must send an encrypted cardholder safe key header for each request that involves safe-protected information. Saving users (/cardsavr_users), accounts (/cardsavr_accounts) and cards (/cardsavr_cards) requires the key in order to write encrypted data like PANs and merchant site passwords to the server side safe.  Safe keys can be stored by the third party, or they can optionally be stored by Strivve within Cardsavr. Individual endpoint documentation will indicate if a safe key header is required.

When rotating a safe key, you must provide a 'new-cardholder-safe-key' header.  Both headers are required (new- and existing) in this case.

See the [cardholder safe key section](https://swch.github.io/slate/?javascript#safe-key) for more information on generating and using safe keys.

# API Usage 

Query parameter filters can be used with GET requests that do not have an ID path parameter (i.e. '/cardsavr_cards' but not '/cardsavr_cards/123'). When using a query filter, you must place a '?' after the endpoint (preceding the first query filter). Mutiple query filters must be separated by an '&'. There are six filter types in CardSavr:

## GET Filters

> Filters can be aggregated together to apply multiple filters

```javascript
const merchants = await session.getMerchantSites({ top_hosts : "amazon.com,apple.com", exclude_hosts : "walmart.com" });
```

```csharp
CardSavrResponse<List<MerchantSite>> merchants = await http.GetMerchantSitesAsync(
    new NameValueCollection() {
        { "top_hosts", "amazon.com,apple.com"}, {"exclude_hosts", "walmart.com" }
    }
);
```

```java
  List<NameValuePair> filters = new ArrayList<>(1);
  filters.add(new BasicNameValuePair("tags", "canada"));
  JsonArray response = (JsonArray)session.get("/merchant_sites", filters, null);
```


```shell
curl "https://api.INSTANCE.cardsavr.io/cardsavr_users?top_hosts=amazon.com,apple.com&exclude_hosts=walmart.com" 
  -H "x-cardsavr-trace: {\"key\": \"NlOFNNlKabi7Fn26CLw==\"}" 
  -H "x-cardsavr-session-jwt: {{JWT_TOKEN}}"
```

### Singular filters

**Singular filters** select for results with one specific value. If the property has a unique constraint (e.g. "username" for '/cardsavr_users'), the singular filter can only select one object.

For string properties, singular filters always use **partial** matching, meaning they will match any string that contains the filter value as a substring.

### Multiple filters

**Multiple filters** select for any object containing one of the specified values for a property. Multiple values must be separated by commas and no spaces. A single value can be submitted for multiple filter, as well.

Multiple filters for string properties always use **partial** matching, meaning they will match any string that contains the filter value as a substring.

<aside class="notice">
"/cardsavr_accounts?cardholder_ids=1,2,3" would return accounts associated with the cardholders that have the IDs 1, 2, and 3.
</aside>

### Starts-with filters

**Starts-with** filters select all objects where the property value begins with the provided query value.

<aside class="notice">
"/merchant_sites?name_starts_with=a" returns all sites with names beginning with A (e.g. names of "Apple", "Amazon", "Atlantis").
</aside>

### Top filters

**Top filters** select for objects with specified properties to be returned first, in the order specified.

<aside class="notice">
"/merchant_sites?top_ids=2,4,6" would return an array with sites with IDs 2,4,6 in the 1st, 2nd, and 3rd index positions, respectively, with any additional matching objects returned after.
</aside>

### Include/exclude filters

**Include filters** select for any objects that have the specified property value. Unlike multiple filters, include filters use exact matching.

<aside class="notice">
"/cardsavr_users?roles_include=cardholder_agent,customer_agent" returns users with roles of cardholder_agent and customer_agent.
"/cardsavr_users?roles_include=dev,ana" would return no users, as "dev" and "ana" are not roles defined in CardSavr.
</aside>

**Exclude filters** select for any objects that do NOT have the specified property value.  Exclude filters use exact matching.

<aside class="notice">
"/cardsavr_users?roles_exclude=cardholder,admin" filters out users with the roles cardholder and admin.
</aside>

### Min/Max filters

**Max filters** select for objects that have a value equal to or less than the specified value.

<aside class="notice">
"/cardsavr_accounts?created_on_max=2018-04-20T23:10:36.657Z" returns accounts that were created on or before the date string 2018-04-20T23:10:36.657Z.
</aside>

**Min filters** select for any objects that have a value equal to or greater than the specified value.

<aside class="notice">
'/cardsavr_accounts?created_on_min=2018-04-20T23:10:36.657Z' returns accounts that were created on or after the date string 2018-04-20T23:10:36.657Z.
</aside>

## Cascading DELETE

> Deleting user 123 will delete their corresponding jobs, cards, and addresses.  Their job results will remain.

```javascript
await session.deleteCardholder(123); 
```

```csharp
await http.DeleteCardholderAsync(123);
```

```java
session.delete("/cardholder", 123);
```

```shell
curl "https://api.INSTANCE.cardsavr.io/cardsavr_users" 
  -X DELETE
  -H "x-cardsavr-trace: {\"key\": \"NlOFNNlKabi7Fn26CLw==\"}" 
  -B "{ \"id\": 123 }" 
  -H "x-cardsavr-session-jwt: {{JWT_TOKEN}}"
```

A successful DELETE request will also delete any object that references the deleted object. The additional object types that will be deleted for a particular DELETE endpoint are listed in the individual endpoint documentation.

For example, a successful DELETE request to '/cardsavr_accounts/123' would also delete any single-site jobs that reference the account with ID 123, as single-site jobs contain a foreign key reference to an account.

## Plural POST

```javascript
await session.createSingleSiteJobs([{"cardholder_id": 1, "account_id": 1, "status" : "REQUESTED"}, 
                                    {"cardholder_id": 2, "account_id": 2, "status" : "REQUESTED"}]); 
```

```csharp
//unsupported
```

```java
JsonArray body = Json.createArrayBuilder()
  .add(Json.createJsonBuilder().add("cardholder_id", 1).add("account_id", 1).add("status", "REQUESTED").build())
  .add(Json.createJsonBuilder().add("cardholder_id", 1).add("account_id", 2).add("status", "REQUESTED").build())
  .build();
await session.post("/place_card_on_single_site_jobs", body, null);
```

```shell
curl "https://api.INSTANCE.cardsavr.io/place_card_on_single_site-jobs" 
  -X POST
  -H "x-cardsavr-trace: {\"key\": \"NlOFNNlKabi7Fn26CLw==\"}" 
  -B "{\"cardholder_id\": 1, \"account_id\": 1, \"status\" : \"REQUESTED\"}, {\"cardholder_id\": 1, \"account_id\": 2, \"status\" : \"REQUESTED\"}]" 
  -H "x-cardsavr-session-jwt: {{JWT_TOKEN}}"
```

Some objects support bulk creation (e.g. single site jobs).  This is accomplished by passing in array of objects rather than simply a single object.  

## Plural PUT/DELETE

Some objects support updating and deleting using the standard filter parameters (e.g. single site jobs).  This is noted in the per-object documentation.

## Customer keys and Upserting

Cards, cardholders, and accounts support external references.  This enables integrators to access entities using alternative namespaces rather than by the cardsavr supplied ids.  These external references are generally existing entities in the integrators system (e.g. a cardholder bank account id).  

Integrators can also "upsert" these entities by providing the customer_key rather than cardsavr ids.  If the entity exists, it is merely updated and returned.  If the entity does not exist, it will be created.  This simplifies the integration and can reduce the complexity of the integrator's middleware.

Entity | External ID | Default | card_placement_result column
------ | ---- | ----------- | ----------------
Cardholder | cuid | random | cuid
Card | customer_key | random | card_customer_key
Account | customer_key | merchant site, $, and cuid concatenated | account_customer_key

<aside class="notice">
The par is an alternate customer_key for the card entity (for backward compatibility).  If a par is supplied without a customer_key, the par will be used.  If they are both supplied, the par cannot be used as an upserting key.  If the are both omitted, the PAR remains null, and the customer_key gets set to a random value.
</aside>


## Request Hydration on POST

```javascript
await session.createSingleSiteJob(body); 
```

```csharp
//unsupported
```

```java
JsonObject body = Json.createObjectBuilder()
  .add(... //various nested properties using JsonObjects and JsonArrays (JsonValues)
  .build();
await session.post("/place_card_on_single_site_jobs", body, null);
```

```shell
curl "https://api.INSTANCE.cardsavr.io/place_card_on_single_site-jobs" 
  -X POST
  -H "x-cardsavr-trace: {\"key\": \"NlOFNNlKabi7Fn26CLw==\"}" 
  -B "{\"cardholder_id\": 1, \"account_id\": 1, \"status\" : \"REQUESTED\"}, {\"cardholder_id\": 1, \"account_id\": 2, \"status\" : \"REQUESTED\"}]" 
  -H "x-cardsavr-session-jwt: {{JWT_TOKEN}}"
```

```json
{
  "status": "REQUESTED",
  "cardholder":
    {
      "cuid":"12345678",
    },
  "card":
    {
      "cardholder_ref": {
        "cuid": "12345678"
      },
      "customer_key":"12345678",
      "par":"peLpzDnEHdhiiWEtuhUgIbN12345678",
      "pan":"KOnalFfwdrBXlZD",
      "cvv":"123",
      "expiration_month":12,
      "expiration_year":24,
      "name_on_card":"FirstName LastName",
      "address":
        {
          "cardholder_ref": {
            "cuid": "12345678"
          },
          "first_name":"Switch",
          "last_name":"Strivve",
          "address1":"SGTClNSCCMqlfjuzTmJuepDyFgvWhlCMRycXlKGiRIooOJJkoXeObOcAwJMGeqjSDWfhTHobAWMimcCynMIQcvlBFSbMQlwUFyJ",
          "address2":"AyFgoCTjCLXUQVylBAfkHJOtqkkKJjuaLHnmJpSctqBOQueIvciyAUPqYoFpkiAPlkGjgPuabhAPCHFPvaxciObOmIBvBUWpngD",
          "city":"Seattle",
          "subnational":"WA",
          "postal_code":"98177",
          "email":"email@domain.com",
          "phone_number":"5555555555",
          "country":"USA",
          "is_primary": true
        }
    },
  "account":
    {
      "cardholder_ref": {
        "cuid": "12345678"
      },
      "merchant_site_id":1,
      "username":"bad_email",
      "password":"good_password"
    }
}
```
Some objects support posting multiple nested objects to avoid multiple server calls.  This is supported by the Single Site Job, Card, Account and Address APIs.  For example, a Job can be posted with a nested cardholder, account, and a card (the card can even have a nested address).  This is currently only supported when single jobs are posted, not with Plural POSTs.  

If a nested cardholder is referenced by multiple objects, the nested object should reference the created instance using the cardholder cuid.  Notice the body required on the request to the right.  A cardholder_ref parameter is required on card, account, and address entities to ensure the correstponding cardholder_id properties are filled in properly.