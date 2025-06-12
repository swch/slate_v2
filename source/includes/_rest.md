
# Accounts
Account objects contain the account information, such as username and password, for a particular cardhoder. They are used to log in to a cardholder's account for placing a payment card.
## Get account

```javascript
const accounts = await session.getAccounts(47228145,{"sort":"id","is_descending":true,"page":1, "page_length":25,{'x-cardsavr-hydration':JSON.stringify(["cardholder","merchant_site","cardsavr_card"])});
```

```csharp
Paging paging = new Paging() { PageLength = 100, IsDescending = true, Page = 1, Sort = "id" };
HttpRequestHeaders headers = new HttpRequestMessage().Headers;
string[] array = { "cardholder","merchant_site","cardsavr_card" };
var json = JsonConvert.SerializeObject(array);
headers.Add("x-cardsavr-hydration", json);
var query = new {ids = 1};
QueryDef qd = new QueryDef(query);
CardSavrResponse<Accounts> accounts = await session.GetAccountsAsync(qd,paging,headers);
```

```java
Headers headers = session.createHeaders();
headers.paging = Json.createObjectBuilder().add("page", 1).add("page_length", 5).add("is_descending", true).add("sort", "id").build();
headers.hydration = {'x-cardsavr-hydration':JSON.stringify(["cardholder","merchant_site","cardsavr_card"])}
JsonArray response = (JsonArray)session.get(47228145, null, headers);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 47228145,
  "last_password_update": "1979-12-12T03:49:13.139Z",
  "last_saved_card": "2002-05-04T03:36:43.354Z",
  "created_on": "2008-11-18T07:43:23.338Z",
  "last_updated_on": "1975-05-17T15:54:45.367Z",
  "cardholder": {
    "id": 556795655,
    "type": "ephemeral",
    "first_name": "Jane",
    "last_name": "Smith",
    "email": "test_email@strivve.com",
    "meta_key": "gRTuwgIODUkS",
    "webhook_url": "https://mywebhooks.com/this",
    "custom_data": {
      "CvyxZweDlkFn": "jnix!vlJ2",
      "wDbxreWiNwvc": 68,
      "ywTiaWkRdNgG": false
    },
    "created_on": "1998-04-22T08:06:09.705Z",
    "last_updated_on": "2002-04-03T19:23:10.423Z",
    "cuid": "nUKDfBWfn",
    "source": {
      "type": "weblink",
      "category": "campaign",
      "sub_category": "fDO",
      "device": "desktop web",
      "integration": "CS"
    }
  },
  "merchant_site": {
    "id": 686396852,
    "name": "Amazon",
    "note": "NIGwHAOJKlxiOLPrcosUWyxIn",
    "host": "amazon.com",
    "tags": [
      "]&r{b28d4UuxbF5vqC3![t",
      94,
      "54_Ba!38R*Vw%){dEb_"
    ],
    "interface_type": "rpa",
    "job_type": "BILL_PAY",
    "required_form_fields": [
      "email",
      "phone_number",
      "card_data",
      "cvv",
      "billing_address",
      "postal_code"
    ],
    "images": [
      {
        "url": "https://d1t7g1oas7m24a.cloudfront.net/tiles/dollarshaveclub.com?width=128&version=21f917315911eec1b1705bc7784ce861579cff2b",
        "width": 128,
        "grayscale": false
      },
      {
        "url": "https://d1t7g1oas7m24a.cloudfront.net/tiles/dollarshaveclub.com?width=32&version=21f917315911eec1b1705bc7784ce861579cff2b",
        "width": 32,
        "grayscale": false
      }
    ],
    "account_link": [
      {
        "key_name": "username",
        "label": "Username",
        "type": "initial_account_link"
      },
      {
        "key_name": "password",
        "label": "Password",
        "type": "initial_account_link",
        "secret": true
      },
      {
        "key_name": "otp",
        "label": "One Time Passcode",
        "type": ""
      }
    ],
    "messages": {
      "mfa_label": "Additional information required, this code may be sent to your phone or email address.",
      "additional_info_message": "",
      "auth_message": "Linking account."
    },
    "login_page": "https://www.merchantsite.com/login",
    "forgot_password_page": "https://www.merchantsite.com/forgot_password",
    "credit_card_page": "https://www.merchantsite.com/credit_card",
    "wallet_page": "CPQxAkIaPAOvNl",
    "merchant_sso_group": "GycelkTjmnLWyMCHxPqhqsKnD",
    "tier": 1424929660
  },
  "cardsavr_card": {
    "id": 104850381,
    "type": "American Express",
    "expiration_month": 12,
    "expiration_year": 24,
    "name_on_card": "Jane Smith",
    "last_4": "GPuw",
    "nickname": "Jane's VISA",
    "custom_data": {
      "qaaRUOQhhnrO": "I$.t",
      "hEzpstbIUvtv": 90,
      "rOntMbOcVlTk": false
    },
    "created_on": "1985-12-04T15:52:37.901Z",
    "last_updated_on": "2005-07-20T21:46:36.446Z",
    "par": "kghhnyaeovyGmjbsqbfyTjGYVsDYR",
    "customer_key": "hKhXFWeR"
  },
  "customer_key": "pZBdSaUpMoLsLAbTPXxDxg"
}
```

### Path

GET /cardsavr_accounts **(batch)** or GET /cardsavr_accounts/:id **(singular)**

### Description

Returns the account specified by the provided ID

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

#### Batch GET requests

**Batch requests** return the first page of all viewable accounts, filtered by any [query filters](#get-filters) (see list of possible parameters below) listed in the path.


### Filter parameters
- ids / id (in path)
- cardholder_ids
- merchant_site_ids
- customer_key
- last_card_placed_ids
- last_password_update_min / last_password_update_max
- last_saved_card_min / last_saved_card_max
- created_on_min / created_on_max
- last_updated_on_min / last_updated_on_max

**Example batch GET request path:**<br>`/cardsavr_accounts?ids=1,2`

#### Singular GET requests

**Singular requests** only return the account matching the id provided in the path.

**Example GET request path:**<br>`/cardsavr_accounts/47228145`

### <a name="response-cardsavr_account"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number (pk) | Unique ID of this account.
last_card_placed_id | number (fk) [cards](#cards) | ID of the last card placed on this account by the Virtual Browser System (VBS).
last_password_update | date | 
last_saved_card | date | Date of last card saved on this account.
created_on | date | Date this site was created on
last_updated_on | date | Date this site was last updated on
cardholder_id | number (fk) [cardholders](#cardholders) | ID of the cardholder associated with this account.
merchant_site_id | number (fk) [merchant sites](#merchant-sites) | ID of the merchant site associated with this account.
customer_key | string | An external reference to a merchant site for a specific cardholder.  A key of merchant host and cuid will be used if none provided. The default can potentially violate a constraint with two accounts of the same merchant site.

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

## Create account

```javascript
const account = await session.createAccount({
  "cardholder_id": 306826734,
  "merchant_site_id": 1054667915,
  "customer_key": "pZBdSaUpMoLsLAbTPXxDxg",
  "last_card_placed_id": 665343525,
  "account_link": {
    "username": "jsmith123",
    "password": "BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI="
  }
}, CARDHOLDER_SAFE_KEY);
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "cardholder_id", 306826734 },
	{ "merchant_site_id", 1054667915 },
	{ "customer_key", "pZBdSaUpMoLsLAbTPXxDxg" },
	{ "last_card_placed_id", 665343525 }
};

CardSavrResponse<Account> account = await http.CreateAccountAsync(body, CARDHOLDER_SAFE_KEY);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("cardholder_id", 306826734 )
	.add("merchant_site_id", 1054667915 )
	.add("customer_key", "pZBdSaUpMoLsLAbTPXxDxg" )
	.add("last_card_placed_id", 665343525 )
	.build();
JsonValue account = session.post("/cardsavr_accounts", body, null, null);
```

```shell
curl -d "{\"cardholder_id\":306826734,\"merchant_site_id\":1054667915,\"customer_key\":\"pZBdSaUpMoLsLAbTPXxDxg\",\"last_card_placed_id\":665343525,\"account_link\":{\"username\":\"jsmith123\",\"password\":\"BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI=\"}}"
-X POST -H "Content-Type: application/json"
-H "x-cardsavr-cardholder-safe-key: CARDHOLDER_SAFE_KEY"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/cardsavr_accounts/
```

### Path

POST /cardsavr_accounts

### Description

Create a account and return the created object.

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.



<aside class="notice"><a href=#request-hydration-on-post>Request hydration</a> can be used on this endpoint. This allows you to create a new account and all referential entities in a single POST request.
</aside>

### Body parameters

Parameter | Type | Required | Description
-------- | ---- | --------- | ----------
cardholder_id | number | yes | ID of the cardholder associated with this account.
merchant_site_id | number | yes | ID of the merchant site associated with this account.
customer_key | string | yes | An external reference to a merchant site for a specific cardholder.  A key of merchant host and cuid will be used if none provided. The default can potentially violate a constraint with two accounts of the same merchant site.
last_card_placed_id | number | no | ID of the last card placed on this account by the Virtual Browser System (VBS).
account_link | object | no | One or more properties with key:value pairs that are required for authenticated a user.  These properties are either included as part of initial account collection, or they are requested as part of a credential_request.  An error will be returned if all properties are not provided for a given credential_request. The set of key:value pairs for a site are specified in the merchant site info returned from GET /merchant_sites as 'account_link'.  If credentials are being saved as part of a credential_response, the corresponding envelope_id must be supplied as a header.

See [account response attributes](#response-cardsavr_account).

<aside class="notice">Update calls to /cardsavr_accounts require the cardholder's personal cardholder_safe_key header to encrypt and save the account_link when Strivve does not manage keys for a customer (this is an environment setting). The safe keys are also not required if updating non-safe user properties.</aside>

## Upsert account

```javascript
const account = await session.updateAccount(1,{
  "last_card_placed_id": 104291080,
  "account_link": {
    "username": "jsmith123",
    "password": "BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI="
  }
}, null, CARDHOLDER_SAFE_KEY);
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "last_card_placed_id", 104291080 }
};

CardSavrResponse<Account> account = await http.UpdateAccountAsync(body, CARDHOLDER_SAFE_KEY);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("last_card_placed_id", 104291080 )
	.build();
JsonValue account = session.put("/cardsavr_accounts", body, null, null);
```

```shell
curl -d "{\"last_card_placed_id\":104291080,\"account_link\":{\"username\":\"jsmith123\",\"password\":\"BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI=\"}}"
-X PUT -H "Content-Type: application/json"
-H "cardholder-safe-key: CARDHOLDER_SAFE_KEY"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/cardsavr_accounts/47228145
```

### Path

PUT /cardsavr_accounts OR /cardsavr_accounts/{id}

### Description

Upsert can be used to either update a account, create a new account, or return an existing account.  Either an id or customer_key is required for upsert. The id (in path or body), along with an updated body, can be used to update an existing account; the customer_key (in body) can likewise be used to update a account, and can also be used to create a new account, if the customer_key does not match any existing accounts. If the id or customer_key provided corresponds to a pre-existing account and no updated information has been included in the body, the existing account will be returned.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

### Body parameters

Parameter | Type | Description 
-------- | ---- | ---------
last_card_placed_id | number | ID of the last card placed on this account by the Virtual Browser System (VBS).
account_link | object | One or more properties with key:value pairs that are required for authenticated a user.  These properties are either included as part of initial account collection, or they are requested as part of a credential_request.  An error will be returned if all properties are not provided for a given credential_request. The set of key:value pairs for a site are specified in the merchant site info returned from GET /merchant_sites as 'account_link'.  If credentials are being saved as part of a credential_response, the corresponding envelope_id must be supplied as a header.

See [account response parameters](#response-cardsavr_account).

<aside class="notice">Update calls to /cardsavr_accounts require the cardholder's personal cardholder_safe_key header to encrypt and save the account_link when Strivve does not manage keys for a customer (this is an environment setting). The safe keys are also not required if updating non-safe properties.</aside>

## Delete account

```shell
curl -X DELETE
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/cardsavr_accounts/47228145
```

```javascript
await session.deleteAccount(undefined);
```

```csharp
CardSavrResponse<Account> account = await http.DeleteAccountAsync(undefined);
```

```java
JsonValue account = session.delete("/cardsavr_accounts", undefined, null);
```

### Path

DELETE /cardsavr_accounts/{id}

### Description

Delete a account and purge its [related items](#cascading-delete).  An id is required on every delete request.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.


See [account response parameters](#response-cardsavr_account).


# Addresses
Address objects contain the billing address for a specific cardholder, and are used to populate billing address information on merchant sites. They are linked to cards and cardholders.
## Get address

```javascript
const addresses = await session.getAddresses(485193468,{"sort":"id","is_descending":true,"page":1, "page_length":25,{'x-cardsavr-hydration':JSON.stringify(["cardholder"])});
```

```csharp
Paging paging = new Paging() { PageLength = 100, IsDescending = true, Page = 1, Sort = "id" };
HttpRequestHeaders headers = new HttpRequestMessage().Headers;
string[] array = { "cardholder","merchant_site","cardsavr_card" };
var json = JsonConvert.SerializeObject(array);
headers.Add("x-cardsavr-hydration", json);
var query = new {ids = 1};
QueryDef qd = new QueryDef(query);
CardSavrResponse<Addresses> addresses = await session.GetAddressesAsync(qd,paging,headers);
```

```java
Headers headers = session.createHeaders();
headers.paging = Json.createObjectBuilder().add("page", 1).add("page_length", 5).add("is_descending", true).add("sort", "id").build();
headers.hydration = {'x-cardsavr-hydration':JSON.stringify(["cardholder"])}
JsonArray response = (JsonArray)session.get(485193468, null, headers);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 485193468,
  "address1": "hYzNbLmtguCPlxYpzQtXrftFmUOtACRRpTaFOGOqPTEytBDulBtdsmhVpKGPfkOAQymXDXtksfJPzsFkxJizchsZZFFoAGJEiIl",
  "address2": "nWzmuqDsUoIyQCwhGRTwJJbTCHXnFDlafZFnecgKJaXttgGjwUNJJGFBcphDSbXQWLNIZhjxMNaBfoyYXoTrFrmUzHhOmtXAiIN",
  "city": "Seattle",
  "subnational": "WA",
  "postal_code": "98177",
  "postal_other": "98177-0124",
  "country": "USA",
  "is_primary": true,
  "first_name": "Jane",
  "last_name": "Smith",
  "email": "JaDFtLNxxWuy@uGZfJV.fSq",
  "phone_number": "2065555555",
  "created_on": "2021-08-01T21:16:47.215Z",
  "last_updated_on": "1999-08-09T14:59:13.670Z",
  "cardholder": {
    "id": 992738950,
    "type": "ephemeral",
    "first_name": "Jane",
    "last_name": "Smith",
    "email": "test_email@strivve.com",
    "meta_key": "BNWEliIkHXMPAeKLaUgaA",
    "webhook_url": "https://mywebhooks.com/this",
    "custom_data": {
      "SoJKgcjsXMOI": ",6v7pFpD1Q=z6JXsX7n",
      "nqtVACfTZUps": 60,
      "MQPbJEJFQKon": true
    },
    "created_on": "2000-04-24T02:47:02.980Z",
    "last_updated_on": "1985-06-02T06:09:28.490Z",
    "cuid": "ZMmzGBXNHD",
    "source": {
      "type": "test",
      "category": "other",
      "sub_category": "$,%",
      "device": "mobile app",
      "integration": "CU2"
    }
  }
}
```

### Path

GET /cardsavr_addresses **(batch)** or GET /cardsavr_addresses/:id **(singular)**

### Description

Returns the address specified by the provided ID

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

#### Batch GET requests

**Batch requests** return the first page of all viewable addresses, filtered by any [query filters](#get-filters) (see list of possible parameters below) listed in the path.


### Filter parameters
- ids / id (in path)
- cardholder_ids
- is_primary
- first_name
- last_name
- email
- created_on_min / created_on_max
- last_updated_on_min / last_updated_on_max

**Example batch GET request path:**<br>`/cardsavr_addresses?ids=1,2`

#### Singular GET requests

**Singular requests** only return the address matching the id provided in the path.

**Example GET request path:**<br>`/cardsavr_addresses/485193468`

### <a name="response-cardsavr_address"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number (pk) | Unique ID of this address.
address1 | string | 
address2 | string | Second line of address, if one exists (e.g. apartment number).
city | string | 
subnational | string | Subnational unit (i.e. state or province).
postal_code | string | 
postal_other | string | E.g. last four digits in a zip-plus-four.
country | string | 
is_primary | boolean | Indicates if this is the primary address of this cardholder, as a cardholder can be linked to multiple addresses.
first_name | string | 
last_name | string | 
email | string | 
phone_number | string | 
created_on | date | Date this site was created on
last_updated_on | date | Date this site was last updated on
cardholder_id | number (fk) [cardholders](#cardholders) | ID of the cardholder associated with this address.

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

## Create address

```javascript
const address = await session.createAddress({
  "cardholder_id": 1256039491,
  "address1": "hYzNbLmtguCPlxYpzQtXrftFmUOtACRRpTaFOGOqPTEytBDulBtdsmhVpKGPfkOAQymXDXtksfJPzsFkxJizchsZZFFoAGJEiIl",
  "address2": "nWzmuqDsUoIyQCwhGRTwJJbTCHXnFDlafZFnecgKJaXttgGjwUNJJGFBcphDSbXQWLNIZhjxMNaBfoyYXoTrFrmUzHhOmtXAiIN",
  "city": "Seattle",
  "subnational": "WA",
  "postal_code": "98177",
  "postal_other": "98177-0124",
  "country": "USA",
  "is_primary": true,
  "first_name": "Jane",
  "last_name": "Smith",
  "email": "JaDFtLNxxWuy@uGZfJV.fSq",
  "phone_number": "2065555555"
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "cardholder_id", 1256039491 },
	{ "address1", "hYzNbLmtguCPlxYpzQtXrftFmUOtACRRpTaFOGOqPTEytBDulBtdsmhVpKGPfkOAQymXDXtksfJPzsFkxJizchsZZFFoAGJEiIl" },
	{ "address2", "nWzmuqDsUoIyQCwhGRTwJJbTCHXnFDlafZFnecgKJaXttgGjwUNJJGFBcphDSbXQWLNIZhjxMNaBfoyYXoTrFrmUzHhOmtXAiIN" },
	{ "city", "Seattle" },
	{ "subnational", "WA" },
	{ "postal_code", "98177" },
	{ "postal_other", "98177-0124" },
	{ "country", "USA" },
	{ "is_primary", true },
	{ "first_name", "Jane" },
	{ "last_name", "Smith" },
	{ "email", "JaDFtLNxxWuy@uGZfJV.fSq" },
	{ "phone_number", "2065555555" }
};

CardSavrResponse<Address> address = await http.CreateAddressAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("cardholder_id", 1256039491 )
	.add("address1", "hYzNbLmtguCPlxYpzQtXrftFmUOtACRRpTaFOGOqPTEytBDulBtdsmhVpKGPfkOAQymXDXtksfJPzsFkxJizchsZZFFoAGJEiIl" )
	.add("address2", "nWzmuqDsUoIyQCwhGRTwJJbTCHXnFDlafZFnecgKJaXttgGjwUNJJGFBcphDSbXQWLNIZhjxMNaBfoyYXoTrFrmUzHhOmtXAiIN" )
	.add("city", "Seattle" )
	.add("subnational", "WA" )
	.add("postal_code", "98177" )
	.add("postal_other", "98177-0124" )
	.add("country", "USA" )
	.add("is_primary", true )
	.add("first_name", "Jane" )
	.add("last_name", "Smith" )
	.add("email", "JaDFtLNxxWuy@uGZfJV.fSq" )
	.add("phone_number", "2065555555" )
	.build();
JsonValue address = session.post("/cardsavr_addresses", body, null, null);
```

```shell
curl -d "{\"cardholder_id\":1256039491,\"address1\":\"hYzNbLmtguCPlxYpzQtXrftFmUOtACRRpTaFOGOqPTEytBDulBtdsmhVpKGPfkOAQymXDXtksfJPzsFkxJizchsZZFFoAGJEiIl\",\"address2\":\"nWzmuqDsUoIyQCwhGRTwJJbTCHXnFDlafZFnecgKJaXttgGjwUNJJGFBcphDSbXQWLNIZhjxMNaBfoyYXoTrFrmUzHhOmtXAiIN\",\"city\":\"Seattle\",\"subnational\":\"WA\",\"postal_code\":\"98177\",\"postal_other\":\"98177-0124\",\"country\":\"USA\",\"is_primary\":true,\"first_name\":\"Jane\",\"last_name\":\"Smith\",\"email\":\"JaDFtLNxxWuy@uGZfJV.fSq\",\"phone_number\":\"2065555555\"}"
-X POST -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/cardsavr_addresses/
```

### Path

POST /cardsavr_addresses

### Description

Create a address and return the created object.

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.



<aside class="notice"><a href=#request-hydration-on-post>Request hydration</a> can be used on this endpoint. This allows you to create an new address and all referential entities in a single POST request.
</aside>

### Body parameters

Parameter | Type | Required | Description
-------- | ---- | --------- | ----------
cardholder_id | number | yes | ID of the cardholder associated with this address.
address1 | string | yes | 
address2 | string | no | Second line of address, if one exists (e.g. apartment number).
city | string | yes | 
subnational | string | yes | Subnational unit (i.e. state or province).
postal_code | string | yes | 
postal_other | string | no | E.g. last four digits in a zip-plus-four.
country | [string enum](#post-cardsavr_address-1)* | no | 
is_primary | boolean | yes | Indicates if this is the primary address of this cardholder, as a cardholder can be linked to multiple addresses.
first_name | string | no | 
last_name | string | no | 
email | string | no | 
phone_number | string | no | 

See [address response attributes](#response-cardsavr_address).

#### <a name="post-cardsavr_address-1"></a>string enum*
- usa
- USA
- us
- US
- canada
- Canada
- ca
- CA


## Update address

```javascript
const address = await session.updateAddress(1,{
  "address1": "lLuIcyMuMmQIhZVJKCHLGSnmTFsdTdDUtaTOglcfMeYVlpbXiRvTXMSRsufIbWCKvRDRiWOLnAityehTFiPBnpDFszlhcgbbxgS",
  "address2": "yOsjKrxxKmkVzzTMxmnIwUwdUtGEiuwhGVWEabWMPPKcvdHTlxBwdPDiqxCajCdLmsiaTjOwGAFlmzKyncRtRShioVYxaIMsurZ",
  "city": "Seattle",
  "subnational": "WA",
  "postal_code": "98177",
  "postal_other": "98177-0124",
  "country": "USA",
  "is_primary": true,
  "first_name": "Jane",
  "last_name": "Smith",
  "email": "XxvBARBymInV@mIIPHj.AOk",
  "phone_number": "2065555555"
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "address1", "lLuIcyMuMmQIhZVJKCHLGSnmTFsdTdDUtaTOglcfMeYVlpbXiRvTXMSRsufIbWCKvRDRiWOLnAityehTFiPBnpDFszlhcgbbxgS" },
	{ "address2", "yOsjKrxxKmkVzzTMxmnIwUwdUtGEiuwhGVWEabWMPPKcvdHTlxBwdPDiqxCajCdLmsiaTjOwGAFlmzKyncRtRShioVYxaIMsurZ" },
	{ "city", "Seattle" },
	{ "subnational", "WA" },
	{ "postal_code", "98177" },
	{ "postal_other", "98177-0124" },
	{ "country", "USA" },
	{ "is_primary", true },
	{ "first_name", "Jane" },
	{ "last_name", "Smith" },
	{ "email", "XxvBARBymInV@mIIPHj.AOk" },
	{ "phone_number", "2065555555" }
};

CardSavrResponse<Address> address = await http.UpdateAddressAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("address1", "lLuIcyMuMmQIhZVJKCHLGSnmTFsdTdDUtaTOglcfMeYVlpbXiRvTXMSRsufIbWCKvRDRiWOLnAityehTFiPBnpDFszlhcgbbxgS" )
	.add("address2", "yOsjKrxxKmkVzzTMxmnIwUwdUtGEiuwhGVWEabWMPPKcvdHTlxBwdPDiqxCajCdLmsiaTjOwGAFlmzKyncRtRShioVYxaIMsurZ" )
	.add("city", "Seattle" )
	.add("subnational", "WA" )
	.add("postal_code", "98177" )
	.add("postal_other", "98177-0124" )
	.add("country", "USA" )
	.add("is_primary", true )
	.add("first_name", "Jane" )
	.add("last_name", "Smith" )
	.add("email", "XxvBARBymInV@mIIPHj.AOk" )
	.add("phone_number", "2065555555" )
	.build();
JsonValue address = session.put("/cardsavr_addresses", body, null, null);
```

```shell
curl -d "{\"address1\":\"lLuIcyMuMmQIhZVJKCHLGSnmTFsdTdDUtaTOglcfMeYVlpbXiRvTXMSRsufIbWCKvRDRiWOLnAityehTFiPBnpDFszlhcgbbxgS\",\"address2\":\"yOsjKrxxKmkVzzTMxmnIwUwdUtGEiuwhGVWEabWMPPKcvdHTlxBwdPDiqxCajCdLmsiaTjOwGAFlmzKyncRtRShioVYxaIMsurZ\",\"city\":\"Seattle\",\"subnational\":\"WA\",\"postal_code\":\"98177\",\"postal_other\":\"98177-0124\",\"country\":\"USA\",\"is_primary\":true,\"first_name\":\"Jane\",\"last_name\":\"Smith\",\"email\":\"XxvBARBymInV@mIIPHj.AOk\",\"phone_number\":\"2065555555\"}"
-X PUT -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/cardsavr_addresses/485193468
```

### Path

PUT /cardsavr_addresses OR /cardsavr_addresses/{id}

### Description

Update a address and return the updated object.  An id is required on every update request.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

### Body parameters

Parameter | Type | Description 
-------- | ---- | ---------
address1 | string | 
address2 | string | Second line of address, if one exists (e.g. apartment number).
city | string | 
subnational | string | Subnational unit (i.e. state or province).
postal_code | string | 
postal_other | string | E.g. last four digits in a zip-plus-four.
country | [string enum](#post-cardsavr_address-1)* | 
is_primary | boolean | Indicates if this is the primary address of this cardholder, as a cardholder can be linked to multiple addresses.
first_name | string | 
last_name | string | 
email | string | 
phone_number | string | 

See [address response parameters](#response-cardsavr_address).


## Delete address

```shell
curl -X DELETE
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/cardsavr_addresses/485193468
```

```javascript
await session.deleteAddress(undefined);
```

```csharp
CardSavrResponse<Address> address = await http.DeleteAddressAsync(undefined);
```

```java
JsonValue address = session.delete("/cardsavr_addresses", undefined, null);
```

### Path

DELETE /cardsavr_addresses/{id}

### Description

Delete a address and purge its [related items](#cascading-delete).  An id is required on every delete request.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.


See [address response parameters](#response-cardsavr_address).


# Bins
A Bank Identification Number (BIN) object represents a BIN used by a financial institution in the CardSavr API. They are linked to cards and FIs and used for reporting purposes.
## Get bin

```javascript
const bins = await session.getBins(245003197,{"sort":"id","is_descending":true,"page":1, "page_length":25,{'x-cardsavr-hydration':JSON.stringify(["financial_institution"])});
```

```csharp
Paging paging = new Paging() { PageLength = 100, IsDescending = true, Page = 1, Sort = "id" };
HttpRequestHeaders headers = new HttpRequestMessage().Headers;
string[] array = { "cardholder","merchant_site","cardsavr_card" };
var json = JsonConvert.SerializeObject(array);
headers.Add("x-cardsavr-hydration", json);
var query = new {ids = 1};
QueryDef qd = new QueryDef(query);
CardSavrResponse<Bins> bins = await session.GetBinsAsync(qd,paging,headers);
```

```java
Headers headers = session.createHeaders();
headers.paging = Json.createObjectBuilder().add("page", 1).add("page_length", 5).add("is_descending", true).add("sort", "id").build();
headers.hydration = {'x-cardsavr-hydration':JSON.stringify(["financial_institution"])}
JsonArray response = (JsonArray)session.get(245003197, null, headers);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 245003197,
  "custom_data": {
    "gHzLFGFrwToI": "y]S",
    "CltNpnNGebCI": 1,
    "ygvnDtHPcLFM": false
  },
  "created_on": "1996-03-26T22:56:33.396Z",
  "last_updated_on": "1997-06-03T17:59:13.390Z",
  "financial_institution": {
    "id": 1443639369,
    "name": "LWuNnJADfnOOvfzviewmTKBVSbCDjqsNOoHMKjdqALPkYitqoDNjerDigIaxmly",
    "description": "pNrIjvLXkIKMQNVrmwSlFTjb",
    "lookup_key": "RClkBketoWpYSFuhxPlYzDQZMSAHCwmNJxwvHBXwPaGzASoNZUQmqtMCVOYQauc",
    "alternate_lookup_key": "qGMCZglUqPqYntdNatumsCcacDMneSrFnkyTdqHNQXykgPwuBrAYFIHxvmwxAdn",
    "active": true,
    "last_activity": "1990-03-30T21:44:13.926Z",
    "created_on": "2015-08-07T11:51:32.590Z",
    "last_updated_on": "1996-10-05T01:12:29.642Z"
  },
  "bank_identification_number": "88323510"
}
```

### Path

GET /cardsavr_bins **(batch)** or GET /cardsavr_bins/:id **(singular)**

### Description

Returns the bin specified by the provided ID

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

#### Batch GET requests

**Batch requests** return the first page of all viewable bins, filtered by any [query filters](#get-filters) (see list of possible parameters below) listed in the path.


### Filter parameters
- ids / id (in path)
- financial_institution_id
- bank_identification_numbers
- created_on_min / created_on_max
- last_updated_on_min / last_updated_on_max

**Example batch GET request path:**<br>`/cardsavr_bins?ids=1,2`

#### Singular GET requests

**Singular requests** only return the bin matching the id provided in the path.

**Example GET request path:**<br>`/cardsavr_bins/245003197`

### <a name="response-cardsavr_bin"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number (pk) | Unique ID of this BIN.
financial_institution_id | number (fk) [financial institutions](#financial-institutions) | ID of financial institution that this Bank Identification Number belongs to.
custom_data | object | Custom data (e.g. brand, type) that can be added according to FI need.
created_on | date | Date this site was created on
last_updated_on | date | Date this site was last updated on
bank_identification_number | string | 

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

## Create bin

```javascript
const bin = await session.createBin({
  "financial_institution_id": 680459582,
  "bank_identification_number": "88323510",
  "custom_data": {
    "gHzLFGFrwToI": "y]S",
    "CltNpnNGebCI": 1,
    "ygvnDtHPcLFM": false
  }
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "financial_institution_id", 680459582 },
	{ "bank_identification_number", "88323510" }
};

CardSavrResponse<Bin> bin = await http.CreateBinAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("financial_institution_id", 680459582 )
	.add("bank_identification_number", "88323510" )
	.build();
JsonValue bin = session.post("/cardsavr_bins", body, null, null);
```

```shell
curl -d "{\"financial_institution_id\":680459582,\"bank_identification_number\":\"88323510\",\"custom_data\":{\"gHzLFGFrwToI\":\"y]S\",\"CltNpnNGebCI\":1,\"ygvnDtHPcLFM\":false}}"
-X POST -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/cardsavr_bins/
```

### Path

POST /cardsavr_bins

### Description

Create a bin and return the created object.

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

### Body parameters

Parameter | Type | Required | Description
-------- | ---- | --------- | ----------
financial_institution_id | number | yes | ID of financial institution that this Bank Identification Number belongs to.
bank_identification_number | string | yes | 
custom_data | object | no | Custom data (e.g. brand, type) that can be added according to FI need.

See [bin response attributes](#response-cardsavr_bin).


## Update bin

```javascript
const bin = await session.updateBin(1,{
  "financial_institution_id": 1776071308,
  "custom_data": {
    "BJgvyUSHkBJR": "WF_r=yow&44!@RIIM~^",
    "YexyTVKQyUnd": 87,
    "xgmHPtgTENTV": true
  }
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "financial_institution_id", 1776071308 }
};

CardSavrResponse<Bin> bin = await http.UpdateBinAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("financial_institution_id", 1776071308 )
	.build();
JsonValue bin = session.put("/cardsavr_bins", body, null, null);
```

```shell
curl -d "{\"financial_institution_id\":1776071308,\"custom_data\":{\"BJgvyUSHkBJR\":\"WF_r=yow&44!@RIIM~^\",\"YexyTVKQyUnd\":87,\"xgmHPtgTENTV\":true}}"
-X PUT -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/cardsavr_bins/245003197
```

### Path

PUT /cardsavr_bins OR /cardsavr_bins/{id}

### Description

Update a bin and return the updated object.  An id is required on every update request.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

### Body parameters

Parameter | Type | Description 
-------- | ---- | ---------
financial_institution_id | number | ID of financial institution that this Bank Identification Number belongs to.
custom_data | object | Custom data (e.g. brand, type) that can be added according to FI need.

See [bin response parameters](#response-cardsavr_bin).


## Delete bin

```shell
curl -X DELETE
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/cardsavr_bins/245003197
```

```javascript
await session.deleteBin(undefined);
```

```csharp
CardSavrResponse<Bin> bin = await http.DeleteBinAsync(undefined);
```

```java
JsonValue bin = session.delete("/cardsavr_bins", undefined, null);
```

### Path

DELETE /cardsavr_bins/{id}

### Description

Delete a bin and purge its [related items](#cascading-delete).  An id is required on every delete request.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.


See [bin response parameters](#response-cardsavr_bin).


# Card Placement Results
Card Placement results are a flatted version of the jobs and its publily available meta data. Although sensitive data like the PAN and account creds are not available, all the details of the job are captured here for future reference after the corresponding entities may have been deleted.
## Get card placement result

```javascript
const cardplacementresults = await session.getCardPlacementResults(746989041,{"sort":"id","is_descending":true,"page":1, "page_length":25,{'x-cardsavr-hydration':JSON.stringify(["financial_institution","merchant_site","cardsavr_bin"])});
```

```csharp
Paging paging = new Paging() { PageLength = 100, IsDescending = true, Page = 1, Sort = "id" };
HttpRequestHeaders headers = new HttpRequestMessage().Headers;
string[] array = { "cardholder","merchant_site","cardsavr_card" };
var json = JsonConvert.SerializeObject(array);
headers.Add("x-cardsavr-hydration", json);
var query = new {ids = 1};
QueryDef qd = new QueryDef(query);
CardSavrResponse<CardPlacementResults> cardplacementresults = await session.GetCardPlacementResultsAsync(qd,paging,headers);
```

```java
Headers headers = session.createHeaders();
headers.paging = Json.createObjectBuilder().add("page", 1).add("page_length", 5).add("is_descending", true).add("sort", "id").build();
headers.hydration = {'x-cardsavr-hydration':JSON.stringify(["financial_institution","merchant_site","cardsavr_bin"])}
JsonArray response = (JsonArray)session.get(746989041, null, headers);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 746989041,
  "merchant_site_hostname": "ZKpwKCpIirodTstLiMqFnSUimJABMASGlrmFCivjEpxWvXOXOWdculYFYDKVpNjpFIwhxoVAquYfuiqhvmxktKgtDXUTsxmoUiPbPbFcMnbNzsFDkibTpfGlIfmCSKqsXefIWIVOGdLUacNcoFJnCEBXLopeOxAiWCkOxkCTsjFVvapRsynugfknzuaAEIfNqqmmmOpUmmajoVrXzzqaSTFAxrTnVRClFjLfAIBxCdRkXOUfUqqOkhPwuugign",
  "meta_key": "MB9810411",
  "fi_name": "VyyUMLzqFpKOmGaCSFFrwJjQUjXzwuCiWYNTxckBnLnNvBCjGGuERtMZeoWLQxQ",
  "bank_identification_number": "53945145",
  "cuid": "FIScGZgzMZNeMCoGFTsltNdrbamsocc",
  "par": "jhssWsbROiJhvuUzDCgcbRyZmRDhN",
  "card_customer_key": "LpaZrWlumWEaYMcASExoljzVJfhzIFej",
  "account_customer_key": "Ioxh",
  "status": "SUCCESSFUL",
  "status_message": "Successful",
  "termination_type": "BILLABLE",
  "custom_data": {
    "xwSMrpYRmpQf": "/#1CQJgzI@q_#iYj*L7",
    "EdfGUAIWTBjm": 90,
    "fxfuiuJzHFdR": false
  },
  "source": {
    "type": "promo",
    "category": "activation",
    "sub_category": "@M==",
    "device": "desktop web",
    "integration": "CU3_CL"
  },
  "time_elapsed": 606944656,
  "first_6": "yWyQrvMDfLLAQauCbWVfBWxjFlpbjFUZ",
  "first_7": "bUCOEDQvHKvKHEnXPyvvjRYFexFcLyOY",
  "first_8": "XbFTTamnSgRRUyECljurfZUTXNtGsSwz",
  "card_type": "Visa",
  "trace": "lucLcxThgZxfxuGb",
  "agent_session_id": "scPcvCzmWdDAskHbhqpnZcL",
  "email_sent": false,
  "account_linked_on": "2023-06-20T00:49:46.251Z",
  "job_ready_on": "2023-04-13T14:49:56.830Z",
  "job_created_on": "2017-11-21T11:23:19.179Z",
  "completed_on": "1989-06-26T15:52:45.267Z",
  "created_on": "1988-12-26T18:03:47.003Z",
  "last_updated_on": "1979-07-31T08:53:57.710Z",
  "financial_institution": {
    "id": 556415579,
    "name": "bCBrLuQtAwLNRtIYuOWScyPGxrPfxEoJzeTfUArjKXObLIfglyKdvFkjJNiIjGb",
    "description": "NxATbXxpIvSZ",
    "lookup_key": "nmVrOVPbBqJxSbODetKiBUcNZiXptqHcdqPVAZgnPIpbWtDXHbsokHgmFSjLKri",
    "alternate_lookup_key": "bWNGaYIuQopNbLfNmvLWIKJnYeJLmquMQmrjKKBEFkZIqMsZRFWiBAmreHtlNsN",
    "active": true,
    "last_activity": "2022-04-27T00:51:22.768Z",
    "created_on": "2015-04-02T10:20:35.457Z",
    "last_updated_on": "1979-06-22T02:05:09.624Z"
  },
  "merchant_site": {
    "id": 426187207,
    "name": "Amazon",
    "note": "vW",
    "host": "amazon.com",
    "tags": [
      "dL1",
      30,
      "B[fgXV_Z)p***e=!FHZ8u4F}h&"
    ],
    "interface_type": "dcs_loopback",
    "job_type": "CARD_PLACEMENT",
    "required_form_fields": [
      "email",
      "phone_number",
      "card_data",
      "cvv",
      "billing_address",
      "postal_code"
    ],
    "images": [
      {
        "url": "https://d1t7g1oas7m24a.cloudfront.net/tiles/dollarshaveclub.com?width=128&version=21f917315911eec1b1705bc7784ce861579cff2b",
        "width": 128,
        "grayscale": false
      },
      {
        "url": "https://d1t7g1oas7m24a.cloudfront.net/tiles/dollarshaveclub.com?width=32&version=21f917315911eec1b1705bc7784ce861579cff2b",
        "width": 32,
        "grayscale": false
      }
    ],
    "account_link": [
      {
        "key_name": "username",
        "label": "Username",
        "type": "initial_account_link"
      },
      {
        "key_name": "password",
        "label": "Password",
        "type": "initial_account_link",
        "secret": true
      },
      {
        "key_name": "otp",
        "label": "One Time Passcode",
        "type": ""
      }
    ],
    "messages": {
      "mfa_label": "Additional information required, this code may be sent to your phone or email address.",
      "additional_info_message": "",
      "auth_message": "Linking account."
    },
    "login_page": "https://www.merchantsite.com/login",
    "forgot_password_page": "https://www.merchantsite.com/forgot_password",
    "credit_card_page": "https://www.merchantsite.com/credit_card",
    "wallet_page": "jLZKwSObbEeUftXX",
    "merchant_sso_group": "EOOg",
    "tier": 757852295
  },
  "cardsavr_bin": {
    "id": 69501061,
    "custom_data": {
      "ZiSOfEHCmLyw": "W02D8gM",
      "scNRcibYzLcw": 12,
      "BQIngkGYlswW": false
    },
    "created_on": "2018-06-28T01:36:46.009Z",
    "last_updated_on": "1993-05-24T13:12:38.159Z",
    "bank_identification_number": "83035535"
  },
  "place_card_on_single_site_job_id": 343592123
}
```

### Path

GET /card_placement_results **(batch)** or GET /card_placement_results/:id **(singular)**

### Description

Returns the card placement result specified by the provided ID

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

#### Batch GET requests

**Batch requests** return the first page of all viewable card placement results, filtered by any [query filters](#get-filters) (see list of possible parameters below) listed in the path.


### Filter parameters
- ids / id (in path)
- merchant_site_hostnames
- merchant_site_hostname
- meta_key
- fi_name
- bank_identification_numbers
- cuids
- pars
- card_customer_keys
- account_customer_keys
- statuses
- status
- termination_type
- termination_types_include / termination_types_exclude
- first_6
- first_7
- first_8
- last_4
- types
- type
- place_card_on_single_site_job_ids
- financial_institution_id
- merchant_site_ids
- agent_session_id
- email_sent
- account_linked_on_min / account_linked_on_max
- job_ready_on_min / job_ready_on_max
- job_created_on_min / job_created_on_max
- completed_on_min / completed_on_max
- created_on_min / created_on_max
- last_updated_on_min / last_updated_on_max

**Example batch GET request path:**<br>`/card_placement_results?ids=1,2`

#### Singular GET requests

**Singular requests** only return the card placement result matching the id provided in the path.

**Example GET request path:**<br>`/card_placement_results/746989041`

### <a name="response-card_placement_result"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number (pk) | Unique ID of this card placement result.
merchant_site_hostname | string | 
meta_key | string | Key used for billing record identification; automatically generated during card creation.
fi_name | string | 
bank_identification_number | string | 
cuid | string | External unique ID for cardholder--can be account_id, email address, phone number, etc.  A random number will be gnenerated if not provided.
par | string | 
card_customer_key | string | Unique customer reference for this card. A random number will be generated and returned if not provided
account_customer_key | string | An external reference to a merchant site for a specific cardholder.  A key of merchant host and cuid will be used if none provided. The default can potentially violate a constraint with two accounts of the same merchant site.
status | string | Status of job (when it terminated).
status_message | string | Human readable representation of the job's status.
termination_type | string | Final termination status of a job. (BILLABLE, SITE_INTERACTION_FAILURE, USER_DATA_FAILURE, PROCESS FAILURE)
custom_data | object | 
source | object | Information that identifies how the cardholder was acquired. Parameters supported are type, category, device and sub_category.
time_elapsed | number | 
first_6 | string | First six digits of card number.
first_7 | string | First seven digits of card number.
first_8 | string | First eight digits of card number.
card_type | string | Type of card (e.g. Visa), automatically filled in by CardSavr.
trace | string | The trace key follows jobs as they are processed from beginning to end.  This helps with debugging the logs.
financial_institution_id | number (fk) [financial institutions](#financial-institutions) | 
merchant_site_id | number (fk) [merchant sites](#merchant-sites) | 
agent_session_id | string | 
email_sent | boolean | 
account_linked_on | date | Timestamp from when the account for this job is linked -- this could use persistent or user provided credentials
job_ready_on | date | Timestamp from when initial credentials have been set on the account for the job.
job_created_on | date | Timestamp from when the job was created.
completed_on | date | 
created_on | date | Date this job result was created on
last_updated_on | date | Date this job result was last updated on
place_card_on_single_site_job_id | number | 

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

# Card Lists
A list of cards that can be uploaded and stored for future use.
## Get card list

```javascript
const cardlists = await session.getCardLists(1536441587,{"sort":"id","is_descending":true,"page":1, "page_length":25,{'x-cardsavr-hydration':JSON.stringify(["financial_institution"])});
```

```csharp
Paging paging = new Paging() { PageLength = 100, IsDescending = true, Page = 1, Sort = "id" };
HttpRequestHeaders headers = new HttpRequestMessage().Headers;
string[] array = { "cardholder","merchant_site","cardsavr_card" };
var json = JsonConvert.SerializeObject(array);
headers.Add("x-cardsavr-hydration", json);
var query = new {ids = 1};
QueryDef qd = new QueryDef(query);
CardSavrResponse<CardLists> cardlists = await session.GetCardListsAsync(qd,paging,headers);
```

```java
Headers headers = session.createHeaders();
headers.paging = Json.createObjectBuilder().add("page", 1).add("page_length", 5).add("is_descending", true).add("sort", "id").build();
headers.hydration = {'x-cardsavr-hydration':JSON.stringify(["financial_institution"])}
JsonArray response = (JsonArray)session.get(1536441587, null, headers);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 1536441587,
  "name": "JTujMOGZveAejbOxumGpmysiEqecqbYtywzWrSKoMrTDJFKAIBycIRNGjBBzxaRJKfLcyYXvNJNwruggqaYfIklnKvUhekIycwHHZXCIavULkXVZbCgMhUlhiHLjJbZZrMFMWiUERaJYvqSSJlUbPXBDEbvXjJfDVnhXOseQOrDRCYABteXvKhiiKLTIJXADSgFaIRQfkkyUToxlLgxwETpeHWfvnCzKjPpbRKVugKaUuCJJimWWcnnBwSzyxA",
  "custom_data": {
    "vBgPddSByutf": "PNtwK4!,e(s2+4RxMH&]/F",
    "pBNKtvuQlEMK": 49,
    "OGiCgNSxfKch": true
  },
  "created_on": "1995-01-30T01:36:56.037Z",
  "last_updated_on": "2004-12-14T22:57:00.102Z",
  "financial_institution": {
    "id": 814518508,
    "name": "PmekbzZCzWgWrtVkxVygRgpJubJstoBQCHcdBnVCDeCmyanwxVrJJRvlRtUrvQA",
    "description": "kMTgnpxmvrlndXmQnl",
    "lookup_key": "mWZAzeJCcOvGgaZkCFegbAeRdHULyFLgbsCVAWVwwuGZXBDqrZgUSEbatCjnQga",
    "alternate_lookup_key": "DyBNHiPwdYOxsTiUzXnABrEPfkggyQdRZtsrvOeMOPBrMnIsSkmkqshcZlSzOpR",
    "active": false,
    "last_activity": "1978-01-07T20:25:54.410Z",
    "created_on": "2024-05-05T23:36:31.114Z",
    "last_updated_on": "2010-12-27T08:06:16.744Z"
  }
}
```

### Path

GET /card_lists **(batch)** or GET /card_lists/:id **(singular)**

### Description

Returns the card list specified by the provided ID

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

#### Batch GET requests

**Batch requests** return the first page of all viewable card lists, filtered by any [query filters](#get-filters) (see list of possible parameters below) listed in the path.


### Filter parameters
- ids / id (in path)
- financial_institution_id
- created_on_min / created_on_max
- last_updated_on_min / last_updated_on_max

**Example batch GET request path:**<br>`/card_lists?ids=1,2`

#### Singular GET requests

**Singular requests** only return the card list matching the id provided in the path.

**Example GET request path:**<br>`/card_lists/1536441587`

### <a name="response-card_list"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number (pk) | Unique ID of this list.
name | string | 
custom_data | object | Additional data that can be added to the card list if necessary.
created_on | date | Date this list was created on
last_updated_on | date | Date this list was last updated on
financial_institution_id | number (fk) [financial institutions](#financial-institutions) | 

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

## Create card list

```javascript
const cardlist = await session.createCardList({
  "name": "JTujMOGZveAejbOxumGpmysiEqecqbYtywzWrSKoMrTDJFKAIBycIRNGjBBzxaRJKfLcyYXvNJNwruggqaYfIklnKvUhekIycwHHZXCIavULkXVZbCgMhUlhiHLjJbZZrMFMWiUERaJYvqSSJlUbPXBDEbvXjJfDVnhXOseQOrDRCYABteXvKhiiKLTIJXADSgFaIRQfkkyUToxlLgxwETpeHWfvnCzKjPpbRKVugKaUuCJJimWWcnnBwSzyxA",
  "financial_institution_id": 491694546,
  "custom_data": {
    "vBgPddSByutf": "PNtwK4!,e(s2+4RxMH&]/F",
    "pBNKtvuQlEMK": 49,
    "OGiCgNSxfKch": true
  }
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "name", "JTujMOGZveAejbOxumGpmysiEqecqbYtywzWrSKoMrTDJFKAIBycIRNGjBBzxaRJKfLcyYXvNJNwruggqaYfIklnKvUhekIycwHHZXCIavULkXVZbCgMhUlhiHLjJbZZrMFMWiUERaJYvqSSJlUbPXBDEbvXjJfDVnhXOseQOrDRCYABteXvKhiiKLTIJXADSgFaIRQfkkyUToxlLgxwETpeHWfvnCzKjPpbRKVugKaUuCJJimWWcnnBwSzyxA" },
	{ "financial_institution_id", 491694546 }
};

CardSavrResponse<CardList> cardlist = await http.CreateCardListAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("name", "JTujMOGZveAejbOxumGpmysiEqecqbYtywzWrSKoMrTDJFKAIBycIRNGjBBzxaRJKfLcyYXvNJNwruggqaYfIklnKvUhekIycwHHZXCIavULkXVZbCgMhUlhiHLjJbZZrMFMWiUERaJYvqSSJlUbPXBDEbvXjJfDVnhXOseQOrDRCYABteXvKhiiKLTIJXADSgFaIRQfkkyUToxlLgxwETpeHWfvnCzKjPpbRKVugKaUuCJJimWWcnnBwSzyxA" )
	.add("financial_institution_id", 491694546 )
	.build();
JsonValue cardlist = session.post("/card_lists", body, null, null);
```

```shell
curl -d "{\"name\":\"JTujMOGZveAejbOxumGpmysiEqecqbYtywzWrSKoMrTDJFKAIBycIRNGjBBzxaRJKfLcyYXvNJNwruggqaYfIklnKvUhekIycwHHZXCIavULkXVZbCgMhUlhiHLjJbZZrMFMWiUERaJYvqSSJlUbPXBDEbvXjJfDVnhXOseQOrDRCYABteXvKhiiKLTIJXADSgFaIRQfkkyUToxlLgxwETpeHWfvnCzKjPpbRKVugKaUuCJJimWWcnnBwSzyxA\",\"financial_institution_id\":491694546,\"custom_data\":{\"vBgPddSByutf\":\"PNtwK4!,e(s2+4RxMH&]/F\",\"pBNKtvuQlEMK\":49,\"OGiCgNSxfKch\":true}}"
-X POST -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/card_lists/
```

### Path

POST /card_lists

### Description

Create a card list and return the created object.

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

### Body parameters

Parameter | Type | Required | Description
-------- | ---- | --------- | ----------
name | string | yes | 
financial_institution_id | number | yes | 
custom_data | object | no | Additional data that can be added to the card list if necessary.

See [card list response attributes](#response-card_list).


## Update card list

```javascript
const cardlist = await session.updateCardList(1,{
  "name": "UgmtTOiVNcotqgWappQjjkTkbwCecghJGqmyRHUDOehxGpDKamwxdQrGxlxvhTYlfCtkIhOIvVcnruRFMbVoYAkVNgQuZgTAqNQSppeUgCELKWgrtVVXcfpyUDQeFlCrTOEjCntrNDadLrFjhgqgnyrUpNSEURuQruzrrlCDeTMJRbyoFCQQIWaTeDzaynHUxDdYctThVSalRHJDRGbxZhrWoTYyrsDwoQfqoFgxSpOggkbXMbgneUIKJlsuLs",
  "custom_data": {
    "pwLehCaMnMcX": "1_/d1r0Y6!7}p_QK_^N5UIy",
    "prVdFGHvsakH": 29,
    "IQOlciRUoLoO": true
  }
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "name", "UgmtTOiVNcotqgWappQjjkTkbwCecghJGqmyRHUDOehxGpDKamwxdQrGxlxvhTYlfCtkIhOIvVcnruRFMbVoYAkVNgQuZgTAqNQSppeUgCELKWgrtVVXcfpyUDQeFlCrTOEjCntrNDadLrFjhgqgnyrUpNSEURuQruzrrlCDeTMJRbyoFCQQIWaTeDzaynHUxDdYctThVSalRHJDRGbxZhrWoTYyrsDwoQfqoFgxSpOggkbXMbgneUIKJlsuLs" }
};

CardSavrResponse<CardList> cardlist = await http.UpdateCardListAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("name", "UgmtTOiVNcotqgWappQjjkTkbwCecghJGqmyRHUDOehxGpDKamwxdQrGxlxvhTYlfCtkIhOIvVcnruRFMbVoYAkVNgQuZgTAqNQSppeUgCELKWgrtVVXcfpyUDQeFlCrTOEjCntrNDadLrFjhgqgnyrUpNSEURuQruzrrlCDeTMJRbyoFCQQIWaTeDzaynHUxDdYctThVSalRHJDRGbxZhrWoTYyrsDwoQfqoFgxSpOggkbXMbgneUIKJlsuLs" )
	.build();
JsonValue cardlist = session.put("/card_lists", body, null, null);
```

```shell
curl -d "{\"name\":\"UgmtTOiVNcotqgWappQjjkTkbwCecghJGqmyRHUDOehxGpDKamwxdQrGxlxvhTYlfCtkIhOIvVcnruRFMbVoYAkVNgQuZgTAqNQSppeUgCELKWgrtVVXcfpyUDQeFlCrTOEjCntrNDadLrFjhgqgnyrUpNSEURuQruzrrlCDeTMJRbyoFCQQIWaTeDzaynHUxDdYctThVSalRHJDRGbxZhrWoTYyrsDwoQfqoFgxSpOggkbXMbgneUIKJlsuLs\",\"custom_data\":{\"pwLehCaMnMcX\":\"1_/d1r0Y6!7}p_QK_^N5UIy\",\"prVdFGHvsakH\":29,\"IQOlciRUoLoO\":true}}"
-X PUT -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/card_lists/1536441587
```

### Path

PUT /card_lists OR /card_lists/{id}

### Description

Update a card list and return the updated object.  An id is required on every update request.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

### Body parameters

Parameter | Type | Description 
-------- | ---- | ---------
name | string | 
custom_data | object | Additional data that can be added to the card list if necessary.

See [card list response parameters](#response-card_list).


## Delete card list

```shell
curl -X DELETE
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/card_lists/1536441587
```

```javascript
await session.deleteCardList(undefined);
```

```csharp
CardSavrResponse<CardList> cardlist = await http.DeleteCardListAsync(undefined);
```

```java
JsonValue cardlist = session.delete("/card_lists", undefined, null);
```

### Path

DELETE /card_lists/{id}

### Description

Delete a card list and purge its [related items](#cascading-delete).  An id is required on every delete request.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.


See [card list response parameters](#response-card_list).


# Card Links
Meta properties about a link that enables a cardholder to initiate a cardholder session with a specific card.
## Get card link

```javascript
const cardlinks = await session.getCardLinks(1895187881,{"sort":"id","is_descending":true,"page":1, "page_length":25,{'x-cardsavr-hydration':JSON.stringify(["card_list","cardsavr_card"])});
```

```csharp
Paging paging = new Paging() { PageLength = 100, IsDescending = true, Page = 1, Sort = "id" };
HttpRequestHeaders headers = new HttpRequestMessage().Headers;
string[] array = { "cardholder","merchant_site","cardsavr_card" };
var json = JsonConvert.SerializeObject(array);
headers.Add("x-cardsavr-hydration", json);
var query = new {ids = 1};
QueryDef qd = new QueryDef(query);
CardSavrResponse<CardLinks> cardlinks = await session.GetCardLinksAsync(qd,paging,headers);
```

```java
Headers headers = session.createHeaders();
headers.paging = Json.createObjectBuilder().add("page", 1).add("page_length", 5).add("is_descending", true).add("sort", "id").build();
headers.hydration = {'x-cardsavr-hydration':JSON.stringify(["card_list","cardsavr_card"])}
JsonArray response = (JsonArray)session.get(1895187881, null, headers);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 1895187881,
  "error": "This is an error",
  "custom_data": {
    "ygCaMZjLcmIa": ")8]3(YbHvkjI&Hh8w1iwV3~(K",
    "GVItpiIcANoX": 23,
    "QFkgAsBKpJaY": false
  },
  "created_on": "2018-04-23T15:17:52.908Z",
  "last_updated_on": "1995-06-01T05:35:55.149Z",
  "card_list": {
    "id": 811543121,
    "name": "HADMpDAzNvlvoeBkymGIXexZCTlQADAWSMjMQOEazjWICfdIFfrLEXkavTsItMkKaMVSFqQFUiXtRtVMrIWxqyVlBTCUffKtxdQwhYZfMKDnxkKnICHMILHmKraYgAejntUkxHIZqGOAxpNATNDkbueyzBRdgphoOBatxDmazBjLFYWeFJnzbbyCxlBqRmMLsyFSXXfHsUXLwvpaePlHloJxzCaPIAMUdMjoDCyHUJIyXtvMqAjknQVVXwCSsw",
    "custom_data": {
      "nwAPgHViLWhB": "Z/BwK",
      "kdNmnCMIpRJi": 85,
      "JjfDnxVZZFHx": true
    },
    "created_on": "1998-08-30T04:38:00.814Z",
    "last_updated_on": "2011-11-15T10:42:48.224Z"
  },
  "cardsavr_card": {
    "id": 807244379,
    "type": "American Express",
    "expiration_month": 12,
    "expiration_year": 24,
    "name_on_card": "Jane Smith",
    "last_4": "BLRP",
    "nickname": "Jane's VISA",
    "custom_data": {
      "IJmWZmtDpOrF": "V9[of1(]ay6tFS]EGoFF0J",
      "RcmJHuAGMJEb": 92,
      "SZvkLMysqFff": true
    },
    "created_on": "2022-04-10T21:48:07.873Z",
    "last_updated_on": "2009-09-21T00:37:43.541Z",
    "par": "TzujjmnyPjhXJljIuGfkKzMdJOcnQ",
    "customer_key": "haRpCsfniohUCvcAbpUNQWtc"
  }
}
```

### Path

GET /card_links **(batch)** or GET /card_links/:id **(singular)**

### Description

Returns the card link specified by the provided ID

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

#### Batch GET requests

**Batch requests** return the first page of all viewable card links, filtered by any [query filters](#get-filters) (see list of possible parameters below) listed in the path.


### Filter parameters
- ids / id (in path)
- card_list_id
- card_id
- created_on_min / created_on_max
- last_updated_on_min / last_updated_on_max

**Example batch GET request path:**<br>`/card_links?ids=1,2`

#### Singular GET requests

**Singular requests** only return the card link matching the id provided in the path.

**Example GET request path:**<br>`/card_links/1895187881`

### <a name="response-card_link"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number (pk) | Unique ID of this list.
error | string | 
custom_data | object | Additional data that can be added to the card list if necessary.
created_on | date | Date this link was created on
last_updated_on | date | Date this link was last updated on
card_list_id | number (fk) [card lists](#card-lists) | ID of the associated list.
card_id | number (fk) [cards](#cards) | Associated card_id for this link.

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

## Create card link

```javascript
const cardlink = await session.createCardLink({
  "card_list_id": 1621565878,
  "error": "This is an error",
  "card_id": 302556045,
  "custom_data": {
    "ygCaMZjLcmIa": ")8]3(YbHvkjI&Hh8w1iwV3~(K",
    "GVItpiIcANoX": 23,
    "QFkgAsBKpJaY": false
  }
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "card_list_id", 1621565878 },
	{ "error", "This is an error" },
	{ "card_id", 302556045 }
};

CardSavrResponse<CardLink> cardlink = await http.CreateCardLinkAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("card_list_id", 1621565878 )
	.add("error", "This is an error" )
	.add("card_id", 302556045 )
	.build();
JsonValue cardlink = session.post("/card_links", body, null, null);
```

```shell
curl -d "{\"card_list_id\":1621565878,\"error\":\"This is an error\",\"card_id\":302556045,\"custom_data\":{\"ygCaMZjLcmIa\":\")8]3(YbHvkjI&Hh8w1iwV3~(K\",\"GVItpiIcANoX\":23,\"QFkgAsBKpJaY\":false}}"
-X POST -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/card_links/
```

### Path

POST /card_links

### Description

Create a card link and return the created object.

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

### Body parameters

Parameter | Type | Required | Description
-------- | ---- | --------- | ----------
card_list_id | number | yes | ID of the associated list.
error | string | no | 
card_id | number | no | Associated card_id for this link.
custom_data | object | no | Additional data that can be added to the card list if necessary.

See [card link response attributes](#response-card_link).


## Update card link

```javascript
const cardlink = await session.updateCardLink(1,{
  "error": "This is an error",
  "custom_data": {
    "JLIcKVbULNCs": "0wv",
    "CaDWCeTFxxAJ": 72,
    "oJYDsADGTvzu": true
  }
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "error", "This is an error" }
};

CardSavrResponse<CardLink> cardlink = await http.UpdateCardLinkAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("error", "This is an error" )
	.build();
JsonValue cardlink = session.put("/card_links", body, null, null);
```

```shell
curl -d "{\"error\":\"This is an error\",\"custom_data\":{\"JLIcKVbULNCs\":\"0wv\",\"CaDWCeTFxxAJ\":72,\"oJYDsADGTvzu\":true}}"
-X PUT -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/card_links/1895187881
```

### Path

PUT /card_links OR /card_links/{id}

### Description

Update a card link and return the updated object.  An id is required on every update request.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

### Body parameters

Parameter | Type | Description 
-------- | ---- | ---------
error | string | 
custom_data | object | Additional data that can be added to the card list if necessary.

See [card link response parameters](#response-card_link).


## Delete card link

```shell
curl -X DELETE
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/card_links/1895187881
```

```javascript
await session.deleteCardLink(undefined);
```

```csharp
CardSavrResponse<CardLink> cardlink = await http.DeleteCardLinkAsync(undefined);
```

```java
JsonValue cardlink = session.delete("/card_links", undefined, null);
```

### Path

DELETE /card_links/{id}

### Description

Delete a card link and purge its [related items](#cascading-delete).  An id is required on every delete request.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.


See [card link response parameters](#response-card_link).


# Cardholder sessions
A record of information associated with the session of a carholder -- it terminates after explicit completion or 15 minutes of inactivity.
## Get cardholder session

```javascript
const cardholdersessions = await session.getCardholderSessions(1899508020,{"sort":"id","is_descending":true,"page":1, "page_length":25,{'x-cardsavr-hydration':JSON.stringify(["cardholder","financial_institution"])});
```

```csharp
Paging paging = new Paging() { PageLength = 100, IsDescending = true, Page = 1, Sort = "id" };
HttpRequestHeaders headers = new HttpRequestMessage().Headers;
string[] array = { "cardholder","merchant_site","cardsavr_card" };
var json = JsonConvert.SerializeObject(array);
headers.Add("x-cardsavr-hydration", json);
var query = new {ids = 1};
QueryDef qd = new QueryDef(query);
CardSavrResponse<CardholderSessions> cardholdersessions = await session.GetCardholderSessionsAsync(qd,paging,headers);
```

```java
Headers headers = session.createHeaders();
headers.paging = Json.createObjectBuilder().add("page", 1).add("page_length", 5).add("is_descending", true).add("sort", "id").build();
headers.hydration = {'x-cardsavr-hydration':JSON.stringify(["cardholder","financial_institution"])}
JsonArray response = (JsonArray)session.get(1899508020, null, headers);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 1899508020,
  "source": {
    "type": "alert",
    "category": "activation",
    "sub_category": "bR&(_@",
    "device": "mobile app",
    "integration": "CS"
  },
  "successful_jobs": 1023232358,
  "failed_jobs": 1326056501,
  "total_jobs": 2022286871,
  "financial_institution_lookup_key": "NzbNtAHDsXuULSXPPXUrUsJce",
  "clickstream": [
    {
      "lqCrXfiKjNmV": "k*",
      "FSOYGXMtfYwP": 77,
      "AdmHvOvcHfVT": true
    },
    {
      "hwoOmfgIWGOO": "*F0T*rO/3H/G8=hNWW%PU)V^s+l#+u(",
      "lKYwItjuWkFA": 61,
      "eYkBylcOIujC": true
    },
    {
      "IkGwtMbUPBvi": "le(",
      "jUCnRpwmrNFU": 80,
      "XUnZWhpYvurh": true
    }
  ],
  "closed_on": "2024-11-25T20:34:45.635Z",
  "custom_data": {
    "EvipljCOONEf": "cn@NkzrzLbVR[P6t",
    "UKpYMQUnpCoL": 3,
    "zWVUjRBLqetd": true
  },
  "created_on": "2008-11-09T08:18:09.743Z",
  "last_updated_on": "1995-03-29T15:54:23.502Z",
  "cardholder": {
    "id": 1335613178,
    "type": "persistent_nocreds",
    "first_name": "Jane",
    "last_name": "Smith",
    "email": "test_email@strivve.com",
    "meta_key": "vTeCTUuzAWrXApKgcdr",
    "webhook_url": "https://mywebhooks.com/this",
    "custom_data": {
      "bSRVogUDfuNG": "@u=Mm]UPD8}ZWNR!0E2#9/xMLTUX8#",
      "anBaNzaEnOXF": 62,
      "VhcUitRYiOdw": true
    },
    "created_on": "2002-08-12T13:56:36.219Z",
    "last_updated_on": "1983-06-23T10:16:42.286Z",
    "cuid": "KbLVu",
    "source": {
      "type": "alert",
      "category": "other",
      "sub_category": "II",
      "device": "mobile web",
      "integration": "CU2"
    }
  },
  "financial_institution": {
    "id": 251236523,
    "name": "GPwtSXIaZXxoAwYjtexgNGzaebAfiVIlLeJKLnUaptLrBKHdjxeMWWaVTBvSCpf",
    "description": "LqYHWANiFCmuv",
    "lookup_key": "PQOlCgSeuXzzJGfkxpETReRYxyFmcWLqBZbzYeqQHcjSWTIDPRMMoAlJUwCVKDZ",
    "alternate_lookup_key": "vRZhHpFvSnVCJHLSXaUDUcVeLMLLjSxREyqGrKrJfKNFLpKpOMZlWuaIxkrCmaG",
    "active": true,
    "last_activity": "1987-05-30T22:05:48.276Z",
    "created_on": "1991-03-11T08:20:58.389Z",
    "last_updated_on": "2008-04-22T18:16:04.980Z"
  },
  "cuid": "LbGCJNwbnxMrm"
}
```

### Path

GET /cardholder_sessions **(batch)** or GET /cardholder_sessions/:id **(singular)**

### Description

Returns the cardholder session specified by the provided ID

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

#### Batch GET requests

**Batch requests** return the first page of all viewable cardholder sessions, filtered by any [query filters](#get-filters) (see list of possible parameters below) listed in the path.


### Filter parameters
- ids / id (in path)
- cuid
- cardholder_id
- financial_institution_id
- financial_institution_lookup_key
- closed_on_min / closed_on_max
- created_on_min / created_on_max
- last_updated_on_min / last_updated_on_max

**Example batch GET request path:**<br>`/cardholder_sessions?ids=1,2`

#### Singular GET requests

**Singular requests** only return the cardholder session matching the id provided in the path.

**Example GET request path:**<br>`/cardholder_sessions/1899508020`

### <a name="response-cardholder_session"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number (pk) | Unique ID of this card placement result.
source | object | Information that identifies how the cardholder was acquired. Parameters supported are type, category, device and sub_category.
successful_jobs | number | 
failed_jobs | number | 
total_jobs | number | 
cardholder_id | number (fk) [cardholders](#cardholders) | 
financial_institution_id | number (fk) [financial institutions](#financial-institutions) | 
financial_institution_lookup_key | string | 
clickstream | array | Click stream events and their corresponding timestamps
closed_on | date | Timestamp at which this cardholder session was closed
custom_data | object | Additional data that can be added to the cardholder if needed.
created_on | date | Date this job result was created on
last_updated_on | date | Date this job result was last updated on
cuid | string | 

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).


## Upsert cardholder session

```javascript
const cardholdersession = await session.updateCardholderSession(1,{
  "source": {
    "type": "weblink",
    "category": "campaign",
    "sub_category": "g~dq{b",
    "device": "mobile app",
    "integration": "CU2"
  },
  "successful_jobs": 1383075187,
  "failed_jobs": 986444518,
  "total_jobs": 951484837,
  "clickstream": [
    {
      "ZFNnKogzuHSq": "Obk",
      "ZSKZVpWiRvHp": 75,
      "IKoTiiIfqYNC": false
    },
    {
      "drbHghppvwmb": "u&gRgqhb*AU-}V]#)+6^zWhY]/.",
      "PVhRitklsXAS": 67,
      "EzenVDXDKrNp": false
    },
    {
      "cKzPoJkjqXYZ": "nfT}!7-/7f}~}Yk#GF==/StLO!O2xhW",
      "lwegbVKxHAVg": 65,
      "VwmKCFKnTqyZ": true
    }
  ]
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "successful_jobs", 1383075187 },
	{ "failed_jobs", 986444518 },
	{ "total_jobs", 951484837 }
};

CardSavrResponse<CardholderSession> cardholdersession = await http.UpdateCardholderSessionAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("successful_jobs", 1383075187 )
	.add("failed_jobs", 986444518 )
	.add("total_jobs", 951484837 )
	.build();
JsonValue cardholdersession = session.put("/cardholder_sessions", body, null, null);
```

```shell
curl -d "{\"source\":{\"type\":\"weblink\",\"category\":\"campaign\",\"sub_category\":\"g~dq{b\",\"device\":\"mobile app\",\"integration\":\"CU2\"},\"successful_jobs\":1383075187,\"failed_jobs\":986444518,\"total_jobs\":951484837,\"clickstream\":[{\"ZFNnKogzuHSq\":\"Obk\",\"ZSKZVpWiRvHp\":75,\"IKoTiiIfqYNC\":false},{\"drbHghppvwmb\":\"u&gRgqhb*AU-}V]#)+6^zWhY]/.\",\"PVhRitklsXAS\":67,\"EzenVDXDKrNp\":false},{\"cKzPoJkjqXYZ\":\"nfT}!7-/7f}~}Yk#GF==/StLO!O2xhW\",\"lwegbVKxHAVg\":65,\"VwmKCFKnTqyZ\":true}]}"
-X PUT -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/cardholder_sessions/1899508020
```

### Path

PUT /cardholder_sessions OR /cardholder_sessions/{id}

### Description

Upsert can be used to either update a cardholder session, create a new cardholder session, or return an existing cardholder session.  Either an id or customer_key is required for upsert. The id (in path or body), along with an updated body, can be used to update an existing cardholder session; the customer_key (in body) can likewise be used to update a cardholder session, and can also be used to create a new cardholder session, if the customer_key does not match any existing cardholder sessions. If the id or customer_key provided corresponds to a pre-existing cardholder session and no updated information has been included in the body, the existing cardholder session will be returned.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

### Body parameters

Parameter | Type | Description 
-------- | ---- | ---------
source | object | Information that identifies how the cardholder was acquired. Parameters supported are type, category, device and sub_category.
successful_jobs | number | 
failed_jobs | number | 
total_jobs | number | 
clickstream | array | Click stream events and their corresponding timestamps

See [cardholder session response parameters](#response-cardholder_session).

# Cards
A card object contains information about a payment card for a specific cardholder. Card objects are used to populate payment information on merchant sites.
## Get card

```javascript
const cards = await session.getCards(1061970351,{"sort":"id","is_descending":true,"page":1, "page_length":25,{'x-cardsavr-hydration':JSON.stringify(["cardholder","cardsavr_address","cardsavr_bin"])});
```

```csharp
Paging paging = new Paging() { PageLength = 100, IsDescending = true, Page = 1, Sort = "id" };
HttpRequestHeaders headers = new HttpRequestMessage().Headers;
string[] array = { "cardholder","merchant_site","cardsavr_card" };
var json = JsonConvert.SerializeObject(array);
headers.Add("x-cardsavr-hydration", json);
var query = new {ids = 1};
QueryDef qd = new QueryDef(query);
CardSavrResponse<Cards> cards = await session.GetCardsAsync(qd,paging,headers);
```

```java
Headers headers = session.createHeaders();
headers.paging = Json.createObjectBuilder().add("page", 1).add("page_length", 5).add("is_descending", true).add("sort", "id").build();
headers.hydration = {'x-cardsavr-hydration':JSON.stringify(["cardholder","cardsavr_address","cardsavr_bin"])}
JsonArray response = (JsonArray)session.get(1061970351, null, headers);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 1061970351,
  "type": "American Express",
  "expiration_month": 12,
  "expiration_year": 24,
  "name_on_card": "Jane Smith",
  "last_4": "aUyP",
  "nickname": "Jane's VISA",
  "custom_data": {
    "oNgrtVFAKauZ": ".~yZIx#oiNVNB3%",
    "RkvemHIOgvxv": 57,
    "sRIoOOePRECt": false
  },
  "created_on": "2006-09-02T21:16:51.566Z",
  "last_updated_on": "1990-10-02T22:17:28.263Z",
  "cardholder": {
    "id": 1778815841,
    "type": "ephemeral",
    "first_name": "Jane",
    "last_name": "Smith",
    "email": "test_email@strivve.com",
    "meta_key": "lOPmFXwBjSXUOpAR",
    "webhook_url": "https://mywebhooks.com/this",
    "custom_data": {
      "YJZQPYEMiCHS": "UBg[z8liu@3oL2J{",
      "VqLvgUQynZVC": 74,
      "ZwdtclvqtlNU": false
    },
    "created_on": "2001-10-06T14:00:50.316Z",
    "last_updated_on": "2022-07-17T09:40:26.163Z",
    "cuid": "nhXIBiHDWnJQwSlCICOHTccWOZo",
    "source": {
      "type": "email",
      "category": "activation",
      "sub_category": "_Pos",
      "device": "mobile web",
      "integration": "CS"
    }
  },
  "cardsavr_address": {
    "id": 256183602,
    "address1": "yaczUKYNdjtgcprWZcNDTtmdRoyhGoGJaOYExsgzlPfdtljwVGoCQdPdWtQOHDwEZKqAjkeJHNJOMdLVDaikoktcOWVpQjOYNjL",
    "address2": "rzICvotRYzayelTcfmhDdmuoLdyFkgLQPtPLlqkdSlcItSLxszcXEHUmmoLdrnIxawiFAjnGMLVQKVzjpOLRKCSONFYVKghXTCb",
    "city": "Seattle",
    "subnational": "WA",
    "postal_code": "98177",
    "postal_other": "98177-0124",
    "country": "USA",
    "is_primary": true,
    "first_name": "Jane",
    "last_name": "Smith",
    "email": "WTXytuEnxnGS@KksGDC.EMs",
    "phone_number": "2065555555",
    "created_on": "1990-12-06T12:04:01.050Z",
    "last_updated_on": "2018-09-26T03:50:27.417Z"
  },
  "cardsavr_bin": {
    "id": 54782207,
    "custom_data": {
      "yJFYaiXlEOkS": "+.!2{oq",
      "ceWJhFGEddMa": 59,
      "IScPHorWQAtY": true
    },
    "created_on": "2006-04-11T04:19:49.020Z",
    "last_updated_on": "1995-01-13T15:40:55.558Z",
    "bank_identification_number": "24401281"
  },
  "par": "NvzgeTDIzCgfYdaRgSBXxmKhvAZAe",
  "customer_key": "Mvhunz"
}
```

### Path

GET /cardsavr_cards **(batch)** or GET /cardsavr_cards/:id **(singular)**

### Description

Returns the card specified by the provided ID

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

#### Batch GET requests

**Batch requests** return the first page of all viewable cards, filtered by any [query filters](#get-filters) (see list of possible parameters below) listed in the path.


### Filter parameters
- ids / id (in path)
- cardholder_ids
- address_ids
- bin_ids
- pars
- customer_keys
- types
- type
- last_4
- nickname
- created_on_min / created_on_max
- last_updated_on_min / last_updated_on_max

**Example batch GET request path:**<br>`/cardsavr_cards?ids=1,2`

#### Singular GET requests

**Singular requests** only return the card matching the id provided in the path.

**Example GET request path:**<br>`/cardsavr_cards/1061970351`

### <a name="response-cardsavr_card"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number (pk) | Unique ID of this card.
address_id | number (fk) [addresses](#addresses) | ID of address associated with this card.
bin_id | number (fk) [bins](#bins) | ID of BIN associated with this card.
type | string | Type of card (e.g. Visa), automatically filled in by CardSavr.
expiration_month | string | 
expiration_year | string | 
name_on_card | string | 
last_4 | string | Last four digits of PAN.
nickname | string | 
custom_data | object | Meta-data that can be added to the card if needed.
created_on | date | Date this site was created on
last_updated_on | date | Date this site was last updated on
cardholder_id | number (fk) [cardholders](#cardholders) | ID of cardholder associated with this card.
par | string | Unique Personal Account Reference number for this card, to be used for card lookup. Generated automatically from PAN, expiration date, and username if using the SDK.
customer_key | string | Unique customer reference for this card. A random number will be generated and returned if not provided

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

## Create card

```javascript
const card = await session.createCard({
  "cardholder_id": 1931393826,
  "address_id": 258029205,
  "bin_id": 1743484985,
  "par": "NvzgeTDIzCgfYdaRgSBXxmKhvAZAe",
  "customer_key": "Mvhunz",
  "pan": "4111111111111111",
  "cvv": "111",
  "expiration_month": 12,
  "expiration_year": 24,
  "name_on_card": "Jane Smith",
  "nickname": "Jane's VISA",
  "custom_data": {
    "oNgrtVFAKauZ": ".~yZIx#oiNVNB3%",
    "RkvemHIOgvxv": 57,
    "sRIoOOePRECt": false
  }
}, CARDHOLDER_SAFE_KEY);
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "cardholder_id", 1931393826 },
	{ "address_id", 258029205 },
	{ "bin_id", 1743484985 },
	{ "par", "NvzgeTDIzCgfYdaRgSBXxmKhvAZAe" },
	{ "customer_key", "Mvhunz" },
	{ "pan", "4111111111111111" },
	{ "cvv", "111" },
	{ "expiration_month", 12 },
	{ "expiration_year", 24 },
	{ "name_on_card", "Jane Smith" },
	{ "nickname", "Jane's VISA" }
};

CardSavrResponse<Card> card = await http.CreateCardAsync(body, CARDHOLDER_SAFE_KEY);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("cardholder_id", 1931393826 )
	.add("address_id", 258029205 )
	.add("bin_id", 1743484985 )
	.add("par", "NvzgeTDIzCgfYdaRgSBXxmKhvAZAe" )
	.add("customer_key", "Mvhunz" )
	.add("pan", "4111111111111111" )
	.add("cvv", "111" )
	.add("expiration_month", 12 )
	.add("expiration_year", 24 )
	.add("name_on_card", "Jane Smith" )
	.add("nickname", "Jane's VISA" )
	.build();
JsonValue card = session.post("/cardsavr_cards", body, null, null);
```

```shell
curl -d "{\"cardholder_id\":1931393826,\"address_id\":258029205,\"bin_id\":1743484985,\"par\":\"NvzgeTDIzCgfYdaRgSBXxmKhvAZAe\",\"customer_key\":\"Mvhunz\",\"pan\":\"4111111111111111\",\"cvv\":\"111\",\"expiration_month\":12,\"expiration_year\":24,\"name_on_card\":\"Jane Smith\",\"nickname\":\"Jane's VISA\",\"custom_data\":{\"oNgrtVFAKauZ\":\".~yZIx#oiNVNB3%\",\"RkvemHIOgvxv\":57,\"sRIoOOePRECt\":false}}"
-X POST -H "Content-Type: application/json"
-H "x-cardsavr-cardholder-safe-key: CARDHOLDER_SAFE_KEY"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/cardsavr_cards/
```

### Path

POST /cardsavr_cards

### Description

Create a card and return the created object.

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.



<aside class="notice"><a href=#request-hydration-on-post>Request hydration</a> can be used on this endpoint. This allows you to create a new card and all referential entities in a single POST request.
</aside>

### Body parameters

Parameter | Type | Required | Description
-------- | ---- | --------- | ----------
cardholder_id | number | yes | ID of cardholder associated with this card.
address_id | number | no | ID of address associated with this card.
bin_id | number | no | ID of BIN associated with this card.
par | string | no | Unique Personal Account Reference number for this card, to be used for card lookup. Generated automatically from PAN, expiration date, and username if using the SDK.
customer_key | string | yes | Unique customer reference for this card. A random number will be generated and returned if not provided
pan | string | yes | Personal Account Number (PAN) of this card.
cvv | string | no | 
expiration_month | [string enum](#post-cardsavr_card-2)** | yes | 
expiration_year | string | yes | 
name_on_card | string | yes | 
nickname | string | yes | 
custom_data | object | no | Meta-data that can be added to the card if needed.

See [card response attributes](#response-cardsavr_card).

#### <a name="post-cardsavr_card-1"></a>string enum*
- Visa
- Mastercard
- American Express
- Unknown Type

#### <a name="post-cardsavr_card-2"></a>string enum**
- 01
- 02
- 03
- 04
- 05
- 06
- 07
- 08
- 09
- 10
- 11
- 12

<aside class="notice">Update calls to /cardsavr_cards require the cardholder's personal cardholder_safe_key header to encrypt and save the pan and cvv when Strivve does not manage keys for a customer (this is an environment setting). The safe keys are also not required if updating non-safe user properties.</aside>

## Upsert card

```javascript
const card = await session.updateCard(1,{
  "address_id": 1690088502,
  "bin_id": 1673463854,
  "cvv": "111",
  "expiration_month": 12,
  "expiration_year": 24,
  "name_on_card": "Jane Smith",
  "nickname": "Jane's VISA",
  "custom_data": {
    "LPiaVmoPaOeb": "{}",
    "nkqHjvKoZzLo": 4,
    "xIaHNrcVLNXX": true
  },
  "pan": "4111111111111111"
}, CARDHOLDER_SAFE_KEY);
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "address_id", 1690088502 },
	{ "bin_id", 1673463854 },
	{ "cvv", "111" },
	{ "expiration_month", 12 },
	{ "expiration_year", 24 },
	{ "name_on_card", "Jane Smith" },
	{ "nickname", "Jane's VISA" },
	{ "pan", "4111111111111111" }
};

CardSavrResponse<Card> card = await http.UpdateCardAsync(body, CARDHOLDER_SAFE_KEY);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("address_id", 1690088502 )
	.add("bin_id", 1673463854 )
	.add("cvv", "111" )
	.add("expiration_month", 12 )
	.add("expiration_year", 24 )
	.add("name_on_card", "Jane Smith" )
	.add("nickname", "Jane's VISA" )
	.add("pan", "4111111111111111" )
	.build();
JsonValue card = session.put("/cardsavr_cards", body, null, null);
```

```shell
curl -d "{\"address_id\":1690088502,\"bin_id\":1673463854,\"cvv\":\"111\",\"expiration_month\":12,\"expiration_year\":24,\"name_on_card\":\"Jane Smith\",\"nickname\":\"Jane's VISA\",\"custom_data\":{\"LPiaVmoPaOeb\":\"{}\",\"nkqHjvKoZzLo\":4,\"xIaHNrcVLNXX\":true},\"pan\":\"4111111111111111\"}"
-X PUT -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/cardsavr_cards/1061970351
```

### Path

PUT /cardsavr_cards OR /cardsavr_cards/{id}

### Description

Upsert can be used to either update a card, create a new card, or return an existing card.  Either an id or customer_key is required for upsert. The id (in path or body), along with an updated body, can be used to update an existing card; the customer_key (in body) can likewise be used to update a card, and can also be used to create a new card, if the customer_key does not match any existing cards. If the id or customer_key provided corresponds to a pre-existing card and no updated information has been included in the body, the existing card will be returned.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

### Body parameters

Parameter | Type | Description 
-------- | ---- | ---------
address_id | number | ID of address associated with this card.
bin_id | number | ID of BIN associated with this card.
cvv | string | 
expiration_month | [string enum](#post-cardsavr_card-2)** | 
expiration_year | string | 
name_on_card | string | 
nickname | string | 
custom_data | object | Meta-data that can be added to the card if needed.

See [card response parameters](#response-cardsavr_card).


## Delete card

```shell
curl -X DELETE
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/cardsavr_cards/1061970351
```

```javascript
await session.deleteCard(undefined);
```

```csharp
CardSavrResponse<Card> card = await http.DeleteCardAsync(undefined);
```

```java
JsonValue card = session.delete("/cardsavr_cards", undefined, null);
```

### Path

DELETE /cardsavr_cards/{id}

### Description

Delete a card and purge its [related items](#cascading-delete).  An id is required on every delete request.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.


See [card response parameters](#response-cardsavr_card).


# Cardholders
Cardholders are the end-users of the CardSavr API, who can have their their payment information updated on merchant site(s). Cardholders can be linked to cards, accounts, and addresses.
## Get cardholder

```javascript
const cardholders = await session.getCardholders(156249640,{"sort":"id","is_descending":true,"page":1, "page_length":25,{'x-cardsavr-hydration':JSON.stringify(["financial_institution","integrator"])});
```

```csharp
Paging paging = new Paging() { PageLength = 100, IsDescending = true, Page = 1, Sort = "id" };
HttpRequestHeaders headers = new HttpRequestMessage().Headers;
string[] array = { "cardholder","merchant_site","cardsavr_card" };
var json = JsonConvert.SerializeObject(array);
headers.Add("x-cardsavr-hydration", json);
var query = new {ids = 1};
QueryDef qd = new QueryDef(query);
CardSavrResponse<Cardholders> cardholders = await session.GetCardholdersAsync(qd,paging,headers);
```

```java
Headers headers = session.createHeaders();
headers.paging = Json.createObjectBuilder().add("page", 1).add("page_length", 5).add("is_descending", true).add("sort", "id").build();
headers.hydration = {'x-cardsavr-hydration':JSON.stringify(["financial_institution","integrator"])}
JsonArray response = (JsonArray)session.get(156249640, null, headers);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 156249640,
  "type": "persistent_all",
  "first_name": "Jane",
  "last_name": "Smith",
  "email": "test_email@strivve.com",
  "meta_key": "AaqJvLSKTEnrtXUvX",
  "webhook_url": "https://mywebhooks.com/this",
  "custom_data": {
    "gwNcdzYDmZCu": "QCz8Ks/SGG.",
    "DgMbXSgNDHOW": 41,
    "FgiamDUOHWRb": false
  },
  "created_on": "1991-04-04T20:55:09.907Z",
  "last_updated_on": "1983-10-24T19:36:36.406Z",
  "financial_institution": {
    "id": 942157022,
    "name": "xKjlMCHZATxLfuhlIuPPBNxngIBhgTZIgdqcOtiWFFHrOiUymbiUMjNuUpTOHru",
    "description": "hJlrRkMSdPWLf",
    "lookup_key": "lobjEWhdbXreJgvBXgWBJkqIiWJTrVNtuSKZBxUHurYMUGWsEOXgBHKkrENKojU",
    "alternate_lookup_key": "DKOabfHqHrZdeHXzrFMokqFZVRKHkUAJkScGNDIchEqJhPERnCAWdNNDZHtyEMw",
    "active": true,
    "last_activity": "1997-03-30T08:47:42.756Z",
    "created_on": "1991-02-10T11:21:45.051Z",
    "last_updated_on": "1985-02-14T19:40:49.404Z"
  },
  "integrator": {
    "id": 452548627,
    "name": "IQsdcMwYICMvNkHoGbFtnXWUGSirKIbwnDeDLxoxHAupWOiMU",
    "description": "xoNVuWRTQupdOZO",
    "current_key": "7EIRbwU7PBPmYOM2y4dxiCmj7r+F01W370tjjmtgdh0=",
    "key_lifetime": 94,
    "key_timestamp": "1989-06-20T13:42:27.784Z",
    "next_rotation_on": "1997-01-21T15:31:09.307Z",
    "created_on": "2010-11-15T00:54:07.191Z",
    "last_updated_on": "2008-04-15T13:32:19.557Z"
  },
  "cuid": "cOLPvEWgkqvpSrI",
  "source": {
    "type": "navigation",
    "category": "card_controls",
    "sub_category": "(ks",
    "device": "mobile app",
    "integration": "CU3_CL"
  }
}
```

### Path

GET /cardholders **(batch)** or GET /cardholders/:id **(singular)**

### Description

Returns the cardholder specified by the provided ID

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

#### Batch GET requests

**Batch requests** return the first page of all viewable cardholders, filtered by any [query filters](#get-filters) (see list of possible parameters below) listed in the path.


### Filter parameters
- ids / id (in path)
- financial_institution_id
- cuid
- type
- first_name
- last_name
- email
- meta_key
- created_on_min / created_on_max
- last_updated_on_min / last_updated_on_max

**Example batch GET request path:**<br>`/cardholders?ids=1,2`

#### Singular GET requests

**Singular requests** only return the cardholder matching the id provided in the path.

**Example GET request path:**<br>`/cardholders/156249640`

### <a name="response-cardholder"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number (pk) | Unique ID of this cardholder.
financial_institution_id | number (fk) [financial institutions](#financial-institutions) | 
type | string | It is critical to understand the behavior associated with each cardholder type.  The default, 'ephemeral', cardholder is deleted along with all its associated entities upon session termination.  'persistent_credentials' cardholders are not removed automatically, but their associated cards are.  'persistent_all' cardholders are not removed and neither are any of their associated entities. If not storing CardSavr ids within your application, you can look up cards and accounts using the corresponding customer_key. 
first_name | string | 
last_name | string | 
email | string | 
meta_key | string | Key used for billing record identification; automatically generated during card creation.
webhook_url | string | A cardholder specific url for posting job reults following the end of a session.  This overrides the FI global settiings in the portal.
custom_data | object | Additional data that can be added to the cardholder if needed.
created_on | date | Date this site was created on
last_updated_on | date | Date this site was last updated on
cuid | string | External unique ID for cardholder--can be account_id, email address, phone number, etc.  A random number will be gnenerated if not provided.
source | object | Information that identifies how the cardholder was acquired. Parameters supported are type, category, device and sub_category.

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

## Create cardholder

```javascript
const cardholder = await session.createCardholder({
  "cuid": "cOLPvEWgkqvpSrI",
  "type": "persistent_all",
  "first_name": "Jane",
  "last_name": "Smith",
  "email": "test_email@strivve.com",
  "meta_key": "AaqJvLSKTEnrtXUvX",
  "webhook_url": "https://mywebhooks.com/this",
  "custom_data": {
    "gwNcdzYDmZCu": "QCz8Ks/SGG.",
    "DgMbXSgNDHOW": 41,
    "FgiamDUOHWRb": false
  },
  "source": {
    "type": "navigation",
    "category": "card_controls",
    "sub_category": "(ks",
    "device": "mobile app",
    "integration": "CU3_CL"
  }
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "cuid", "cOLPvEWgkqvpSrI" },
	{ "type", "persistent_all" },
	{ "first_name", "Jane" },
	{ "last_name", "Smith" },
	{ "email", "test_email@strivve.com" },
	{ "meta_key", "AaqJvLSKTEnrtXUvX" },
	{ "webhook_url", "https://mywebhooks.com/this" }
};

CardSavrResponse<Cardholder> cardholder = await http.CreateCardholderAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("cuid", "cOLPvEWgkqvpSrI" )
	.add("type", "persistent_all" )
	.add("first_name", "Jane" )
	.add("last_name", "Smith" )
	.add("email", "test_email@strivve.com" )
	.add("meta_key", "AaqJvLSKTEnrtXUvX" )
	.add("webhook_url", "https://mywebhooks.com/this" )
	.build();
JsonValue cardholder = session.post("/cardholders", body, null, null);
```

```shell
curl -d "{\"cuid\":\"cOLPvEWgkqvpSrI\",\"type\":\"persistent_all\",\"first_name\":\"Jane\",\"last_name\":\"Smith\",\"email\":\"test_email@strivve.com\",\"meta_key\":\"AaqJvLSKTEnrtXUvX\",\"webhook_url\":\"https://mywebhooks.com/this\",\"custom_data\":{\"gwNcdzYDmZCu\":\"QCz8Ks/SGG.\",\"DgMbXSgNDHOW\":41,\"FgiamDUOHWRb\":false},\"source\":{\"type\":\"navigation\",\"category\":\"card_controls\",\"sub_category\":\"(ks\",\"device\":\"mobile app\",\"integration\":\"CU3_CL\"}}"
-X POST -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/cardholders/
```

### Path

POST /cardholders

### Description

Create a cardholder and return the created object.

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

### Body parameters

Parameter | Type | Required | Description
-------- | ---- | --------- | ----------
cuid | string | yes | External unique ID for cardholder--can be account_id, email address, phone number, etc.  A random number will be gnenerated if not provided.
type | [string enum](#post-cardholder-1)* | no | It is critical to understand the behavior associated with each cardholder type.  The default, 'ephemeral', cardholder is deleted along with all its associated entities upon session termination.  'persistent_credentials' cardholders are not removed automatically, but their associated cards are.  'persistent_all' cardholders are not removed and neither are any of their associated entities. If not storing CardSavr ids within your application, you can look up cards and accounts using the corresponding customer_key. 
first_name | string | no | 
last_name | string | no | 
email | string | no | 
meta_key | string | no | Key used for billing record identification; automatically generated during card creation.
webhook_url | string | no | A cardholder specific url for posting job reults following the end of a session.  This overrides the FI global settiings in the portal.
custom_data | object | no | Additional data that can be added to the cardholder if needed.
source | object | no | Information that identifies how the cardholder was acquired. Parameters supported are type, category, device and sub_category.

See [cardholder response attributes](#response-cardholder).

#### <a name="post-cardholder-1"></a>string enum*
- ephemeral
- persistent_nocreds
- persistent_creds
- persistent_all


## Upsert cardholder

```javascript
const cardholder = await session.updateCardholder(1,{
  "type": "persistent_creds",
  "first_name": "Jane",
  "last_name": "Smith",
  "email": "test_email@strivve.com",
  "meta_key": "VkpSjPlPREV",
  "webhook_url": "https://mywebhooks.com/this",
  "custom_data": {
    "YSRORpUZtzcj": "W8BRt8$/JO+rtDotTr]p7}zi8ndyL",
    "BnmNBHmmvfuw": 46,
    "oKitBqFotbsg": false
  }
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "type", "persistent_creds" },
	{ "first_name", "Jane" },
	{ "last_name", "Smith" },
	{ "email", "test_email@strivve.com" },
	{ "meta_key", "VkpSjPlPREV" },
	{ "webhook_url", "https://mywebhooks.com/this" }
};

CardSavrResponse<Cardholder> cardholder = await http.UpdateCardholderAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("type", "persistent_creds" )
	.add("first_name", "Jane" )
	.add("last_name", "Smith" )
	.add("email", "test_email@strivve.com" )
	.add("meta_key", "VkpSjPlPREV" )
	.add("webhook_url", "https://mywebhooks.com/this" )
	.build();
JsonValue cardholder = session.put("/cardholders", body, null, null);
```

```shell
curl -d "{\"type\":\"persistent_creds\",\"first_name\":\"Jane\",\"last_name\":\"Smith\",\"email\":\"test_email@strivve.com\",\"meta_key\":\"VkpSjPlPREV\",\"webhook_url\":\"https://mywebhooks.com/this\",\"custom_data\":{\"YSRORpUZtzcj\":\"W8BRt8$/JO+rtDotTr]p7}zi8ndyL\",\"BnmNBHmmvfuw\":46,\"oKitBqFotbsg\":false}}"
-X PUT -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/cardholders/156249640
```

### Path

PUT /cardholders OR /cardholders/{id}

### Description

Upsert can be used to either update a cardholder, create a new cardholder, or return an existing cardholder.  Either an id or cuid is required for upsert. The id (in path or body), along with an updated body, can be used to update an existing cardholder; the cuid (in body) can likewise be used to update a cardholder, and can also be used to create a new cardholder, if the cuid does not match any existing cardholders. If the id or cuid provided corresponds to a pre-existing cardholder and no updated information has been included in the body, the existing cardholder will be returned.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

### Body parameters

Parameter | Type | Description 
-------- | ---- | ---------
type | [string enum](#post-cardholder-1)* | It is critical to understand the behavior associated with each cardholder type.  The default, 'ephemeral', cardholder is deleted along with all its associated entities upon session termination.  'persistent_credentials' cardholders are not removed automatically, but their associated cards are.  'persistent_all' cardholders are not removed and neither are any of their associated entities. If not storing CardSavr ids within your application, you can look up cards and accounts using the corresponding customer_key. 
first_name | string | 
last_name | string | 
email | string | 
meta_key | string | Key used for billing record identification; automatically generated during card creation.
webhook_url | string | A cardholder specific url for posting job reults following the end of a session.  This overrides the FI global settiings in the portal.
custom_data | object | Additional data that can be added to the cardholder if needed.

See [cardholder response parameters](#response-cardholder).


## Delete cardholder

```shell
curl -X DELETE
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/cardholders/156249640
```

```javascript
await session.deleteCardholder(undefined);
```

```csharp
CardSavrResponse<Cardholder> cardholder = await http.DeleteCardholderAsync(undefined);
```

```java
JsonValue cardholder = session.delete("/cardholders", undefined, null);
```

### Path

DELETE /cardholders/{id}

### Description

Delete a cardholder and purge its [related items](#cascading-delete).  An id is required on every delete request.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.


See [cardholder response parameters](#response-cardholder).


# Users
Users are internal entities, such as agents or admins, that can perform such functions as creating and deleting cardholders, fetching merchant sites, creating jobs, etc.
## Get user

```javascript
const users = await session.getUsers(1732070224,{"sort":"id","is_descending":true,"page":1, "page_length":25,{'x-cardsavr-hydration':JSON.stringify(["financial_institution"])});
```

```csharp
Paging paging = new Paging() { PageLength = 100, IsDescending = true, Page = 1, Sort = "id" };
HttpRequestHeaders headers = new HttpRequestMessage().Headers;
string[] array = { "cardholder","merchant_site","cardsavr_card" };
var json = JsonConvert.SerializeObject(array);
headers.Add("x-cardsavr-hydration", json);
var query = new {ids = 1};
QueryDef qd = new QueryDef(query);
CardSavrResponse<Users> users = await session.GetUsersAsync(qd,paging,headers);
```

```java
Headers headers = session.createHeaders();
headers.paging = Json.createObjectBuilder().add("page", 1).add("page_length", 5).add("is_descending", true).add("sort", "id").build();
headers.hydration = {'x-cardsavr-hydration':JSON.stringify(["financial_institution"])}
JsonArray response = (JsonArray)session.get(1732070224, null, headers);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 1732070224,
  "first_name": "Joe",
  "last_name": "Smith",
  "last_login_time": "2013-06-16T23:09:56.164Z",
  "is_locked": false,
  "password_lifetime": 169,
  "email": "test_email@strivve.com",
  "is_password_update_required": false,
  "role": "swch_agent",
  "next_rotation_on": "1974-02-05T14:38:40.492Z",
  "created_on": "2022-07-14T12:12:30.407Z",
  "last_updated_on": "2018-01-22T00:28:53.107Z",
  "username": "jsmith123",
  "financial_institution": {
    "id": 196506442,
    "name": "ZKkcHQjGCFGNIfzYheYokElyHfaolshVJbGvpJqvaWZbskvRmlyAcZmdvZYiINo",
    "description": "Dnohk",
    "lookup_key": "FXvDHHNoAVRglecAHLoZONuidbgzpdSVgHOxuLorfAAfGVCqcMfjkPVQWuRhrmU",
    "alternate_lookup_key": "YDmOocZkluRokdunBzYRDNimcRUIQragrGfrTDacNzKonnbQJmiismFcmtncJZk",
    "active": true,
    "last_activity": "1989-02-24T19:24:24.475Z",
    "created_on": "2011-12-09T10:21:11.599Z",
    "last_updated_on": "1984-01-17T01:09:09.965Z"
  }
}
```

### Path

GET /cardsavr_users **(batch)** or GET /cardsavr_users/:id **(singular)**

### Description

Returns the user specified by the provided ID

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

#### Batch GET requests

**Batch requests** return the first page of all viewable users, filtered by any [query filters](#get-filters) (see list of possible parameters below) listed in the path.


### Filter parameters
- ids / id (in path)
- financial_institution_id
- usernames
- username
- first_name
- last_name
- last_login_time_min / last_login_time_max
- is_locked
- email
- is_password_update_required
- role
- roles_include / roles_exclude
- created_on_min / created_on_max
- last_updated_on_min / last_updated_on_max

**Example batch GET request path:**<br>`/cardsavr_users?ids=1,2`

#### Singular GET requests

**Singular requests** only return the user matching the id provided in the path.

**Example GET request path:**<br>`/cardsavr_users/1732070224`

### <a name="response-cardsavr_user"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number (pk) | Unique ID of this user.
financial_institution_id | number (fk) [financial institutions](#financial-institutions) | 
first_name | string | 
last_name | string | 
last_login_time | date | 
is_locked | boolean | 
password_lifetime | number | Length of time that password will remain valid.
email | string | 
is_password_update_required | boolean | 
role | string | <p>User role (cardholder_agent, cardholder_sso_agent or customer_agent) determines the user's ability to access certain endpoints and perform certain operations within the CardSavr API.</p><p>cardholder_agents can create cardholders, create card's addresses for those cardholders, create accounts for those cardholders, and post jobs for those cardholders. cardholder_sso_agents are like cardholder_agent, but cannot create cardholder or cards.</p>customer_agents can peform all actions on cardholders/accounts/, but are limited to acting on cardholders/jobs/accounts/cards within their FI (unless they are assigned to the admin FI)
next_rotation_on | date | Date of next password rotation for this user.
created_on | date | Date this site was created on
last_updated_on | date | Date this site was last updated on
username | string | 

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

## Create user

```javascript
const user = await session.createUser({
  "financial_institution_id": 528086634,
  "username": "jsmith123",
  "password": "BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI=",
  "first_name": "Joe",
  "last_name": "Smith",
  "password_lifetime": 169,
  "email": "test_email@strivve.com",
  "is_password_update_required": false,
  "role": "swch_agent",
  "next_rotation_on": "1974-02-05T14:38:40.492Z"
}, CARDHOLDER_SAFE_KEY);
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "financial_institution_id", 528086634 },
	{ "username", "jsmith123" },
	{ "password", "BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI=" },
	{ "first_name", "Joe" },
	{ "last_name", "Smith" },
	{ "password_lifetime", 169 },
	{ "email", "test_email@strivve.com" },
	{ "is_password_update_required", false },
	{ "role", "swch_agent" },
	{ "next_rotation_on", "1974-02-05T14:38:40.492Z" }
};

CardSavrResponse<User> user = await http.CreateUserAsync(body, CARDHOLDER_SAFE_KEY);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("financial_institution_id", 528086634 )
	.add("username", "jsmith123" )
	.add("password", "BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI=" )
	.add("first_name", "Joe" )
	.add("last_name", "Smith" )
	.add("password_lifetime", 169 )
	.add("email", "test_email@strivve.com" )
	.add("is_password_update_required", false )
	.add("role", "swch_agent" )
	.add("next_rotation_on", "1974-02-05T14:38:40.492Z" )
	.build();
JsonValue user = session.post("/cardsavr_users", body, null, null);
```

```shell
curl -d "{\"financial_institution_id\":528086634,\"username\":\"jsmith123\",\"password\":\"BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI=\",\"first_name\":\"Joe\",\"last_name\":\"Smith\",\"password_lifetime\":169,\"email\":\"test_email@strivve.com\",\"is_password_update_required\":false,\"role\":\"swch_agent\",\"next_rotation_on\":\"1974-02-05T14:38:40.492Z\"}"
-X POST -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/cardsavr_users/
```

### Path

POST /cardsavr_users

### Description

Create a user and return the created object.

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

### Body parameters

Parameter | Type | Required | Description
-------- | ---- | --------- | ----------
financial_institution_id | number | yes | 
username | string | yes | 
password | string | yes | 
first_name | string | no | 
last_name | string | no | 
password_lifetime | number | no | Length of time that password will remain valid.
email | string | no | 
is_password_update_required | boolean | no | 
role | [string enum](#post-cardsavr_user-1)* | yes | <p>User role (cardholder_agent, cardholder_sso_agent or customer_agent) determines the user's ability to access certain endpoints and perform certain operations within the CardSavr API.</p><p>cardholder_agents can create cardholders, create card's addresses for those cardholders, create accounts for those cardholders, and post jobs for those cardholders. cardholder_sso_agents are like cardholder_agent, but cannot create cardholder or cards.</p>customer_agents can peform all actions on cardholders/accounts/, but are limited to acting on cardholders/jobs/accounts/cards within their FI (unless they are assigned to the admin FI)
next_rotation_on | date | no | Date of next password rotation for this user.

See [user response attributes](#response-cardsavr_user).

#### <a name="post-cardsavr_user-1"></a>string enum*
- admin
- cardholder_sso_agent
- cardholder_agent
- customer_agent
- swch_agent


## Update user

```javascript
const user = await session.updateUser(1,{
  "financial_institution_id": 1870921812,
  "first_name": "Joe",
  "last_name": "Smith",
  "password_lifetime": 288,
  "email": "test_email@strivve.com",
  "is_password_update_required": true,
  "role": "cardholder_sso_agent",
  "next_rotation_on": "1980-01-15T08:03:08.356Z",
  "username": "jsmith123",
  "password": "BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI="
}, NEW_CARDHODLER_SAFE_KEY, CARDHOLDER_SAFE_KEY);
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "financial_institution_id", 1870921812 },
	{ "first_name", "Joe" },
	{ "last_name", "Smith" },
	{ "password_lifetime", 288 },
	{ "email", "test_email@strivve.com" },
	{ "is_password_update_required", true },
	{ "role", "cardholder_sso_agent" },
	{ "next_rotation_on", "1980-01-15T08:03:08.356Z" },
	{ "username", "jsmith123" },
	{ "password", "BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI=" }
};

CardSavrResponse<User> user = await http.UpdateUserAsync(body, NEW_CARDHODLER_SAFE_KEY, CARDHOLDER_SAFE_KEY);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("financial_institution_id", 1870921812 )
	.add("first_name", "Joe" )
	.add("last_name", "Smith" )
	.add("password_lifetime", 288 )
	.add("email", "test_email@strivve.com" )
	.add("is_password_update_required", true )
	.add("role", "cardholder_sso_agent" )
	.add("next_rotation_on", "1980-01-15T08:03:08.356Z" )
	.add("username", "jsmith123" )
	.add("password", "BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI=" )
	.build();
JsonValue user = session.put("/cardsavr_users", body, null, null);
```

```shell
curl -d "{\"financial_institution_id\":1870921812,\"first_name\":\"Joe\",\"last_name\":\"Smith\",\"password_lifetime\":288,\"email\":\"test_email@strivve.com\",\"is_password_update_required\":true,\"role\":\"cardholder_sso_agent\",\"next_rotation_on\":\"1980-01-15T08:03:08.356Z\",\"username\":\"jsmith123\",\"password\":\"BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI=\"}"
-X PUT -H "Content-Type: application/json"
-H "x-cardsavr-new-cardholder-safe-key: NEW_CARDHODLER_SAFE_KEY"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/cardsavr_users/1732070224
```

### Path

PUT /cardsavr_users OR /cardsavr_users/{id}

### Description

Update a user and return the updated object.  An id is required on every update request.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

### Body parameters

Parameter | Type | Description 
-------- | ---- | ---------
financial_institution_id | number | 
first_name | string | 
last_name | string | 
password_lifetime | number | Length of time that password will remain valid.
email | string | 
is_password_update_required | boolean | 
role | [string enum](#post-cardsavr_user-1)* | <p>User role (cardholder_agent, cardholder_sso_agent or customer_agent) determines the user's ability to access certain endpoints and perform certain operations within the CardSavr API.</p><p>cardholder_agents can create cardholders, create card's addresses for those cardholders, create accounts for those cardholders, and post jobs for those cardholders. cardholder_sso_agents are like cardholder_agent, but cannot create cardholder or cards.</p>customer_agents can peform all actions on cardholders/accounts/, but are limited to acting on cardholders/jobs/accounts/cards within their FI (unless they are assigned to the admin FI)
next_rotation_on | date | Date of next password rotation for this user.

See [user response parameters](#response-cardsavr_user).


## Delete user

```shell
curl -X DELETE
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/cardsavr_users/1732070224
```

```javascript
await session.deleteUser(undefined);
```

```csharp
CardSavrResponse<User> user = await http.DeleteUserAsync(undefined);
```

```java
JsonValue user = session.delete("/cardsavr_users", undefined, null);
```

### Path

DELETE /cardsavr_users/{id}

### Description

Delete a user and purge its [related items](#cascading-delete).  An id is required on every delete request.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.


See [user response parameters](#response-cardsavr_user).


# Financial Institutions
Financial Institution (FI) objects represent individual FIs and can be linked to users and cardholders. They also contain the configuration information that can be used to customize an FI's CardUpdatr instance, if one exists.
## Get financial institution

```javascript
const financialinstitutions = await session.getFinancialInstitutions(786378094,{"sort":"id","is_descending":true,"page":1, "page_length":25,);
```

```csharp
Paging paging = new Paging() { PageLength = 100, IsDescending = true, Page = 1, Sort = "id" };
HttpRequestHeaders headers = new HttpRequestMessage().Headers;
string[] array = { "cardholder","merchant_site","cardsavr_card" };
var json = JsonConvert.SerializeObject(array);
headers.Add("x-cardsavr-hydration", json);
var query = new {ids = 1};
QueryDef qd = new QueryDef(query);
CardSavrResponse<FinancialInstitutions> financialinstitutions = await session.GetFinancialInstitutionsAsync(qd,paging,headers);
```

```java
Headers headers = session.createHeaders();
headers.paging = Json.createObjectBuilder().add("page", 1).add("page_length", 5).add("is_descending", true).add("sort", "id").build();
headers.hydration = 
JsonArray response = (JsonArray)session.get(786378094, null, headers);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 786378094,
  "name": "mSZpxEFiuQjmiJXBBOaymjQveickzyRIAWhEOayRGHlmAEKUmSgYCdmzJOQSmuT",
  "description": "QsJp",
  "lookup_key": "qduwUpvVTtBtDjaqEXDzyScUqVUphsahPqdbBRRRLuiwzIqmRzDlKwgGIgHiiyw",
  "alternate_lookup_key": "BxNvDJNyMjZFbMBkmCzMcuqCppIriytgqVABbjmnOpwLjsiNmMmRsSuhROpoXyX",
  "active": false,
  "last_activity": "2022-07-30T15:20:29.805Z",
  "created_on": "1990-07-03T01:53:23.862Z",
  "last_updated_on": "1998-10-26T06:28:22.190Z"
}
```

### Path

GET /financial_institutions **(batch)** or GET /financial_institutions/:id **(singular)**

### Description

Returns the financial institution specified by the provided ID

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

#### Batch GET requests

**Batch requests** return the first page of all viewable financial institutions, filtered by any [query filters](#get-filters) (see list of possible parameters below) listed in the path.


### Filter parameters
- ids / id (in path)
- id
- names
- lookup_key
- exclude_lookup_keys
- alternate_lookup_key
- active
- last_activity_min / last_activity_max
- created_on_min / created_on_max
- last_updated_on_min / last_updated_on_max

**Example batch GET request path:**<br>`/financial_institutions?ids=1,2`

#### Singular GET requests

**Singular requests** only return the financial institution matching the id provided in the path.

**Example GET request path:**<br>`/financial_institutions/786378094`

### <a name="response-financial_institution"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number (pk) | Unique ID of this financial institution.
name | string | 
description | string | 
lookup_key | string | Unique key used to identify financial institution.
alternate_lookup_key | string | Alternate lookup key; can be used in case of FI name change that does not match original lookup_key, in order to maintain backwards compatibility.
active | boolean | FI's set as inactive or still accessible in the portal, but not usable on the frontend.  All usage with this fi will be rejected except looking it up.
last_activity | date | Date of last cardholder creation for this financial institution
created_on | date | Date this financial institution was created on
last_updated_on | date | Date this financial institution was last updated on

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

## Create financial institution

```javascript
const financialinstitution = await session.createFinancialInstitution({
  "name": "mSZpxEFiuQjmiJXBBOaymjQveickzyRIAWhEOayRGHlmAEKUmSgYCdmzJOQSmuT",
  "description": "QsJp",
  "lookup_key": "qduwUpvVTtBtDjaqEXDzyScUqVUphsahPqdbBRRRLuiwzIqmRzDlKwgGIgHiiyw",
  "alternate_lookup_key": "BxNvDJNyMjZFbMBkmCzMcuqCppIriytgqVABbjmnOpwLjsiNmMmRsSuhROpoXyX",
  "active": false
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "name", "mSZpxEFiuQjmiJXBBOaymjQveickzyRIAWhEOayRGHlmAEKUmSgYCdmzJOQSmuT" },
	{ "description", "QsJp" },
	{ "lookup_key", "qduwUpvVTtBtDjaqEXDzyScUqVUphsahPqdbBRRRLuiwzIqmRzDlKwgGIgHiiyw" },
	{ "alternate_lookup_key", "BxNvDJNyMjZFbMBkmCzMcuqCppIriytgqVABbjmnOpwLjsiNmMmRsSuhROpoXyX" },
	{ "active", false }
};

CardSavrResponse<FinancialInstitution> financialinstitution = await http.CreateFinancialInstitutionAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("name", "mSZpxEFiuQjmiJXBBOaymjQveickzyRIAWhEOayRGHlmAEKUmSgYCdmzJOQSmuT" )
	.add("description", "QsJp" )
	.add("lookup_key", "qduwUpvVTtBtDjaqEXDzyScUqVUphsahPqdbBRRRLuiwzIqmRzDlKwgGIgHiiyw" )
	.add("alternate_lookup_key", "BxNvDJNyMjZFbMBkmCzMcuqCppIriytgqVABbjmnOpwLjsiNmMmRsSuhROpoXyX" )
	.add("active", false )
	.build();
JsonValue financialinstitution = session.post("/financial_institutions", body, null, null);
```

```shell
curl -d "{\"name\":\"mSZpxEFiuQjmiJXBBOaymjQveickzyRIAWhEOayRGHlmAEKUmSgYCdmzJOQSmuT\",\"description\":\"QsJp\",\"lookup_key\":\"qduwUpvVTtBtDjaqEXDzyScUqVUphsahPqdbBRRRLuiwzIqmRzDlKwgGIgHiiyw\",\"alternate_lookup_key\":\"BxNvDJNyMjZFbMBkmCzMcuqCppIriytgqVABbjmnOpwLjsiNmMmRsSuhROpoXyX\",\"active\":false}"
-X POST -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/financial_institutions/
```

### Path

POST /financial_institutions

### Description

Create a financial institution and return the created object.

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

### Body parameters

Parameter | Type | Required | Description
-------- | ---- | --------- | ----------
name | string | yes | 
description | string | no | 
lookup_key | string | yes | Unique key used to identify financial institution.
alternate_lookup_key | string | no | Alternate lookup key; can be used in case of FI name change that does not match original lookup_key, in order to maintain backwards compatibility.
active | boolean | no | FI's set as inactive or still accessible in the portal, but not usable on the frontend.  All usage with this fi will be rejected except looking it up.

See [financial institution response attributes](#response-financial_institution).


## Update financial institution

```javascript
const financialinstitution = await session.updateFinancialInstitution(1,{
  "name": "TErxacDCOREouvzLOSQWIMQiFagEJfvwziUylwOVwtSFDljKqlmfDAoaOcSRwUi",
  "description": "hAEPk",
  "lookup_key": "GqxRGGQYGZdOAZFzBPusDNekdVWMUmksbDSRniOECPHyopvbPrEtpAHATtzuCxY",
  "alternate_lookup_key": "kNdKcTifrGGSNjoXNEypXhawdXPQqZIVOhUicbkRrvYnHixvBMvPTkQMIunfluZ",
  "active": false
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "name", "TErxacDCOREouvzLOSQWIMQiFagEJfvwziUylwOVwtSFDljKqlmfDAoaOcSRwUi" },
	{ "description", "hAEPk" },
	{ "lookup_key", "GqxRGGQYGZdOAZFzBPusDNekdVWMUmksbDSRniOECPHyopvbPrEtpAHATtzuCxY" },
	{ "alternate_lookup_key", "kNdKcTifrGGSNjoXNEypXhawdXPQqZIVOhUicbkRrvYnHixvBMvPTkQMIunfluZ" },
	{ "active", false }
};

CardSavrResponse<FinancialInstitution> financialinstitution = await http.UpdateFinancialInstitutionAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("name", "TErxacDCOREouvzLOSQWIMQiFagEJfvwziUylwOVwtSFDljKqlmfDAoaOcSRwUi" )
	.add("description", "hAEPk" )
	.add("lookup_key", "GqxRGGQYGZdOAZFzBPusDNekdVWMUmksbDSRniOECPHyopvbPrEtpAHATtzuCxY" )
	.add("alternate_lookup_key", "kNdKcTifrGGSNjoXNEypXhawdXPQqZIVOhUicbkRrvYnHixvBMvPTkQMIunfluZ" )
	.add("active", false )
	.build();
JsonValue financialinstitution = session.put("/financial_institutions", body, null, null);
```

```shell
curl -d "{\"name\":\"TErxacDCOREouvzLOSQWIMQiFagEJfvwziUylwOVwtSFDljKqlmfDAoaOcSRwUi\",\"description\":\"hAEPk\",\"lookup_key\":\"GqxRGGQYGZdOAZFzBPusDNekdVWMUmksbDSRniOECPHyopvbPrEtpAHATtzuCxY\",\"alternate_lookup_key\":\"kNdKcTifrGGSNjoXNEypXhawdXPQqZIVOhUicbkRrvYnHixvBMvPTkQMIunfluZ\",\"active\":false}"
-X PUT -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/financial_institutions/786378094
```

### Path

PUT /financial_institutions OR /financial_institutions/{id}

### Description

Update a financial institution and return the updated object.  An id is required on every update request.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

### Body parameters

Parameter | Type | Description 
-------- | ---- | ---------
name | string | 
description | string | 
lookup_key | string | Unique key used to identify financial institution.
alternate_lookup_key | string | Alternate lookup key; can be used in case of FI name change that does not match original lookup_key, in order to maintain backwards compatibility.
active | boolean | FI's set as inactive or still accessible in the portal, but not usable on the frontend.  All usage with this fi will be rejected except looking it up.

See [financial institution response parameters](#response-financial_institution).


## Delete financial institution

```shell
curl -X DELETE
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/financial_institutions/786378094
```

```javascript
await session.deleteFinancialInstitution(undefined);
```

```csharp
CardSavrResponse<FinancialInstitution> financialinstitution = await http.DeleteFinancialInstitutionAsync(undefined);
```

```java
JsonValue financialinstitution = session.delete("/financial_institutions", undefined, null);
```

### Path

DELETE /financial_institutions/{id}

### Description

Delete a financial institution and purge its [related items](#cascading-delete).  An id is required on every delete request.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.


See [financial institution response parameters](#response-financial_institution).


# Integrators
Integrators are applications that integrate the CardSavr API, using their own unique integrator key. An integrator name and key are required for all calls to the CardSavr API. An integrator can be associated with multiple users.
## Get integrator

```javascript
const integrators = await session.getIntegrators(1641648524,{"sort":"id","is_descending":true,"page":1, "page_length":25,{'x-cardsavr-hydration':JSON.stringify(["financial_institution"])});
```

```csharp
Paging paging = new Paging() { PageLength = 100, IsDescending = true, Page = 1, Sort = "id" };
HttpRequestHeaders headers = new HttpRequestMessage().Headers;
string[] array = { "cardholder","merchant_site","cardsavr_card" };
var json = JsonConvert.SerializeObject(array);
headers.Add("x-cardsavr-hydration", json);
var query = new {ids = 1};
QueryDef qd = new QueryDef(query);
CardSavrResponse<Integrators> integrators = await session.GetIntegratorsAsync(qd,paging,headers);
```

```java
Headers headers = session.createHeaders();
headers.paging = Json.createObjectBuilder().add("page", 1).add("page_length", 5).add("is_descending", true).add("sort", "id").build();
headers.hydration = {'x-cardsavr-hydration':JSON.stringify(["financial_institution"])}
JsonArray response = (JsonArray)session.get(1641648524, null, headers);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 1641648524,
  "name": "fWwZFbKtttZulZZCZUpIBPhprFiKoTuTivuscyFJKbUuTOwNq",
  "description": "xMmFdiEK",
  "current_key": "vmiwlJw3NXRQveQiV+KNupn2Osyf4nKf4W1Tg/c1gcM=",
  "key_lifetime": 262,
  "key_timestamp": "1977-06-09T21:22:38.458Z",
  "next_rotation_on": "1983-12-22T13:41:02.872Z",
  "created_on": "1989-01-17T10:40:17.987Z",
  "last_updated_on": "2000-11-06T04:29:53.122Z",
  "financial_institution": {
    "id": 60267621,
    "name": "mJykevfPczDfptfUByDRTPVUmQvDCUqXFeXZwMUSpobPRzVRekMgQINQLLFLDar",
    "description": "WSIAZjNKp",
    "lookup_key": "QVrlYMMtwxyKSKWQRbQcCYUKgMLCexxcYCfLVGSoqFvwjsdYIlaPHzUXsqisYeb",
    "alternate_lookup_key": "sOZUctBQuLMwtteyLRhIUERzkkDVrZUaurdmVIAqaEiblUCVoJBxnAKebTtLuDH",
    "active": false,
    "last_activity": "2015-08-24T03:19:35.861Z",
    "created_on": "1972-06-15T20:21:22.018Z",
    "last_updated_on": "1984-02-20T23:15:00.062Z"
  }
}
```

### Path

GET /integrators **(batch)** or GET /integrators/:id **(singular)**

### Description

Returns the integrator specified by the provided ID

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

#### Batch GET requests

**Batch requests** return the first page of all viewable integrators, filtered by any [query filters](#get-filters) (see list of possible parameters below) listed in the path.


### Filter parameters
- ids / id (in path)
- names
- name
- financial_institution_id
- next_rotation_on_min / next_rotation_on_max
- created_on_min / created_on_max
- last_updated_on_min / last_updated_on_max

**Example batch GET request path:**<br>`/integrators?ids=1,2`

#### Singular GET requests

**Singular requests** only return the integrator matching the id provided in the path.

**Example GET request path:**<br>`/integrators/1641648524`

### <a name="response-integrator"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number (pk) | Unique ID of this integrator.
name | string | Name of integrator.
financial_institution_id | number (fk) [financial institutions](#financial-institutions) | Financial Institution associated with this integrator
description | string | 
current_key | string | Current key for this integrator.
key_lifetime | number | Sets the duration of validity for integrator key.
key_timestamp | date | Date that key was last updated (includes creation, rotation, or revert).
next_rotation_on | date | Date of next key rotation for this integrator.
created_on | date | Date this integrator was created on
last_updated_on | date | Date this integrator was last updated on

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

## Create integrator

```javascript
const integrator = await session.createIntegrator({
  "name": "fWwZFbKtttZulZZCZUpIBPhprFiKoTuTivuscyFJKbUuTOwNq",
  "financial_institution_id": 1798221655,
  "description": "xMmFdiEK",
  "current_key": "vmiwlJw3NXRQveQiV+KNupn2Osyf4nKf4W1Tg/c1gcM=",
  "key_lifetime": 262,
  "next_rotation_on": "1983-12-22T13:41:02.872Z"
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "name", "fWwZFbKtttZulZZCZUpIBPhprFiKoTuTivuscyFJKbUuTOwNq" },
	{ "financial_institution_id", 1798221655 },
	{ "description", "xMmFdiEK" },
	{ "current_key", "vmiwlJw3NXRQveQiV+KNupn2Osyf4nKf4W1Tg/c1gcM=" },
	{ "key_lifetime", 262 },
	{ "next_rotation_on", "1983-12-22T13:41:02.872Z" }
};

CardSavrResponse<Integrator> integrator = await http.CreateIntegratorAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("name", "fWwZFbKtttZulZZCZUpIBPhprFiKoTuTivuscyFJKbUuTOwNq" )
	.add("financial_institution_id", 1798221655 )
	.add("description", "xMmFdiEK" )
	.add("current_key", "vmiwlJw3NXRQveQiV+KNupn2Osyf4nKf4W1Tg/c1gcM=" )
	.add("key_lifetime", 262 )
	.add("next_rotation_on", "1983-12-22T13:41:02.872Z" )
	.build();
JsonValue integrator = session.post("/integrators", body, null, null);
```

```shell
curl -d "{\"name\":\"fWwZFbKtttZulZZCZUpIBPhprFiKoTuTivuscyFJKbUuTOwNq\",\"financial_institution_id\":1798221655,\"description\":\"xMmFdiEK\",\"current_key\":\"vmiwlJw3NXRQveQiV+KNupn2Osyf4nKf4W1Tg/c1gcM=\",\"key_lifetime\":262,\"next_rotation_on\":\"1983-12-22T13:41:02.872Z\"}"
-X POST -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/integrators/
```

### Path

POST /integrators

### Description

Create a integrator and return the created object.

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

### Body parameters

Parameter | Type | Required | Description
-------- | ---- | --------- | ----------
name | string | yes | Name of integrator.
financial_institution_id | number | yes | Financial Institution associated with this integrator
description | string | no | 
current_key | string | yes | Current key for this integrator.
key_lifetime | number | no | Sets the duration of validity for integrator key.
next_rotation_on | date | no | Date of next key rotation for this integrator.

See [integrator response attributes](#response-integrator).


## Update integrator

```javascript
const integrator = await session.updateIntegrator(1,{
  "name": "rkOeYkVChfjzYNLPpKlWiStzXDoEhoWviTocvJKwrmwgXTwdW",
  "financial_institution_id": 1558894823,
  "description": "lOfwVIpllvGgGdTvh",
  "current_key": "puqY4EVCYl6+/HmyDJu0rtJrdOUEZyOUx5sQNLKjW/0=",
  "key_lifetime": 254,
  "next_rotation_on": "1975-03-18T10:12:29.984Z"
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "name", "rkOeYkVChfjzYNLPpKlWiStzXDoEhoWviTocvJKwrmwgXTwdW" },
	{ "financial_institution_id", 1558894823 },
	{ "description", "lOfwVIpllvGgGdTvh" },
	{ "current_key", "puqY4EVCYl6+/HmyDJu0rtJrdOUEZyOUx5sQNLKjW/0=" },
	{ "key_lifetime", 254 },
	{ "next_rotation_on", "1975-03-18T10:12:29.984Z" }
};

CardSavrResponse<Integrator> integrator = await http.UpdateIntegratorAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("name", "rkOeYkVChfjzYNLPpKlWiStzXDoEhoWviTocvJKwrmwgXTwdW" )
	.add("financial_institution_id", 1558894823 )
	.add("description", "lOfwVIpllvGgGdTvh" )
	.add("current_key", "puqY4EVCYl6+/HmyDJu0rtJrdOUEZyOUx5sQNLKjW/0=" )
	.add("key_lifetime", 254 )
	.add("next_rotation_on", "1975-03-18T10:12:29.984Z" )
	.build();
JsonValue integrator = session.put("/integrators", body, null, null);
```

```shell
curl -d "{\"name\":\"rkOeYkVChfjzYNLPpKlWiStzXDoEhoWviTocvJKwrmwgXTwdW\",\"financial_institution_id\":1558894823,\"description\":\"lOfwVIpllvGgGdTvh\",\"current_key\":\"puqY4EVCYl6+/HmyDJu0rtJrdOUEZyOUx5sQNLKjW/0=\",\"key_lifetime\":254,\"next_rotation_on\":\"1975-03-18T10:12:29.984Z\"}"
-X PUT -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/integrators/1641648524
```

### Path

PUT /integrators OR /integrators/{id}

### Description

Update a integrator and return the updated object.  An id is required on every update request.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

### Body parameters

Parameter | Type | Description 
-------- | ---- | ---------
name | string | Name of integrator.
financial_institution_id | number | Financial Institution associated with this integrator
description | string | 
current_key | string | Current key for this integrator.
key_lifetime | number | Sets the duration of validity for integrator key.
next_rotation_on | date | Date of next key rotation for this integrator.

See [integrator response parameters](#response-integrator).


## Delete integrator

```shell
curl -X DELETE
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/integrators/1641648524
```

```javascript
await session.deleteIntegrator(undefined);
```

```csharp
CardSavrResponse<Integrator> integrator = await http.DeleteIntegratorAsync(undefined);
```

```java
JsonValue integrator = session.delete("/integrators", undefined, null);
```

### Path

DELETE /integrators/{id}

### Description

Delete a integrator and purge its [related items](#cascading-delete).  An id is required on every delete request.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.


See [integrator response parameters](#response-integrator).


# Merchant sites
A merchant site object contains information, such as images URLs and hostname, for a CardSavr-supported merchant site.
## Get merchant site

```javascript
const merchantsites = await session.getMerchantSites(1201166184,{"sort":"id","is_descending":true,"page":1, "page_length":25,);
```

```csharp
Paging paging = new Paging() { PageLength = 100, IsDescending = true, Page = 1, Sort = "id" };
HttpRequestHeaders headers = new HttpRequestMessage().Headers;
string[] array = { "cardholder","merchant_site","cardsavr_card" };
var json = JsonConvert.SerializeObject(array);
headers.Add("x-cardsavr-hydration", json);
var query = new {ids = 1};
QueryDef qd = new QueryDef(query);
CardSavrResponse<MerchantSites> merchantsites = await session.GetMerchantSitesAsync(qd,paging,headers);
```

```java
Headers headers = session.createHeaders();
headers.paging = Json.createObjectBuilder().add("page", 1).add("page_length", 5).add("is_descending", true).add("sort", "id").build();
headers.hydration = 
JsonArray response = (JsonArray)session.get(1201166184, null, headers);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 1201166184,
  "name": "Amazon",
  "note": "saVSGMmHRazagmCqScjUGhyKzcO",
  "host": "amazon.com",
  "tags": [
    "]E(}eU{=",
    96,
    "c9f!5vy7K^&E$F3{2p3.h/+d#[3#XOSP"
  ],
  "interface_type": "rpa_loopback",
  "job_type": "CARD_PLACEMENT",
  "required_form_fields": [
    "email",
    "phone_number",
    "card_data",
    "cvv",
    "billing_address",
    "postal_code"
  ],
  "images": [
    {
      "url": "https://d1t7g1oas7m24a.cloudfront.net/tiles/dollarshaveclub.com?width=128&version=21f917315911eec1b1705bc7784ce861579cff2b",
      "width": 128,
      "grayscale": false
    },
    {
      "url": "https://d1t7g1oas7m24a.cloudfront.net/tiles/dollarshaveclub.com?width=32&version=21f917315911eec1b1705bc7784ce861579cff2b",
      "width": 32,
      "grayscale": false
    }
  ],
  "account_link": [
    {
      "key_name": "username",
      "label": "Username",
      "type": "initial_account_link"
    },
    {
      "key_name": "password",
      "label": "Password",
      "type": "initial_account_link",
      "secret": true
    },
    {
      "key_name": "otp",
      "label": "One Time Passcode",
      "type": ""
    }
  ],
  "messages": {
    "mfa_label": "Additional information required, this code may be sent to your phone or email address.",
    "additional_info_message": "",
    "auth_message": "Linking account."
  },
  "login_page": "https://www.merchantsite.com/login",
  "forgot_password_page": "https://www.merchantsite.com/forgot_password",
  "credit_card_page": "https://www.merchantsite.com/credit_card",
  "wallet_page": "QXsigyUuGTqDECexkjhXGUrUoJI",
  "merchant_sso_group": "VSkFuUjzIDWfwLIwTOW",
  "tier": 940302177
}
```

### Path

GET /merchant_sites **(batch)** or GET /merchant_sites/:id **(singular)**

### Description

Returns the merchant site specified by the provided ID

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

#### Batch GET requests

**Batch requests** return the first page of all viewable merchant sites, filtered by any [query filters](#get-filters) (see list of possible parameters below) listed in the path.


### Filter parameters
- ids / id (in path)
- id
- exclude_ids
- top_ids
- name_starts_with
- hosts
- host
- exclude_hosts
- top_hosts
- host_starts_with
- tags
- image_widths

**Example batch GET request path:**<br>`/merchant_sites?ids=1,2`

#### Singular GET requests

**Singular requests** only return the merchant site matching the id provided in the path.

**Example GET request path:**<br>`/merchant_sites/1201166184`

### <a name="response-merchant_site"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number (pk) | Unique ID of this merchant site.
name | string | 
note | string | Human-readable note about the site for developers
host | string | For interface type 'dcs',  hostname of the DCS broker server for the merchant site; for interface type 'vbs' hostname of the merchant_site. e.g. amazon.com
tags | array | Tags for filtering desired merchant sites.  This could either be site status (e.g. prod, development), countries supported (e.g. usa, canada), or site attributes (e.g. synthetic).  Tags can also be compounded to create combinations: (e.g. ?tags=prod,usa&tags=synthetic means all sites tagged prod and usa as well as sites tagged synthetic)
interface_type | string | Type of interface agent to use with merchant. Set to 'dcs' for a site that has direct connect support; and to 'vbs' for a site using Robotic Process Automation
job_type | string | Type of job this site supports. Card placement or bill payment
required_form_fields | array | Indicates the cardholder personal information fields that are required by this site.
images | array | URLs of the images for this merchant site.  Use a filter parameter of 'image_widths', a comma delimited list of widths (e.g. image_widths=64).  Tile images with these widths will be returned.  The default is 128 and 32 width images.
account_link | array | One or more property sets with key names to populated on POST/PUT /cardsavr_accounts requests, and labels to display to the end user for the type of information being requested for this site ( e.g. Username, Password, Account Number, Email, ... ) Each property contains its 'key_name', a 'label' that defines the property, a 'secret' flag (property should be masked on input like a password), and a type.  Only properties with a type of 'initial_account_link' should be presented upon initial credential collection.  For example, an input field for 'tfa' is not displayed on initial collection.  All other non-'initial_account_link' properties will be requested while the transactiion progresses and they are only listed here for informational purposes.
messages | object | Message properties to display to end users.  Supercedes the deprecated loging properties. The message properties are mfa_label: additional informaton required for mfs challenges such as a code sent to users phone or email, additional_info_message: some contextual info sent from CardSavr to aid the user interaction, auth_message: a label to display during during the authentication phase
login_page | string | URL of login page.
forgot_password_page | string | Merchant's forgotten password page.
credit_card_page | string | Merchant's credit card entry page.
wallet_page | string | URL of the site's wallet page, where the is a list of last 4 card numbers.
merchant_sso_group | string | Default group a site rolls up to. Jobs for the same user account should not run simultaneously.
tier | number | Site's tier based on perceived card usage on that site.

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

# Notifications
Notification objects define a set of actions to be triggered by certain CardSavr events, such as session completion.
## Get notification

```javascript
const notifications = await session.getNotifications(1437913716,{"sort":"id","is_descending":true,"page":1, "page_length":25,{'x-cardsavr-hydration':JSON.stringify(["financial_institution"])});
```

```csharp
Paging paging = new Paging() { PageLength = 100, IsDescending = true, Page = 1, Sort = "id" };
HttpRequestHeaders headers = new HttpRequestMessage().Headers;
string[] array = { "cardholder","merchant_site","cardsavr_card" };
var json = JsonConvert.SerializeObject(array);
headers.Add("x-cardsavr-hydration", json);
var query = new {ids = 1};
QueryDef qd = new QueryDef(query);
CardSavrResponse<Notifications> notifications = await session.GetNotificationsAsync(qd,paging,headers);
```

```java
Headers headers = session.createHeaders();
headers.paging = Json.createObjectBuilder().add("page", 1).add("page_length", 5).add("is_descending", true).add("sort", "id").build();
headers.hydration = {'x-cardsavr-hydration':JSON.stringify(["financial_institution"])}
JsonArray response = (JsonArray)session.get(1437913716, null, headers);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 1437913716,
  "name": "Sample Notification",
  "type": "email",
  "event": "merchant_site_updates_all",
  "config": {
    "recipient": "cardholder",
    "url": null,
    "from_email": "CardUpdatr <no-reply@cardupdatr.app>",
    "return_path": "no-reply@cardupdatr.app",
    "send_email_time": null,
    "interval_length": null,
    "interval_type": null
  },
  "html_template": "ShrfwhjTHbJIRt",
  "text_template": "o",
  "created_on": "1970-04-29T03:11:24.092Z",
  "last_updated_on": "2013-04-27T12:06:50.859Z",
  "financial_institution": {
    "id": 444833257,
    "name": "SxnRQkOLHmHvHhMUKmaYqqUctZWnqRVBGmrBMZJITOlSeABmzBIDYESAYbFcwEI",
    "description": "oEuXvjZHTfKnGxUJ",
    "lookup_key": "oNMWFtjMGueBOmkXDfUUetZdXLiGLAMDtlkYDSuKgwaaFQHgeFBMOSMpjfLajXI",
    "alternate_lookup_key": "HKUYnjLQWgBiYTMtkNdCbmTVVFXzQnMNpPJslcKdCwbJTeSRXZFHjLMRWlmjodR",
    "active": true,
    "last_activity": "2021-02-05T18:36:49.512Z",
    "created_on": "1989-02-21T02:39:47.279Z",
    "last_updated_on": "1998-04-04T09:37:18.503Z"
  }
}
```

### Path

GET /notifications **(batch)** or GET /notifications/:id **(singular)**

### Description

Returns the notification specified by the provided ID

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

#### Batch GET requests

**Batch requests** return the first page of all viewable notifications, filtered by any [query filters](#get-filters) (see list of possible parameters below) listed in the path.


### Filter parameters
- ids / id (in path)
- financial_institution_id
- names
- type
- events
- event
- created_on_min / created_on_max
- last_updated_on_min / last_updated_on_max

**Example batch GET request path:**<br>`/notifications?ids=1,2`

#### Singular GET requests

**Singular requests** only return the notification matching the id provided in the path.

**Example GET request path:**<br>`/notifications/1437913716`

### <a name="response-notification"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number (pk) | Unique ID of this notification.
name | string | Name of this notification.
type | string | Notification type (e.g. webhook or email).
event | string | Event that will triger the notification (e.g. session complete).
config | object | 
html_template | string | Overrides the default CardUpdatr html email template (for email notifications).
text_template | string | Overrides the default CardUpdatr text email template (for email notifications).
created_on | date | Date this notification was created on
last_updated_on | date | Date this notification was last updated on
financial_institution_id | number (fk) [financial institutions](#financial-institutions) | ID of the financial institution associated with this notification.

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

## Create notification

```javascript
const notification = await session.createNotification({
  "financial_institution_id": 563292186,
  "name": "Sample Notification",
  "type": "email",
  "event": "merchant_site_updates_all",
  "config": {
    "recipient": "cardholder",
    "url": null,
    "from_email": "CardUpdatr <no-reply@cardupdatr.app>",
    "return_path": "no-reply@cardupdatr.app",
    "send_email_time": null,
    "interval_length": null,
    "interval_type": null
  },
  "html_template": "ShrfwhjTHbJIRt",
  "text_template": "o"
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "financial_institution_id", 563292186 },
	{ "name", "Sample Notification" },
	{ "type", "email" },
	{ "event", "merchant_site_updates_all" },
	{ "html_template", "ShrfwhjTHbJIRt" },
	{ "text_template", "o" }
};

CardSavrResponse<Notification> notification = await http.CreateNotificationAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("financial_institution_id", 563292186 )
	.add("name", "Sample Notification" )
	.add("type", "email" )
	.add("event", "merchant_site_updates_all" )
	.add("html_template", "ShrfwhjTHbJIRt" )
	.add("text_template", "o" )
	.build();
JsonValue notification = session.post("/notifications", body, null, null);
```

```shell
curl -d "{\"financial_institution_id\":563292186,\"name\":\"Sample Notification\",\"type\":\"email\",\"event\":\"merchant_site_updates_all\",\"config\":{\"recipient\":\"cardholder\",\"url\":null,\"from_email\":\"CardUpdatr <no-reply@cardupdatr.app>\",\"return_path\":\"no-reply@cardupdatr.app\",\"send_email_time\":null,\"interval_length\":null,\"interval_type\":null},\"html_template\":\"ShrfwhjTHbJIRt\",\"text_template\":\"o\"}"
-X POST -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/notifications/
```

### Path

POST /notifications

### Description

Create a notification and return the created object.

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

### Body parameters

Parameter | Type | Required | Description
-------- | ---- | --------- | ----------
financial_institution_id | number | yes | ID of the financial institution associated with this notification.
name | string | yes | Name of this notification.
type | [string enum](#post-notification-1)* | yes | Notification type (e.g. webhook or email).
event | [string enum](#post-notification-2)** | yes | Event that will triger the notification (e.g. session complete).
config | object | no | 
html_template | string | no | Overrides the default CardUpdatr html email template (for email notifications).
text_template | string | no | Overrides the default CardUpdatr text email template (for email notifications).

See [notification response attributes](#response-notification).

#### <a name="post-notification-1"></a>string enum*
- email
- webhook

#### <a name="post-notification-2"></a>string enum**
- session_complete
- webhook_error_summary
- merchant_site_updates_top
- merchant_site_updates_all


## Update notification

```javascript
const notification = await session.updateNotification(1,{
  "name": "Sample Notification",
  "type": "email",
  "event": "merchant_site_updates_top",
  "config": {
    "recipient": "cardholder",
    "url": null,
    "from_email": "CardUpdatr <no-reply@cardupdatr.app>",
    "return_path": "no-reply@cardupdatr.app",
    "send_email_time": null,
    "interval_length": null,
    "interval_type": null
  },
  "html_template": "JRzFvYrmrVqtEYhpGFyQUQs",
  "text_template": "wGKQs"
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "name", "Sample Notification" },
	{ "type", "email" },
	{ "event", "merchant_site_updates_top" },
	{ "html_template", "JRzFvYrmrVqtEYhpGFyQUQs" },
	{ "text_template", "wGKQs" }
};

CardSavrResponse<Notification> notification = await http.UpdateNotificationAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("name", "Sample Notification" )
	.add("type", "email" )
	.add("event", "merchant_site_updates_top" )
	.add("html_template", "JRzFvYrmrVqtEYhpGFyQUQs" )
	.add("text_template", "wGKQs" )
	.build();
JsonValue notification = session.put("/notifications", body, null, null);
```

```shell
curl -d "{\"name\":\"Sample Notification\",\"type\":\"email\",\"event\":\"merchant_site_updates_top\",\"config\":{\"recipient\":\"cardholder\",\"url\":null,\"from_email\":\"CardUpdatr <no-reply@cardupdatr.app>\",\"return_path\":\"no-reply@cardupdatr.app\",\"send_email_time\":null,\"interval_length\":null,\"interval_type\":null},\"html_template\":\"JRzFvYrmrVqtEYhpGFyQUQs\",\"text_template\":\"wGKQs\"}"
-X PUT -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/notifications/1437913716
```

### Path

PUT /notifications OR /notifications/{id}

### Description

Update a notification and return the updated object.  An id is required on every update request.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

### Body parameters

Parameter | Type | Description 
-------- | ---- | ---------
name | string | Name of this notification.
type | [string enum](#post-notification-1)* | Notification type (e.g. webhook or email).
event | [string enum](#post-notification-2)** | Event that will triger the notification (e.g. session complete).
config | object | 
html_template | string | Overrides the default CardUpdatr html email template (for email notifications).
text_template | string | Overrides the default CardUpdatr text email template (for email notifications).

See [notification response parameters](#response-notification).


## Delete notification

```shell
curl -X DELETE
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/notifications/1437913716
```

```javascript
await session.deleteNotification(undefined);
```

```csharp
CardSavrResponse<Notification> notification = await http.DeleteNotificationAsync(undefined);
```

```java
JsonValue notification = session.delete("/notifications", undefined, null);
```

### Path

DELETE /notifications/{id}

### Description

Delete a notification and purge its [related items](#cascading-delete).  An id is required on every delete request.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.


See [notification response parameters](#response-notification).


# Notification results
Notification result objects are records of an attempt/attempts to send a notification, indicating success/failure and additional relevant information.
## Get notification result

```javascript
const notificationresults = await session.getNotificationResults(1497801210,{"sort":"id","is_descending":true,"page":1, "page_length":25,{'x-cardsavr-hydration':JSON.stringify(["notification"])});
```

```csharp
Paging paging = new Paging() { PageLength = 100, IsDescending = true, Page = 1, Sort = "id" };
HttpRequestHeaders headers = new HttpRequestMessage().Headers;
string[] array = { "cardholder","merchant_site","cardsavr_card" };
var json = JsonConvert.SerializeObject(array);
headers.Add("x-cardsavr-hydration", json);
var query = new {ids = 1};
QueryDef qd = new QueryDef(query);
CardSavrResponse<NotificationResults> notificationresults = await session.GetNotificationResultsAsync(qd,paging,headers);
```

```java
Headers headers = session.createHeaders();
headers.paging = Json.createObjectBuilder().add("page", 1).add("page_length", 5).add("is_descending", true).add("sort", "id").build();
headers.hydration = {'x-cardsavr-hydration':JSON.stringify(["notification"])}
JsonArray response = (JsonArray)session.get(1497801210, null, headers);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 1497801210,
  "last_attempt_date": "1986-09-12T01:43:47.475Z",
  "fi_lookup_key": "ntkHRzftByxiYloibeFzjSXusDJobOVkRhAVGlZTWvFhYJRWChZHhkqnKplHkaI",
  "cuid": "rqQEGhekKVzRVDw",
  "status": "failure",
  "attempts": 1218123007,
  "notification_data": {
    "QGqhjHrHAvBT": "^@!K8$,hrHfDk",
    "OGiwelwvFFjS": 54,
    "gBaWbyIpfoZp": false
  },
  "created_on": "2007-09-14T05:14:51.558Z",
  "last_updated_on": "1977-01-01T20:44:00.867Z",
  "notification": {
    "id": 380005480,
    "name": "Sample Notification",
    "type": "email",
    "event": "webhook_error_summary",
    "config": {
      "recipient": "cardholder",
      "url": null,
      "from_email": "CardUpdatr <no-reply@cardupdatr.app>",
      "return_path": "no-reply@cardupdatr.app",
      "send_email_time": null,
      "interval_length": null,
      "interval_type": null
    },
    "html_template": "HlZGbRSObBygHzeSjwqombE",
    "text_template": "hoSEPer",
    "created_on": "1973-12-20T08:53:56.903Z",
    "last_updated_on": "1988-12-28T17:07:13.546Z"
  }
}
```

### Path

GET /notification_results **(batch)** or GET /notification_results/:id **(singular)**

### Description

Returns the notification result specified by the provided ID

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

#### Batch GET requests

**Batch requests** return the first page of all viewable notification results, filtered by any [query filters](#get-filters) (see list of possible parameters below) listed in the path.


### Filter parameters
- ids / id (in path)
- notification_ids
- last_attempt_date_min / last_attempt_date_max
- fi_lookup_keys
- cuid
- status
- attempts
- attempts_min / attempts_max
- created_on_min / created_on_max
- last_updated_on_min / last_updated_on_max

**Example batch GET request path:**<br>`/notification_results?ids=1,2`

#### Singular GET requests

**Singular requests** only return the notification result matching the id provided in the path.

**Example GET request path:**<br>`/notification_results/1497801210`

### <a name="response-notification_result"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number (pk) | Unique ID of this notification.
last_attempt_date | date | Date of last attempt to post this notification.
fi_lookup_key | string | FI lookup key associated with the attempted notification.
cuid | string | External unique ID for cardholder--can be account_id, email address, phone number, etc.  A random number will be gnenerated if not provided.
status | string | Status of the notification attempt.
attempts | number | Number of attempts made to send or post notification.
notification_data | object | Data sent with the notification.
created_on | date | Date this notification result was created on
last_updated_on | date | Date this notification result was last updated on
notification_id | number (fk) [notifications](#notifications) | ID of the attempted notification.

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

## Create notification result

```javascript
const notificationresult = await session.createNotificationResult({
  "notification_id": 1970768932,
  "fi_lookup_key": "ntkHRzftByxiYloibeFzjSXusDJobOVkRhAVGlZTWvFhYJRWChZHhkqnKplHkaI",
  "cuid": "rqQEGhekKVzRVDw",
  "status": "failure",
  "attempts": 1218123007,
  "notification_data": {
    "QGqhjHrHAvBT": "^@!K8$,hrHfDk",
    "OGiwelwvFFjS": 54,
    "gBaWbyIpfoZp": false
  }
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "notification_id", 1970768932 },
	{ "fi_lookup_key", "ntkHRzftByxiYloibeFzjSXusDJobOVkRhAVGlZTWvFhYJRWChZHhkqnKplHkaI" },
	{ "cuid", "rqQEGhekKVzRVDw" },
	{ "status", "failure" },
	{ "attempts", 1218123007 }
};

CardSavrResponse<NotificationResult> notificationresult = await http.CreateNotificationResultAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("notification_id", 1970768932 )
	.add("fi_lookup_key", "ntkHRzftByxiYloibeFzjSXusDJobOVkRhAVGlZTWvFhYJRWChZHhkqnKplHkaI" )
	.add("cuid", "rqQEGhekKVzRVDw" )
	.add("status", "failure" )
	.add("attempts", 1218123007 )
	.build();
JsonValue notificationresult = session.post("/notification_results", body, null, null);
```

```shell
curl -d "{\"notification_id\":1970768932,\"fi_lookup_key\":\"ntkHRzftByxiYloibeFzjSXusDJobOVkRhAVGlZTWvFhYJRWChZHhkqnKplHkaI\",\"cuid\":\"rqQEGhekKVzRVDw\",\"status\":\"failure\",\"attempts\":1218123007,\"notification_data\":{\"QGqhjHrHAvBT\":\"^@!K8$,hrHfDk\",\"OGiwelwvFFjS\":54,\"gBaWbyIpfoZp\":false}}"
-X POST -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/notification_results/
```

### Path

POST /notification_results

### Description

Create a notification result and return the created object.

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

### Body parameters

Parameter | Type | Required | Description
-------- | ---- | --------- | ----------
notification_id | number | yes | ID of the attempted notification.
fi_lookup_key | string | yes | FI lookup key associated with the attempted notification.
cuid | string | yes | External unique ID for cardholder--can be account_id, email address, phone number, etc.  A random number will be gnenerated if not provided.
status | [string enum](#post-notification_result-1)* | yes | Status of the notification attempt.
attempts | number | yes | Number of attempts made to send or post notification.
notification_data | object | no | Data sent with the notification.

See [notification result response attributes](#response-notification_result).

#### <a name="post-notification_result-1"></a>string enum*
- success
- failure

# Single-site jobs
Single-site job objects contain the information necessary to place a payment card on a merchant site, as well as status information about the card placement attempt. They are linked to a single cardholder, account, card, and merchant site.
## Get single-site job

```javascript
const singlesitejobs = await session.getSingleSiteJobs(2035432543,{"sort":"id","is_descending":true,"page":1, "page_length":25,{'x-cardsavr-hydration':JSON.stringify(["cardholder","cardsavr_card","cardsavr_account","credential_requests"])});
```

```csharp
Paging paging = new Paging() { PageLength = 100, IsDescending = true, Page = 1, Sort = "id" };
HttpRequestHeaders headers = new HttpRequestMessage().Headers;
string[] array = { "cardholder","merchant_site","cardsavr_card" };
var json = JsonConvert.SerializeObject(array);
headers.Add("x-cardsavr-hydration", json);
var query = new {ids = 1};
QueryDef qd = new QueryDef(query);
CardSavrResponse<SingleSiteJobs> singlesitejobs = await session.GetSingleSiteJobsAsync(qd,paging,headers);
```

```java
Headers headers = session.createHeaders();
headers.paging = Json.createObjectBuilder().add("page", 1).add("page_length", 5).add("is_descending", true).add("sort", "id").build();
headers.hydration = {'x-cardsavr-hydration':JSON.stringify(["cardholder","cardsavr_card","cardsavr_account","credential_requests"])}
JsonArray response = (JsonArray)session.get(2035432543, null, headers);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 2035432543,
  "status": "INITIATED",
  "status_message": "TyteZuaDcNtNPiIQgCytvuEjZgeGlGJI",
  "termination_type": "USER_DATA_FAILURE",
  "custom_data": {
    "oDepnzVonxbu": "v[dAC4po=.uCM=Hhv,xaI%F@j%DR6i!J",
    "gEEimTAkgyfD": 78,
    "KmxBjhKLoYxc": true
  },
  "notification_sent": true,
  "time_elapsed": 1742483631,
  "auth_percent_complete": 1081565246,
  "percent_complete": 736081701,
  "started_on": "1982-12-17T03:00:55.403Z",
  "completed_on": "2006-11-22T06:04:43.127Z",
  "created_on": "1982-06-27T04:19:32.883Z",
  "last_updated_on": "2022-02-22T13:03:23.980Z",
  "cardholder": {
    "id": 1308093874,
    "type": "persistent_creds",
    "first_name": "Jane",
    "last_name": "Smith",
    "email": "test_email@strivve.com",
    "meta_key": "kkXShhMhTGylTdkIodKSSfoapAov",
    "webhook_url": "https://mywebhooks.com/this",
    "custom_data": {
      "lvhnXNQWvTHo": "6COnA_Oo",
      "lnTWReigYRvA": 44,
      "WSYREzVnaaeV": true
    },
    "created_on": "1988-01-27T03:05:31.514Z",
    "last_updated_on": "2000-08-19T06:27:25.562Z",
    "cuid": "UJi",
    "source": {
      "type": "alert",
      "category": "other",
      "sub_category": "ei(/OVu$",
      "device": "mobile app",
      "integration": "CS"
    }
  },
  "cardsavr_card": {
    "id": 1585351781,
    "type": "American Express",
    "expiration_month": 12,
    "expiration_year": 24,
    "name_on_card": "Jane Smith",
    "last_4": "VkzZ",
    "nickname": "Jane's VISA",
    "custom_data": {
      "ZsmNZQNOQFTX": "M.$",
      "PCxHcAIPEbDh": 38,
      "BodKcCJUchVh": false
    },
    "created_on": "1976-05-28T01:29:39.786Z",
    "last_updated_on": "2007-06-14T16:31:55.949Z",
    "par": "XzVxHufJWpyhCrlypjpgaCywRhPOA",
    "customer_key": "PzuhiJbhv"
  },
  "cardsavr_account": {
    "id": 573293468,
    "last_password_update": "2002-11-11T08:10:39.484Z",
    "last_saved_card": "1991-02-19T19:57:06.767Z",
    "created_on": "1996-03-23T08:26:01.513Z",
    "last_updated_on": "2016-03-23T10:00:30.212Z",
    "customer_key": "RNZDSVKGlBhrFjTiPJxnPIBCJ"
  },
  "credential_timeout": 941874093
}
```

### Path

GET /place_card_on_single_site_jobs **(batch)** or GET /place_card_on_single_site_jobs/:id **(singular)**

### Description

Returns the single-site job specified by the provided ID

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

#### Batch GET requests

**Batch requests** return the first page of all viewable single-site jobs, filtered by any [query filters](#get-filters) (see list of possible parameters below) listed in the path.


### Filter parameters
- ids / id (in path)
- cardholder_ids
- card_ids
- account_ids
- status
- status_include / status_exclude
- termination_type
- termination_types_include / termination_types_exclude
- notification_sent
- time_elapsed_min / time_elapsed_max
- started_on_min / started_on_max
- completed_on_min / completed_on_max
- created_on_min / created_on_max
- last_updated_on_min / last_updated_on_max

**Example batch GET request path:**<br>`/place_card_on_single_site_jobs?ids=1,2`

#### Singular GET requests

**Singular requests** only return the single-site job matching the id provided in the path.

**Example GET request path:**<br>`/place_card_on_single_site_jobs/2035432543`

To hydrate all credential requests currently associated with a job, include credential_requests in the hydration header (see example at right).`

### <a name="response-place_card_on_single_site_job"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number (pk) | Unique ID of this job.
card_id | number (fk) [cards](#cards) | ID of card associated with this job.
status | string | Current status of job (e.g. pending_tfa). These names are dynamic and change frequently, so it is best to use status_message to communicate with cardholders.
status_message | string | Human readable representation of the job's status.
termination_type | string | Final termination status of a job. (BILLABLE, SITE_INTERACTION_FAILURE, USER_DATA_FAILURE, PROCESS FAILURE)
custom_data | object | 
notification_sent | boolean | Indicates if a notification has been sent or posted for this job.
time_elapsed | number | Amount of time elapsed since the creation of the job.
auth_percent_complete | number | Percentage this job has progressed toward account link.
percent_complete | number | Percentage this job has progressed toward full card placement.
started_on | date | Time when job started.
completed_on | date | Timestamp of job completion.
created_on | date | Date this site was created on
last_updated_on | date | Date this site was last updated on
cardholder_id | number (fk) [cardholders](#cardholders) | ID of cardholder associated with this job.
account_id | number (fk) [accounts](#accounts) | ID of account associated with this job.
credential_timeout | number | Credential timeout value in seconds.

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

## Create single-site job

```javascript
const singlesitejob = await session.createSingleSiteJob({
  "cardholder_id": 1324527895,
  "card_id": 43704002,
  "account_id": 1995054453,
  "status": "INITIATED",
  "custom_data": {
    "oDepnzVonxbu": "v[dAC4po=.uCM=Hhv,xaI%F@j%DR6i!J",
    "gEEimTAkgyfD": 78,
    "KmxBjhKLoYxc": true
  },
  "notification_sent": true,
  "time_elapsed": 1742483631,
  "credential_timeout": 941874093,
  "auth_percent_complete": 1081565246,
  "percent_complete": 736081701,
  "started_on": "1982-12-17T03:00:55.403Z",
  "completed_on": "2006-11-22T06:04:43.127Z"
}, CARDHOLDER_SAFE_KEY);
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "cardholder_id", 1324527895 },
	{ "card_id", 43704002 },
	{ "account_id", 1995054453 },
	{ "status", "INITIATED" },
	{ "notification_sent", true },
	{ "time_elapsed", 1742483631 },
	{ "credential_timeout", 941874093 },
	{ "auth_percent_complete", 1081565246 },
	{ "percent_complete", 736081701 },
	{ "started_on", "1982-12-17T03:00:55.403Z" },
	{ "completed_on", "2006-11-22T06:04:43.127Z" }
};

CardSavrResponse<SingleSiteJob> singlesitejob = await http.CreateSingleSiteJobAsync(body, CARDHOLDER_SAFE_KEY);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("cardholder_id", 1324527895 )
	.add("card_id", 43704002 )
	.add("account_id", 1995054453 )
	.add("status", "INITIATED" )
	.add("notification_sent", true )
	.add("time_elapsed", 1742483631 )
	.add("credential_timeout", 941874093 )
	.add("auth_percent_complete", 1081565246 )
	.add("percent_complete", 736081701 )
	.add("started_on", "1982-12-17T03:00:55.403Z" )
	.add("completed_on", "2006-11-22T06:04:43.127Z" )
	.build();
JsonValue singlesitejob = session.post("/place_card_on_single_site_jobs", body, null, null);
```

```shell
curl -d "{\"cardholder_id\":1324527895,\"card_id\":43704002,\"account_id\":1995054453,\"status\":\"INITIATED\",\"custom_data\":{\"oDepnzVonxbu\":\"v[dAC4po=.uCM=Hhv,xaI%F@j%DR6i!J\",\"gEEimTAkgyfD\":78,\"KmxBjhKLoYxc\":true},\"notification_sent\":true,\"time_elapsed\":1742483631,\"credential_timeout\":941874093,\"auth_percent_complete\":1081565246,\"percent_complete\":736081701,\"started_on\":\"1982-12-17T03:00:55.403Z\",\"completed_on\":\"2006-11-22T06:04:43.127Z\"}"
-X POST -H "Content-Type: application/json"
-H "x-cardsavr-cardholder-safe-key: CARDHOLDER_SAFE_KEY"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/place_card_on_single_site_jobs/
```

### Path

POST /place_card_on_single_site_jobs

### Description

Create a single-site job and return the created object.

### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.



<aside class="notice"><a href=#request-hydration-on-post>Request hydration</a> can be used on this endpoint. This allows you to create a new single-site job and all referential entities in a single POST request.
</aside>

### Body parameters

Parameter | Type | Required | Description
-------- | ---- | --------- | ----------
cardholder_id | number | yes | ID of cardholder associated with this job.
card_id | number | yes | ID of card associated with this job.
account_id | number | yes | ID of account associated with this job.
status | [string enum](#post-place_card_on_single_site_job-1)* | no | Current status of job (e.g. pending_tfa). These names are dynamic and change frequently, so it is best to use status_message to communicate with cardholders.
custom_data | object | no | 
notification_sent | boolean | no | Indicates if a notification has been sent or posted for this job.
time_elapsed | number | no | Amount of time elapsed since the creation of the job.
credential_timeout | number | no | Credential timeout value in seconds.
auth_percent_complete | number | no | Percentage this job has progressed toward account link.
percent_complete | number | no | Percentage this job has progressed toward full card placement.
started_on | date | no | Time when job started.
completed_on | date | no | Timestamp of job completion.

See [single-site job response attributes](#response-place_card_on_single_site_job).

#### <a name="post-place_card_on_single_site_job-1"></a>string enum*
- INITIATED
- REQUESTED
- IN_PROGRESS
- AUTH
- LOGIN_SUBMITTED
- CREDS_RECEIVED
- TFA_CODE_RECEIVED
- TFA_SUBMITTED
- SUBMITTED
- PENDING_NEWCREDS
- PENDING_TFA
- PENDING_TFA_MESSAGE
- PENDING
- UPDATING
- QUEUED
- SITE_BLOCKED
- CANCEL_REQUESTED
- CANCELED
- JOB_RECORD_DELETED
- ABANDONED
- ABANDONED_QUICKSTART
- KILLED
- ACCOUNT_SETUP_INCOMPLETE
- ACCOUNT_NOT_SUPPORTED
- TFA_NOT_SUPPORTED
- PREPAID_ACCOUNT
- INACTIVE_ACCOUNT
- MISSING_CARD_DATA
- CARD_FORM_FAILED
- UNEXPECTED_ERROR
- INVALID_CARD_DETAILS
- INVALID_CARD_TYPE
- MULTI_ACCOUNT_CARD_NOT_ALLOWED
- INVALID_ADDRESS
- PASSWORD_RESET_REQUIRED
- BUNDLED_SUBSCRIPTION
- FREE_ACCOUNT
- ACCOUNT_LOCKED
- INVALID_EXPIRATION_DATE
- EXPIRED_CARD
- INVALID_CVV
- INVALID_NETWORK
- MAX_LIMIT_OF_STORED_CARDS
- PAYMENT_PROCESSOR_DOWN
- DUPLICATE_CARD
- TEST_COMPLETE_SUCCESS
- SUCCESSFUL
- UNSUPPORTED_CAPTCHA
- TIMEOUT_CAPTCHA
- TIMEOUT_CREDENTIALS
- MISSING_CREDENTIALS
- TIMEOUT_TFA
- TOO_MANY_LOGIN_FAILURES
- TOO_MANY_TFA_FAILURES
- TOO_MANY_OTP_FAILURES
- INVALID_SECURITY_ANSWERS
- INVALID_CREDENTIAL_REQUEST_TYPE
- UNSUCCESSFUL
- PROXY_PROBE_FAILED
- VBS_TIMEOUT
- VBS_ERROR
- UNKNOWN_INTERFACE_TYPE
- UNIMPLEMENTED_JOB_TYPE
- UNKNOWN_JOB_TYPE
- INTERNAL_ERROR
- ACCOUNT_NOT_FOUND
- MERCHANT_SECURITY_NOT_IMPLEMENTED
- MERCHANT_PROCESSOR_NOT_IMPLEMENTED
- WALLET_PROCESSOR_NOT_IMPLEMENTED

#### <a name="post-place_card_on_single_site_job-2"></a>string enum**
- USER_DATA_FAILURE
- PROCESS_FAILURE
- SITE_INTERACTION_FAILURE
- BILLABLE
- NEVER_STARTED

<aside class="notice">Update calls to /place_card_on_single_site_jobs require the cardholder's personal cardholder_safe_key header to encrypt and save the safe when Strivve does not manage keys for a customer (this is an environment setting). The safe keys are also not required if updating non-safe user properties.</aside>

## Update single-site job

```javascript
const singlesitejob = await session.updateSingleSiteJob(1,{
  "card_id": 314542492,
  "status": "MISSING_CARD_DATA",
  "custom_data": {
    "bJrcYKxaTrcX": "7m~V2uL+,rqK",
    "javgUKKiugNJ": 81,
    "QBbTNEEoCKWI": true
  },
  "notification_sent": false,
  "time_elapsed": 673694121,
  "auth_percent_complete": 1925619588,
  "percent_complete": 2145603628,
  "started_on": "2008-06-13T09:34:24.017Z",
  "completed_on": "2018-07-13T17:55:41.974Z"
}, CARDHOLDER_SAFE_KEY);
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "card_id", 314542492 },
	{ "status", "MISSING_CARD_DATA" },
	{ "notification_sent", false },
	{ "time_elapsed", 673694121 },
	{ "auth_percent_complete", 1925619588 },
	{ "percent_complete", 2145603628 },
	{ "started_on", "2008-06-13T09:34:24.017Z" },
	{ "completed_on", "2018-07-13T17:55:41.974Z" }
};

CardSavrResponse<SingleSiteJob> singlesitejob = await http.UpdateSingleSiteJobAsync(body, CARDHOLDER_SAFE_KEY);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("card_id", 314542492 )
	.add("status", "MISSING_CARD_DATA" )
	.add("notification_sent", false )
	.add("time_elapsed", 673694121 )
	.add("auth_percent_complete", 1925619588 )
	.add("percent_complete", 2145603628 )
	.add("started_on", "2008-06-13T09:34:24.017Z" )
	.add("completed_on", "2018-07-13T17:55:41.974Z" )
	.build();
JsonValue singlesitejob = session.put("/place_card_on_single_site_jobs", body, null, null);
```

```shell
curl -d "{\"card_id\":314542492,\"status\":\"MISSING_CARD_DATA\",\"custom_data\":{\"bJrcYKxaTrcX\":\"7m~V2uL+,rqK\",\"javgUKKiugNJ\":81,\"QBbTNEEoCKWI\":true},\"notification_sent\":false,\"time_elapsed\":673694121,\"auth_percent_complete\":1925619588,\"percent_complete\":2145603628,\"started_on\":\"2008-06-13T09:34:24.017Z\",\"completed_on\":\"2018-07-13T17:55:41.974Z\"}"
-X PUT -H "Content-Type: application/json"
-H "cardholder-safe-key: CARDHOLDER_SAFE_KEY"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/place_card_on_single_site_jobs/2035432543
```

### Path

PUT /place_card_on_single_site_jobs OR /place_card_on_single_site_jobs/{id}

### Description

Update a single-site job and return the updated object.  An id is required on every update request.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.

### Body parameters

Parameter | Type | Description 
-------- | ---- | ---------
card_id | number | ID of card associated with this job.
status | [string enum](#post-place_card_on_single_site_job-1)* | Current status of job (e.g. pending_tfa). These names are dynamic and change frequently, so it is best to use status_message to communicate with cardholders.
custom_data | object | 
notification_sent | boolean | Indicates if a notification has been sent or posted for this job.
time_elapsed | number | Amount of time elapsed since the creation of the job.
auth_percent_complete | number | Percentage this job has progressed toward account link.
percent_complete | number | Percentage this job has progressed toward full card placement.
started_on | date | Time when job started.
completed_on | date | Timestamp of job completion.

See [single-site job response parameters](#response-place_card_on_single_site_job).

<aside class="notice">Update calls to /place_card_on_single_site_jobs require the cardholder's personal cardholder_safe_key header to encrypt and save the safe when Strivve does not manage keys for a customer (this is an environment setting). The safe keys are also not required if updating non-safe properties.</aside>

## Delete single-site job

```shell
curl -X DELETE
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" 
https://api.INSTANCE.cardsavr.io/place_card_on_single_site_jobs/2035432543
```

```javascript
await session.deleteSingleSiteJob(undefined);
```

```csharp
CardSavrResponse<SingleSiteJob> singlesitejob = await http.DeleteSingleSiteJobAsync(undefined);
```

```java
JsonValue singlesitejob = session.delete("/place_card_on_single_site_jobs", undefined, null);
```

### Path

DELETE /place_card_on_single_site_jobs/{id}

### Description

Delete a single-site job and purge its [related items](#cascading-delete).  An id is required on every delete request.



### SDK Usage
 Please visit the <a href="https://github.com/swch/Strivve-SDK">javascript</a>, <a href="https://github.com/swch/metro_sdk_c_sharp">c sharp</a>, and <a href="https://github.com/swch/strivve-sdk-java">java</a> SDKs for further examples and information on SDK usage.


See [single-site job response parameters](#response-place_card_on_single_site_job).

