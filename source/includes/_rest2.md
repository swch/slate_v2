
# Accounts
An account object contains a CardSavr user's account information for a specific merchant site.
## Get account

```shell
curl -H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/cardsavr_accounts/1815938555
```

```javascript
const accounts = await session.getAccounts(1815938555);
```

```csharp
CardSavrResponse<Accounts> accounts = await session.GetAccountsAsync(1815938555);
```

```java
JsonValue accounts = session.get("/cardsavr_accounts", 1815938555, null, null);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 1815938555,
  "last_card_placed_id": 2140936059,
  "last_login": "1970-04-24T12:05:27.032Z",
  "last_password_update": "2014-05-10T18:30:32.910Z",
  "last_saved_card": "2002-04-23T00:57:12.741Z",
  "created_on": "2007-12-18T14:13:06.990Z",
  "last_updated_on": "2015-12-13T15:57:21.518Z",
  "cardholder_id": 1307832262,
  "merchant_site_id": 265568938
}
```

### Path

GET /cardsavr_accounts **(batch)** or GET /cardsavr_accounts/:id **(singular)**

### Description

Returns the account specified by the provided ID

#### Batch GET requests

**Batch requests** return the first page of all viewable accounts, filtered by any [query filters](#get-filters) listed in the path.

**Example batch GET request path:**<br>`/cardsavr_accounts?ids=1,2`

#### Singular GET requests

**Singular requests** only return the account matching the id provided in the path.

**Example GET request path:**<br>`/cardsavr_accounts/1815938555`

### <a name="response-cardsavr_account"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number | 
last_card_placed_id | number (fk) | 
last_login | date | 
last_password_update | date | 
last_saved_card | date | 
created_on | date | Date this site was created on
last_updated_on | date | Date this site was last updated on
cardholder_id | number (fk) | 
merchant_site_id | number (fk) | 

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

### Filter parameters
- ids / id (in path)
- cardholder_ids
- merchant_site_ids
- last_card_placed_ids
- last_login_min / last_login_max
- last_password_update_min / last_password_update_max
- last_saved_card_min / last_saved_card_max
- created_on_min / created_on_max
- last_updated_on_min / last_updated_on_max

## Create account

```javascript
const account = await session.createAccount({
  "cardholder_id": 1307832262,
  "merchant_site_id": 265568938,
  "last_card_placed_id": 2140936059,
  "username": "jsmith123",
  "password": "BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI="
}, CARDHOLDER_SAFE_KEY);
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "cardholder_id", 1307832262 },
	{ "merchant_site_id", 265568938 },
	{ "last_card_placed_id", 2140936059 },
	{ "username", "jsmith123" },
	{ "password", "BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI=" }
};

CardSavrResponse<Account> account = await http.CreateAccountAsync(body, CARDHOLDER_SAFE_KEY);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("cardholder_id", 1307832262 )
	.add("merchant_site_id", 265568938 )
	.add("last_card_placed_id", 2140936059 )
	.add("username", "jsmith123" )
	.add("password", "BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI=" )
	.build();
JsonValue account = session.post("/cardsavr_accounts", body, null, null);
```

```shell
curl -d "{\"cardholder_id\":1307832262,\"merchant_site_id\":265568938,\"last_card_placed_id\":2140936059,\"username\":\"jsmith123\",\"password\":\"BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI=\"}"
-X POST -H "Content-Type: application/json"
-H "x-cardsavr-cardholder-safe-key: CARDHOLDER_SAFE_KEY"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/cardsavr_accounts/
```

### Path

POST /cardsavr_accounts

### Description

Create a account and return the created object.

### Body parameters

Parameter | Type | Required | Description
-------- | ---- | --------- | ----------
cardholder_id | number | yes
merchant_site_id | number | yes
last_card_placed_id | number | no
username | string | no
password | string | no

See [account response attributes](#response-cardsavr_account).

<aside class="notice">Update calls to /cardsavr_accounts require the cardholder's personal cardholder_safe_key header to encrypt and save the username and password when Strivve does not manage keys for a customer (this is an environment setting). The safe keys are also not required if updating non-safe user properties.</aside>

## Update account

```javascript
const account = await session.updateAccount(1,{
  "last_card_placed_id": 2089216499,
  "username": "jsmith123",
  "password": "BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI="
}, null, CARDHOLDER_SAFE_KEY);
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "last_card_placed_id", 2089216499 },
	{ "username", "jsmith123" },
	{ "password", "BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI=" }
};

CardSavrResponse<Account> account = await http.UpdateAccountAsync(body, CARDHOLDER_SAFE_KEY);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("last_card_placed_id", 2089216499 )
	.add("username", "jsmith123" )
	.add("password", "BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI=" )
	.build();
JsonValue account = session.put("/cardsavr_accounts", body, null, null);
```

```shell
curl -d "{\"last_card_placed_id\":2089216499,\"username\":\"jsmith123\",\"password\":\"BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI=\"}"
-X PUT -H "Content-Type: application/json"
-H "cardholder-safe-key: CARDHOLDER_SAFE_KEY"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/cardsavr_accounts/1815938555
```

### Path

PUT /cardsavr_accounts OR /cardsavr_accounts/{id}

### Description

Update a account and return the updated object.  An id is required on every update request.

### Body parameters

Parameter | Type | Description 
-------- | ---- | ---------
last_card_placed_id | number |
username | string |
password | string |

See [account response parameters](#response-cardsavr_account).

<aside class="notice">Update calls to /cardsavr_accounts require the cardholder's personal cardholder_safe_key header to encrypt and save the username and password when Strivve does not manage keys for a customer (this is an environment setting). The safe keys are also not required if updating non-safe properties.</aside>

## Delete account

```shell
curl -X DELETE
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/cardsavr_accounts/1815938555
```

```javascript
await session.deleteAccount(1815938555);
```

```csharp
CardSavrResponse<Account> account = await http.DeleteAccountAsync(1815938555);
```

```java
JsonValue account = session.delete("/cardsavr_accounts", 1815938555, null);
```

### Path

DELETE /cardsavr_accounts/{id}

### Description

Delete a account and purge its [related items](#cascading-delete).  An id is required on every delete request.

See [account response parameters](#response-cardsavr_account).


# Addresses
Address objects contain billing address information for a particular user.
## Get address

```shell
curl -H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/cardsavr_addresses/1796377327
```

```javascript
const addresses = await session.getAddresses(1796377327);
```

```csharp
CardSavrResponse<Addresses> addresses = await session.GetAddressesAsync(1796377327);
```

```java
JsonValue addresses = session.get("/cardsavr_addresses", 1796377327, null, null);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 1796377327,
  "address1": "KTHmutKiBxZYtNsdSDVZJeJChQvVMokfUKZOrcndaHKtLGpZZboyHHgIkUgDNUxhDwuiKagUMjTTpYiUIbQjOTySGrdIbIiBDLM",
  "address2": "nayXHhKITsNGeXZpVqReKmcySJjzDyQmsvLOoCJYDjNiWoCZfyGGWEgaFWBgcsglzlPLhWiHTxKRmGvxTEhWQfprrUQFSwScesl",
  "city": "Seattle",
  "subnational": "WA",
  "postal_code": "98177",
  "postal_other": "98177-0124",
  "country": "USA",
  "is_primary": false,
  "first_name": "Joe",
  "last_name": "Smith",
  "email": "test_email@strivve.com",
  "phone_number": "cLcxujIdiGICthQXnSjAjdWxadcoC",
  "created_on": "1983-09-09T20:38:15.606Z",
  "last_updated_on": "1988-12-07T05:39:55.556Z",
  "cardholder_id": 243166541
}
```

### Path

GET /cardsavr_addresses **(batch)** or GET /cardsavr_addresses/:id **(singular)**

### Description

Returns the address specified by the provided ID

#### Batch GET requests

**Batch requests** return the first page of all viewable addresses, filtered by any [query filters](#get-filters) listed in the path.

**Example batch GET request path:**<br>`/cardsavr_addresses?ids=1,2`

#### Singular GET requests

**Singular requests** only return the address matching the id provided in the path.

**Example GET request path:**<br>`/cardsavr_addresses/1796377327`

### <a name="response-cardsavr_address"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number | 
address1 | string | 
address2 | string | 
city | string | 
subnational | string | 
postal_code | string | 
postal_other | string | 
country | string | 
is_primary | boolean | 
first_name | string | 
last_name | string | 
email | string | 
phone_number | string | 
created_on | date | Date this site was created on
last_updated_on | date | Date this site was last updated on
cardholder_id | number (fk) | 

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

### Filter parameters
- ids / id (in path)
- cardholder_ids
- is_primary
- first_name
- last_name
- email
- created_on_min / created_on_max
- last_updated_on_min / last_updated_on_max

## Create address

```javascript
const address = await session.createAddress({
  "cardholder_id": 243166541,
  "address1": "KTHmutKiBxZYtNsdSDVZJeJChQvVMokfUKZOrcndaHKtLGpZZboyHHgIkUgDNUxhDwuiKagUMjTTpYiUIbQjOTySGrdIbIiBDLM",
  "address2": "nayXHhKITsNGeXZpVqReKmcySJjzDyQmsvLOoCJYDjNiWoCZfyGGWEgaFWBgcsglzlPLhWiHTxKRmGvxTEhWQfprrUQFSwScesl",
  "city": "Seattle",
  "subnational": "WA",
  "postal_code": "98177",
  "postal_other": "98177-0124",
  "country": "USA",
  "is_primary": false,
  "first_name": "Joe",
  "last_name": "Smith",
  "email": "test_email@strivve.com",
  "phone_number": "cLcxujIdiGICthQXnSjAjdWxadcoC"
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "cardholder_id", 243166541 },
	{ "address1", "KTHmutKiBxZYtNsdSDVZJeJChQvVMokfUKZOrcndaHKtLGpZZboyHHgIkUgDNUxhDwuiKagUMjTTpYiUIbQjOTySGrdIbIiBDLM" },
	{ "address2", "nayXHhKITsNGeXZpVqReKmcySJjzDyQmsvLOoCJYDjNiWoCZfyGGWEgaFWBgcsglzlPLhWiHTxKRmGvxTEhWQfprrUQFSwScesl" },
	{ "city", "Seattle" },
	{ "subnational", "WA" },
	{ "postal_code", "98177" },
	{ "postal_other", "98177-0124" },
	{ "country", "USA" },
	{ "is_primary", false },
	{ "first_name", "Joe" },
	{ "last_name", "Smith" },
	{ "email", "test_email@strivve.com" },
	{ "phone_number", "cLcxujIdiGICthQXnSjAjdWxadcoC" }
};

CardSavrResponse<Address> address = await http.CreateAddressAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("cardholder_id", 243166541 )
	.add("address1", "KTHmutKiBxZYtNsdSDVZJeJChQvVMokfUKZOrcndaHKtLGpZZboyHHgIkUgDNUxhDwuiKagUMjTTpYiUIbQjOTySGrdIbIiBDLM" )
	.add("address2", "nayXHhKITsNGeXZpVqReKmcySJjzDyQmsvLOoCJYDjNiWoCZfyGGWEgaFWBgcsglzlPLhWiHTxKRmGvxTEhWQfprrUQFSwScesl" )
	.add("city", "Seattle" )
	.add("subnational", "WA" )
	.add("postal_code", "98177" )
	.add("postal_other", "98177-0124" )
	.add("country", "USA" )
	.add("is_primary", false )
	.add("first_name", "Joe" )
	.add("last_name", "Smith" )
	.add("email", "test_email@strivve.com" )
	.add("phone_number", "cLcxujIdiGICthQXnSjAjdWxadcoC" )
	.build();
JsonValue address = session.post("/cardsavr_addresses", body, null, null);
```

```shell
curl -d "{\"cardholder_id\":243166541,\"address1\":\"KTHmutKiBxZYtNsdSDVZJeJChQvVMokfUKZOrcndaHKtLGpZZboyHHgIkUgDNUxhDwuiKagUMjTTpYiUIbQjOTySGrdIbIiBDLM\",\"address2\":\"nayXHhKITsNGeXZpVqReKmcySJjzDyQmsvLOoCJYDjNiWoCZfyGGWEgaFWBgcsglzlPLhWiHTxKRmGvxTEhWQfprrUQFSwScesl\",\"city\":\"Seattle\",\"subnational\":\"WA\",\"postal_code\":\"98177\",\"postal_other\":\"98177-0124\",\"country\":\"USA\",\"is_primary\":false,\"first_name\":\"Joe\",\"last_name\":\"Smith\",\"email\":\"test_email@strivve.com\",\"phone_number\":\"cLcxujIdiGICthQXnSjAjdWxadcoC\"}"
-X POST -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/cardsavr_addresses/
```

### Path

POST /cardsavr_addresses

### Description

Create a address and return the created object.

### Body parameters

Parameter | Type | Required | Description
-------- | ---- | --------- | ----------
cardholder_id | number | yes
address1 | string | yes
address2 | string | no
city | string | yes
subnational | string | yes
postal_code | string | yes
postal_other | string | no
country | string | no
is_primary | boolean | yes
first_name | string | no
last_name | string | no
email | string | no
phone_number | string | no

See [address response attributes](#response-cardsavr_address).


## Update address

```javascript
const address = await session.updateAddress(1,{
  "address1": "xPrLOwNbkfIExrlHnLnyTqTfeLDNQSPgPMcMRlroQJyLrriqpSFazoyvjimWhgBFzWltXDXflIexXupYYwnIiNEXEborMVIblqU",
  "address2": "KLhRYXLOvXyCxhFbeNoPjOPrXeVfEUismbmRncxNzsYRDAYiwTiWhWuegcysfmCaABfBMQMylhNJVEuicmnVmqysHZNBlNSiIgV",
  "city": "Seattle",
  "subnational": "WA",
  "postal_code": "98177",
  "postal_other": "98177-0124",
  "country": "USA",
  "is_primary": false,
  "first_name": "Joe",
  "last_name": "Smith",
  "email": "test_email@strivve.com",
  "phone_number": "lddwcHctIXjOqkgkAJlsVChTyJais"
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "address1", "xPrLOwNbkfIExrlHnLnyTqTfeLDNQSPgPMcMRlroQJyLrriqpSFazoyvjimWhgBFzWltXDXflIexXupYYwnIiNEXEborMVIblqU" },
	{ "address2", "KLhRYXLOvXyCxhFbeNoPjOPrXeVfEUismbmRncxNzsYRDAYiwTiWhWuegcysfmCaABfBMQMylhNJVEuicmnVmqysHZNBlNSiIgV" },
	{ "city", "Seattle" },
	{ "subnational", "WA" },
	{ "postal_code", "98177" },
	{ "postal_other", "98177-0124" },
	{ "country", "USA" },
	{ "is_primary", false },
	{ "first_name", "Joe" },
	{ "last_name", "Smith" },
	{ "email", "test_email@strivve.com" },
	{ "phone_number", "lddwcHctIXjOqkgkAJlsVChTyJais" }
};

CardSavrResponse<Address> address = await http.UpdateAddressAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("address1", "xPrLOwNbkfIExrlHnLnyTqTfeLDNQSPgPMcMRlroQJyLrriqpSFazoyvjimWhgBFzWltXDXflIexXupYYwnIiNEXEborMVIblqU" )
	.add("address2", "KLhRYXLOvXyCxhFbeNoPjOPrXeVfEUismbmRncxNzsYRDAYiwTiWhWuegcysfmCaABfBMQMylhNJVEuicmnVmqysHZNBlNSiIgV" )
	.add("city", "Seattle" )
	.add("subnational", "WA" )
	.add("postal_code", "98177" )
	.add("postal_other", "98177-0124" )
	.add("country", "USA" )
	.add("is_primary", false )
	.add("first_name", "Joe" )
	.add("last_name", "Smith" )
	.add("email", "test_email@strivve.com" )
	.add("phone_number", "lddwcHctIXjOqkgkAJlsVChTyJais" )
	.build();
JsonValue address = session.put("/cardsavr_addresses", body, null, null);
```

```shell
curl -d "{\"address1\":\"xPrLOwNbkfIExrlHnLnyTqTfeLDNQSPgPMcMRlroQJyLrriqpSFazoyvjimWhgBFzWltXDXflIexXupYYwnIiNEXEborMVIblqU\",\"address2\":\"KLhRYXLOvXyCxhFbeNoPjOPrXeVfEUismbmRncxNzsYRDAYiwTiWhWuegcysfmCaABfBMQMylhNJVEuicmnVmqysHZNBlNSiIgV\",\"city\":\"Seattle\",\"subnational\":\"WA\",\"postal_code\":\"98177\",\"postal_other\":\"98177-0124\",\"country\":\"USA\",\"is_primary\":false,\"first_name\":\"Joe\",\"last_name\":\"Smith\",\"email\":\"test_email@strivve.com\",\"phone_number\":\"lddwcHctIXjOqkgkAJlsVChTyJais\"}"
-X PUT -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/cardsavr_addresses/1796377327
```

### Path

PUT /cardsavr_addresses OR /cardsavr_addresses/{id}

### Description

Update a address and return the updated object.  An id is required on every update request.

### Body parameters

Parameter | Type | Description 
-------- | ---- | ---------
address1 | string |
address2 | string |
city | string |
subnational | string |
postal_code | string |
postal_other | string |
country | string |
is_primary | boolean |
first_name | string |
last_name | string |
email | string |
phone_number | string |

See [address response parameters](#response-cardsavr_address).


## Delete address

```shell
curl -X DELETE
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/cardsavr_addresses/1796377327
```

```javascript
await session.deleteAddress(1796377327);
```

```csharp
CardSavrResponse<Address> address = await http.DeleteAddressAsync(1796377327);
```

```java
JsonValue address = session.delete("/cardsavr_addresses", 1796377327, null);
```

### Path

DELETE /cardsavr_addresses/{id}

### Description

Delete a address and purge its [related items](#cascading-delete).  An id is required on every delete request.

See [address response parameters](#response-cardsavr_address).


# Bins
A cardsavr_bin object
## Get bin

```shell
curl -H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/cardsavr_bins/396838717
```

```javascript
const bins = await session.getBins(396838717);
```

```csharp
CardSavrResponse<Bins> bins = await session.GetBinsAsync(396838717);
```

```java
JsonValue bins = session.get("/cardsavr_bins", 396838717, null, null);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 396838717,
  "financial_institution_id": 1082614432,
  "custom_data": {
    "nFBVwkECPcQy": "t%S][Cnj-",
    "cWUrRVdgDUZD": 83,
    "bsOFYZUscJEv": true
  },
  "created_on": "1978-08-24T10:37:07.416Z",
  "last_updated_on": "2012-07-19T10:06:27.532Z",
  "bank_identification_number": "76605674"
}
```

### Path

GET /cardsavr_bins **(batch)** or GET /cardsavr_bins/:id **(singular)**

### Description

Returns the bin specified by the provided ID

#### Batch GET requests

**Batch requests** return the first page of all viewable bins, filtered by any [query filters](#get-filters) listed in the path.

**Example batch GET request path:**<br>`/cardsavr_bins?ids=1,2`

#### Singular GET requests

**Singular requests** only return the bin matching the id provided in the path.

**Example GET request path:**<br>`/cardsavr_bins/396838717`

### <a name="response-cardsavr_bin"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number | 
financial_institution_id | number (fk) | 
custom_data | object | 
created_on | date | Date this site was created on
last_updated_on | date | Date this site was last updated on
bank_identification_number | string | 

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

### Filter parameters
- ids / id (in path)
- financial_institution_ids
- bank_identification_numbers
- created_on_min / created_on_max
- last_updated_on_min / last_updated_on_max

## Create bin

```javascript
const bin = await session.createBin({
  "financial_institution_id": 1082614432,
  "bank_identification_number": "76605674",
  "custom_data": {
    "nFBVwkECPcQy": "t%S][Cnj-",
    "cWUrRVdgDUZD": 83,
    "bsOFYZUscJEv": true
  }
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "financial_institution_id", 1082614432 },
	{ "bank_identification_number", "76605674" }
};

CardSavrResponse<Bin> bin = await http.CreateBinAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("financial_institution_id", 1082614432 )
	.add("bank_identification_number", "76605674" )
	.build();
JsonValue bin = session.post("/cardsavr_bins", body, null, null);
```

```shell
curl -d "{\"financial_institution_id\":1082614432,\"bank_identification_number\":\"76605674\",\"custom_data\":{\"nFBVwkECPcQy\":\"t%S][Cnj-\",\"cWUrRVdgDUZD\":83,\"bsOFYZUscJEv\":true}}"
-X POST -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/cardsavr_bins/
```

### Path

POST /cardsavr_bins

### Description

Create a bin and return the created object.

### Body parameters

Parameter | Type | Required | Description
-------- | ---- | --------- | ----------
financial_institution_id | number | yes
bank_identification_number | string | yes
custom_data | object | no

See [bin response attributes](#response-cardsavr_bin).


## Update bin

```javascript
const bin = await session.updateBin(1,{
  "financial_institution_id": 1256429543,
  "custom_data": {
    "hbfaXnJzpcvm": ",xWz/JQDz<(9W!v6eIltQ.u@Nsp7s",
    "zXNKcqpyPcVM": 15,
    "HlIFBrmHZnPe": true
  }
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "financial_institution_id", 1256429543 }
};

CardSavrResponse<Bin> bin = await http.UpdateBinAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("financial_institution_id", 1256429543 )
	.build();
JsonValue bin = session.put("/cardsavr_bins", body, null, null);
```

```shell
curl -d "{\"financial_institution_id\":1256429543,\"custom_data\":{\"hbfaXnJzpcvm\":\",xWz/JQDz<(9W!v6eIltQ.u@Nsp7s\",\"zXNKcqpyPcVM\":15,\"HlIFBrmHZnPe\":true}}"
-X PUT -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/cardsavr_bins/396838717
```

### Path

PUT /cardsavr_bins OR /cardsavr_bins/{id}

### Description

Update a bin and return the updated object.  An id is required on every update request.

### Body parameters

Parameter | Type | Description 
-------- | ---- | ---------
financial_institution_id | number |
custom_data | object |

See [bin response parameters](#response-cardsavr_bin).


## Delete bin

```shell
curl -X DELETE
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/cardsavr_bins/396838717
```

```javascript
await session.deleteBin(396838717);
```

```csharp
CardSavrResponse<Bin> bin = await http.DeleteBinAsync(396838717);
```

```java
JsonValue bin = session.delete("/cardsavr_bins", 396838717, null);
```

### Path

DELETE /cardsavr_bins/{id}

### Description

Delete a bin and purge its [related items](#cascading-delete).  An id is required on every delete request.

See [bin response parameters](#response-cardsavr_bin).


# Cards
Card objects contain information about a payment card belonging to a single cardholder. Card objects are used to populate users' payment information on merchant sites.
## Get card

```shell
curl -H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/cardsavr_cards/2135437002
```

```javascript
const cards = await session.getCards(2135437002);
```

```csharp
CardSavrResponse<Cards> cards = await session.GetCardsAsync(2135437002);
```

```java
JsonValue cards = session.get("/cardsavr_cards", 2135437002, null, null);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 2135437002,
  "address_id": 1230915824,
  "bin_id": 1624789500,
  "name_on_card": "Joe C Smith",
  "first_6": "000000",
  "first_7": "0000000",
  "first_8": "00000000",
  "created_on": "1986-06-07T11:57:01.008Z",
  "last_updated_on": "1978-10-05T22:14:00.143Z",
  "expiration_month": 12,
  "expiration_year": 24,
  "cardholder_id": 1432522329,
  "par": "pEWXrAwDEBfGKENoeuGRljhoEiiWT"
}
```

### Path

GET /cardsavr_cards **(batch)** or GET /cardsavr_cards/:id **(singular)**

### Description

Returns the card specified by the provided ID

#### Batch GET requests

**Batch requests** return the first page of all viewable cards, filtered by any [query filters](#get-filters) listed in the path.

**Example batch GET request path:**<br>`/cardsavr_cards?ids=1,2`

#### Singular GET requests

**Singular requests** only return the card matching the id provided in the path.

**Example GET request path:**<br>`/cardsavr_cards/2135437002`

### <a name="response-cardsavr_card"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number | 
address_id | number | 
bin_id | number (fk) | 
name_on_card | string | 
first_6 | string | 
first_7 | string | 
first_8 | string | 
created_on | date | Date this site was created on
last_updated_on | date | Date this site was last updated on
expiration_month | string | 
expiration_year | string | 
cardholder_id | number (fk) | 
par | string | 

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

### Filter parameters
- ids / id (in path)
- cardholder_ids
- address_ids
- bin_ids
- pars
- first_6
- first_7
- first_8
- created_on_min / created_on_max
- last_updated_on_min / last_updated_on_max

## Create card

```javascript
const card = await session.createCard({
  "cardholder_id": 1432522329,
  "address_id": 1230915824,
  "bin_id": 1624789500,
  "par": "pEWXrAwDEBfGKENoeuGRljhoEiiWT",
  "pan": "4111111111111111",
  "cvv": "111",
  "expiration_month": 12,
  "expiration_year": 24,
  "name_on_card": "Joe C Smith",
  "first_6": "000000",
  "first_7": "0000000",
  "first_8": "00000000"
}, CARDHOLDER_SAFE_KEY);
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "cardholder_id", 1432522329 },
	{ "address_id", 1230915824 },
	{ "bin_id", 1624789500 },
	{ "par", "pEWXrAwDEBfGKENoeuGRljhoEiiWT" },
	{ "pan", "4111111111111111" },
	{ "cvv", "111" },
	{ "expiration_month", 12 },
	{ "expiration_year", 24 },
	{ "name_on_card", "Joe C Smith" },
	{ "first_6", "000000" },
	{ "first_7", "0000000" },
	{ "first_8", "00000000" }
};

CardSavrResponse<Card> card = await http.CreateCardAsync(body, CARDHOLDER_SAFE_KEY);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("cardholder_id", 1432522329 )
	.add("address_id", 1230915824 )
	.add("bin_id", 1624789500 )
	.add("par", "pEWXrAwDEBfGKENoeuGRljhoEiiWT" )
	.add("pan", "4111111111111111" )
	.add("cvv", "111" )
	.add("expiration_month", 12 )
	.add("expiration_year", 24 )
	.add("name_on_card", "Joe C Smith" )
	.add("first_6", "000000" )
	.add("first_7", "0000000" )
	.add("first_8", "00000000" )
	.build();
JsonValue card = session.post("/cardsavr_cards", body, null, null);
```

```shell
curl -d "{\"cardholder_id\":1432522329,\"address_id\":1230915824,\"bin_id\":1624789500,\"par\":\"pEWXrAwDEBfGKENoeuGRljhoEiiWT\",\"pan\":\"4111111111111111\",\"cvv\":\"111\",\"expiration_month\":12,\"expiration_year\":24,\"name_on_card\":\"Joe C Smith\",\"first_6\":\"000000\",\"first_7\":\"0000000\",\"first_8\":\"00000000\"}"
-X POST -H "Content-Type: application/json"
-H "x-cardsavr-cardholder-safe-key: CARDHOLDER_SAFE_KEY"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/cardsavr_cards/
```

### Path

POST /cardsavr_cards

### Description

Create a card and return the created object.

### Body parameters

Parameter | Type | Required | Description
-------- | ---- | --------- | ----------
cardholder_id | number | yes
address_id | number | no
bin_id | number | no
par | string | yes
pan | string | yes
cvv | string | yes
expiration_month | string | yes
expiration_year | string | yes
name_on_card | string | yes

See [card response attributes](#response-cardsavr_card).

<aside class="notice">Update calls to /cardsavr_cards require the cardholder's personal cardholder_safe_key header to encrypt and save the pan and cvv when Strivve does not manage keys for a customer (this is an environment setting). The safe keys are also not required if updating non-safe user properties.</aside>

## Update card

```javascript
const card = await session.updateCard(1,{
  "address_id": 1361034684,
  "bin_id": 1067808185,
  "name_on_card": "Joe C Smith",
  "pan": "4111111111111111",
  "cvv": "111",
  "expiration_month": 12,
  "expiration_year": 24,
  "first_6": "000000",
  "first_7": "0000000",
  "first_8": "00000000"
}, CARDHOLDER_SAFE_KEY);
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "address_id", 1361034684 },
	{ "bin_id", 1067808185 },
	{ "name_on_card", "Joe C Smith" },
	{ "pan", "4111111111111111" },
	{ "cvv", "111" },
	{ "expiration_month", 12 },
	{ "expiration_year", 24 },
	{ "first_6", "000000" },
	{ "first_7", "0000000" },
	{ "first_8", "00000000" }
};

CardSavrResponse<Card> card = await http.UpdateCardAsync(body, CARDHOLDER_SAFE_KEY);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("address_id", 1361034684 )
	.add("bin_id", 1067808185 )
	.add("name_on_card", "Joe C Smith" )
	.add("pan", "4111111111111111" )
	.add("cvv", "111" )
	.add("expiration_month", 12 )
	.add("expiration_year", 24 )
	.add("first_6", "000000" )
	.add("first_7", "0000000" )
	.add("first_8", "00000000" )
	.build();
JsonValue card = session.put("/cardsavr_cards", body, null, null);
```

```shell
curl -d "{\"address_id\":1361034684,\"bin_id\":1067808185,\"name_on_card\":\"Joe C Smith\",\"pan\":\"4111111111111111\",\"cvv\":\"111\",\"expiration_month\":12,\"expiration_year\":24,\"first_6\":\"000000\",\"first_7\":\"0000000\",\"first_8\":\"00000000\"}"
-X PUT -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/cardsavr_cards/2135437002
```

### Path

PUT /cardsavr_cards OR /cardsavr_cards/{id}

### Description

Update a card and return the updated object.  An id is required on every update request.

### Body parameters

Parameter | Type | Description 
-------- | ---- | ---------
address_id | number |
bin_id | number |
name_on_card | string |

See [card response parameters](#response-cardsavr_card).


## Delete card

```shell
curl -X DELETE
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/cardsavr_cards/2135437002
```

```javascript
await session.deleteCard(2135437002);
```

```csharp
CardSavrResponse<Card> card = await http.DeleteCardAsync(2135437002);
```

```java
JsonValue card = session.delete("/cardsavr_cards", 2135437002, null);
```

### Path

DELETE /cardsavr_cards/{id}

### Description

Delete a card and purge its [related items](#cascading-delete).  An id is required on every delete request.

See [card response parameters](#response-cardsavr_card).


# Cardholders
Entities which represent end-users/cardholders.
## Get cardholder

```shell
curl -H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/cardholders/1305767855
```

```javascript
const cardholders = await session.getCardholders(1305767855);
```

```csharp
CardSavrResponse<Cardholders> cardholders = await session.GetCardholdersAsync(1305767855);
```

```java
JsonValue cardholders = session.get("/cardholders", 1305767855, null, null);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 1305767855,
  "financial_institution_id": 19439489,
  "agent_session_id": "EuzxbhMbznyrG",
  "first_name": "Joe",
  "last_name": "Smith",
  "email": "test_email@strivve.com",
  "meta_key": "BfWwRBzFOOAxMgzMGbaUoHDBmSGK",
  "custom_data": {
    "xAotCEshdCNN": "e8mUw>d",
    "bBjoqThlajFx": 12,
    "werXyBXWQTWy": false
  },
  "created_on": "1973-10-20T17:15:23.462Z",
  "last_updated_on": "2014-04-30T23:31:07.249Z",
  "cuid": "HXKCzKGGYDovIrcEhmQYXBYPkHARy"
}
```

### Path

GET /cardholders **(batch)** or GET /cardholders/:id **(singular)**

### Description

Returns the cardholder specified by the provided ID

#### Batch GET requests

**Batch requests** return the first page of all viewable cardholders, filtered by any [query filters](#get-filters) listed in the path.

**Example batch GET request path:**<br>`/cardholders?ids=1,2`

#### Singular GET requests

**Singular requests** only return the cardholder matching the id provided in the path.

**Example GET request path:**<br>`/cardholders/1305767855`

### <a name="response-cardholder"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number | 
financial_institution_id | number (fk) | 
agent_session_id | string | 
type | string | 
first_name | string | 
last_name | string | 
email | string | 
meta_key | string | 
custom_data | object | 
created_on | date | Date this site was created on
last_updated_on | date | Date this site was last updated on
cuid | string | 

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

### Filter parameters
- ids / id (in path)
- financial_institution_ids
- agent_session_id
- cuid
- type
- first_name
- last_name
- email
- meta_key
- created_on_min / created_on_max
- last_updated_on_min / last_updated_on_max

## Create cardholder

```javascript
const cardholder = await session.createCardholder({
  "financial_institution_id": 19439489,
  "cuid": "HXKCzKGGYDovIrcEhmQYXBYPkHARy",
  "first_name": "Joe",
  "last_name": "Smith",
  "email": "test_email@strivve.com",
  "meta_key": "BfWwRBzFOOAxMgzMGbaUoHDBmSGK",
  "custom_data": {
    "xAotCEshdCNN": "e8mUw>d",
    "bBjoqThlajFx": 12,
    "werXyBXWQTWy": false
  }
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "financial_institution_id", 19439489 },
	{ "cuid", "HXKCzKGGYDovIrcEhmQYXBYPkHARy" },
	{ "first_name", "Joe" },
	{ "last_name", "Smith" },
	{ "email", "test_email@strivve.com" },
	{ "meta_key", "BfWwRBzFOOAxMgzMGbaUoHDBmSGK" }
};

CardSavrResponse<Cardholder> cardholder = await http.CreateCardholderAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("financial_institution_id", 19439489 )
	.add("cuid", "HXKCzKGGYDovIrcEhmQYXBYPkHARy" )
	.add("first_name", "Joe" )
	.add("last_name", "Smith" )
	.add("email", "test_email@strivve.com" )
	.add("meta_key", "BfWwRBzFOOAxMgzMGbaUoHDBmSGK" )
	.build();
JsonValue cardholder = session.post("/cardholders", body, null, null);
```

```shell
curl -d "{\"financial_institution_id\":19439489,\"cuid\":\"HXKCzKGGYDovIrcEhmQYXBYPkHARy\",\"first_name\":\"Joe\",\"last_name\":\"Smith\",\"email\":\"test_email@strivve.com\",\"meta_key\":\"BfWwRBzFOOAxMgzMGbaUoHDBmSGK\",\"custom_data\":{\"xAotCEshdCNN\":\"e8mUw>d\",\"bBjoqThlajFx\":12,\"werXyBXWQTWy\":false}}"
-X POST -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/cardholders/
```

### Path

POST /cardholders

### Description

Create a cardholder and return the created object.

### Body parameters

Parameter | Type | Required | Description
-------- | ---- | --------- | ----------
financial_institution_id | number | no
cuid | string | yes
type | [string enum](#post-cardholder-1)* | no
first_name | string | no
last_name | string | no
email | string | no
meta_key | string | no
custom_data | object | no

See [cardholder response attributes](#response-cardholder).

#### <a name="post-cardholder-1"></a>string enum*
- ephemeral


## Update cardholder

```javascript
const cardholder = await session.updateCardholder(1,{
  "financial_institution_id": 260414691,
  "first_name": "Joe",
  "last_name": "Smith",
  "email": "test_email@strivve.com",
  "meta_key": "fvVNMytZixfFDINNgSHrZQFdZLfFdYbp",
  "custom_data": {
    "jjZYeFjNcSIt": "X7B%xzov@$*EQ([Qv5Bx*bcT&!(k",
    "xXDiCEJsXlsB": 73,
    "pRefwwUdZHwz": true
  }
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "financial_institution_id", 260414691 },
	{ "first_name", "Joe" },
	{ "last_name", "Smith" },
	{ "email", "test_email@strivve.com" },
	{ "meta_key", "fvVNMytZixfFDINNgSHrZQFdZLfFdYbp" }
};

CardSavrResponse<Cardholder> cardholder = await http.UpdateCardholderAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("financial_institution_id", 260414691 )
	.add("first_name", "Joe" )
	.add("last_name", "Smith" )
	.add("email", "test_email@strivve.com" )
	.add("meta_key", "fvVNMytZixfFDINNgSHrZQFdZLfFdYbp" )
	.build();
JsonValue cardholder = session.put("/cardholders", body, null, null);
```

```shell
curl -d "{\"financial_institution_id\":260414691,\"first_name\":\"Joe\",\"last_name\":\"Smith\",\"email\":\"test_email@strivve.com\",\"meta_key\":\"fvVNMytZixfFDINNgSHrZQFdZLfFdYbp\",\"custom_data\":{\"jjZYeFjNcSIt\":\"X7B%xzov@$*EQ([Qv5Bx*bcT&!(k\",\"xXDiCEJsXlsB\":73,\"pRefwwUdZHwz\":true}}"
-X PUT -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/cardholders/1305767855
```

### Path

PUT /cardholders OR /cardholders/{id}

### Description

Update a cardholder and return the updated object.  An id is required on every update request.

### Body parameters

Parameter | Type | Description 
-------- | ---- | ---------
financial_institution_id | number |
type | [string enum](#post-cardholder-1)* |
first_name | string |
last_name | string |
email | string |
meta_key | string |
custom_data | object |

See [cardholder response parameters](#response-cardholder).


## Delete cardholder

```shell
curl -X DELETE
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/cardholders/1305767855
```

```javascript
await session.deleteCardholder(1305767855);
```

```csharp
CardSavrResponse<Cardholder> cardholder = await http.DeleteCardholderAsync(1305767855);
```

```java
JsonValue cardholder = session.delete("/cardholders", 1305767855, null);
```

### Path

DELETE /cardholders/{id}

### Description

Delete a cardholder and purge its [related items](#cascading-delete).  An id is required on every delete request.

See [cardholder response parameters](#response-cardholder).


# Users
User objects correspond to a single CardSavr user.
## Get user

```shell
curl -H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/cardsavr_users/53264242
```

```javascript
const users = await session.getUsers(53264242);
```

```csharp
CardSavrResponse<Users> users = await session.GetUsersAsync(53264242);
```

```java
JsonValue users = session.get("/cardsavr_users", 53264242, null, null);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 53264242,
  "financial_institution_id": 960614802,
  "first_name": "Joe",
  "last_name": "Smith",
  "last_login_time": "2008-08-24T05:13:59.294Z",
  "is_locked": true,
  "password_lifetime": 170,
  "email": "test_email@strivve.com",
  "is_password_update_required": true,
  "role": "admin",
  "custom_data": {
    "NCOrGkDQxMvJ": "{lW6f8",
    "IEsRNTSJfOZV": 99,
    "jfAULyRHXKjF": false
  },
  "next_rotation_on": "2011-05-25T05:02:21.246Z",
  "created_on": "1993-07-13T04:09:42.586Z",
  "last_updated_on": "1995-03-01T08:42:33.433Z",
  "username": "jsmith123"
}
```

### Path

GET /cardsavr_users **(batch)** or GET /cardsavr_users/:id **(singular)**

### Description

Returns the user specified by the provided ID

#### Batch GET requests

**Batch requests** return the first page of all viewable users, filtered by any [query filters](#get-filters) listed in the path.

**Example batch GET request path:**<br>`/cardsavr_users?ids=1,2`

#### Singular GET requests

**Singular requests** only return the user matching the id provided in the path.

**Example GET request path:**<br>`/cardsavr_users/53264242`

### <a name="response-cardsavr_user"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number | 
financial_institution_id | number (fk) | 
first_name | string | 
last_name | string | 
last_login_time | date | 
is_locked | boolean | 
password_lifetime | number | 
email | string | 
is_password_update_required | boolean | 
role | string | 
custom_data | object | 
next_rotation_on | date | 
created_on | date | Date this site was created on
last_updated_on | date | Date this site was last updated on
username | string | 

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

### Filter parameters
- ids / id (in path)
- financial_institution_ids
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

## Create user

```javascript
const user = await session.createUser({
  "financial_institution_id": 960614802,
  "username": "jsmith123",
  "password": "BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI=",
  "first_name": "Joe",
  "last_name": "Smith",
  "password_lifetime": 170,
  "email": "test_email@strivve.com",
  "is_password_update_required": true,
  "role": "admin",
  "custom_data": {
    "NCOrGkDQxMvJ": "{lW6f8",
    "IEsRNTSJfOZV": 99,
    "jfAULyRHXKjF": false
  },
  "next_rotation_on": "2011-05-25T05:02:21.246Z"
}, CARDHOLDER_SAFE_KEY);
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "financial_institution_id", 960614802 },
	{ "username", "jsmith123" },
	{ "password", "BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI=" },
	{ "first_name", "Joe" },
	{ "last_name", "Smith" },
	{ "password_lifetime", 170 },
	{ "email", "test_email@strivve.com" },
	{ "is_password_update_required", true },
	{ "role", "admin" },
	{ "next_rotation_on", "2011-05-25T05:02:21.246Z" }
};

CardSavrResponse<User> user = await http.CreateUserAsync(body, CARDHOLDER_SAFE_KEY);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("financial_institution_id", 960614802 )
	.add("username", "jsmith123" )
	.add("password", "BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI=" )
	.add("first_name", "Joe" )
	.add("last_name", "Smith" )
	.add("password_lifetime", 170 )
	.add("email", "test_email@strivve.com" )
	.add("is_password_update_required", true )
	.add("role", "admin" )
	.add("next_rotation_on", "2011-05-25T05:02:21.246Z" )
	.build();
JsonValue user = session.post("/cardsavr_users", body, null, null);
```

```shell
curl -d "{\"financial_institution_id\":960614802,\"username\":\"jsmith123\",\"password\":\"BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI=\",\"first_name\":\"Joe\",\"last_name\":\"Smith\",\"password_lifetime\":170,\"email\":\"test_email@strivve.com\",\"is_password_update_required\":true,\"role\":\"admin\",\"custom_data\":{\"NCOrGkDQxMvJ\":\"{lW6f8\",\"IEsRNTSJfOZV\":99,\"jfAULyRHXKjF\":false},\"next_rotation_on\":\"2011-05-25T05:02:21.246Z\"}"
-X POST -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/cardsavr_users/
```

### Path

POST /cardsavr_users

### Description

Create a user and return the created object.

### Body parameters

Parameter | Type | Required | Description
-------- | ---- | --------- | ----------
financial_institution_id | number | no
username | string | yes
password | string | yes
first_name | string | no
last_name | string | no
password_lifetime | number | no
email | string | no
is_password_update_required | boolean | no
role | [string enum](#post-cardsavr_user-1)* | yes
custom_data | object | no
next_rotation_on | date | no

See [user response attributes](#response-cardsavr_user).

#### <a name="post-cardsavr_user-1"></a>string enum*
- admin
- cardholder_agent
- customer_agent
- swch_agent


## Update user

```javascript
const user = await session.updateUser(1,{
  "financial_institution_id": 139366338,
  "first_name": "Joe",
  "last_name": "Smith",
  "password_lifetime": 39,
  "email": "test_email@strivve.com",
  "is_password_update_required": true,
  "role": "cardholder_agent",
  "custom_data": {
    "zaDcESCLcByl": "!%.rG<D=!M&7eY",
    "QwjXbkXeXztQ": 58,
    "FeUcyFTssesz": false
  },
  "next_rotation_on": "1979-03-27T11:49:44.479Z",
  "username": "jsmith123",
  "password": "BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI="
}, NEW_CARDHODLER_SAFE_KEY, CARDHOLDER_SAFE_KEY);
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "financial_institution_id", 139366338 },
	{ "first_name", "Joe" },
	{ "last_name", "Smith" },
	{ "password_lifetime", 39 },
	{ "email", "test_email@strivve.com" },
	{ "is_password_update_required", true },
	{ "role", "cardholder_agent" },
	{ "next_rotation_on", "1979-03-27T11:49:44.479Z" },
	{ "username", "jsmith123" },
	{ "password", "BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI=" }
};

CardSavrResponse<User> user = await http.UpdateUserAsync(body, NEW_CARDHODLER_SAFE_KEY, CARDHOLDER_SAFE_KEY);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("financial_institution_id", 139366338 )
	.add("first_name", "Joe" )
	.add("last_name", "Smith" )
	.add("password_lifetime", 39 )
	.add("email", "test_email@strivve.com" )
	.add("is_password_update_required", true )
	.add("role", "cardholder_agent" )
	.add("next_rotation_on", "1979-03-27T11:49:44.479Z" )
	.add("username", "jsmith123" )
	.add("password", "BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI=" )
	.build();
JsonValue user = session.put("/cardsavr_users", body, null, null);
```

```shell
curl -d "{\"financial_institution_id\":139366338,\"first_name\":\"Joe\",\"last_name\":\"Smith\",\"password_lifetime\":39,\"email\":\"test_email@strivve.com\",\"is_password_update_required\":true,\"role\":\"cardholder_agent\",\"custom_data\":{\"zaDcESCLcByl\":\"!%.rG<D=!M&7eY\",\"QwjXbkXeXztQ\":58,\"FeUcyFTssesz\":false},\"next_rotation_on\":\"1979-03-27T11:49:44.479Z\",\"username\":\"jsmith123\",\"password\":\"BSN6W6IF72W6EVWwbwgqYIo51ad/ZCZ74vxa3rzyQqI=\"}"
-X PUT -H "Content-Type: application/json"
-H "x-cardsavr-new-cardholder-safe-key: NEW_CARDHODLER_SAFE_KEY"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/cardsavr_users/53264242
```

### Path

PUT /cardsavr_users OR /cardsavr_users/{id}

### Description

Update a user and return the updated object.  An id is required on every update request.

### Body parameters

Parameter | Type | Description 
-------- | ---- | ---------
financial_institution_id | number |
first_name | string |
last_name | string |
password_lifetime | number |
email | string |
is_password_update_required | boolean |
role | [string enum](#post-cardsavr_user-1)* |
custom_data | object |
next_rotation_on | date |

See [user response parameters](#response-cardsavr_user).


## Delete user

```shell
curl -X DELETE
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/cardsavr_users/53264242
```

```javascript
await session.deleteUser(53264242);
```

```csharp
CardSavrResponse<User> user = await http.DeleteUserAsync(53264242);
```

```java
JsonValue user = session.delete("/cardsavr_users", 53264242, null);
```

### Path

DELETE /cardsavr_users/{id}

### Description

Delete a user and purge its [related items](#cascading-delete).  An id is required on every delete request.

See [user response parameters](#response-cardsavr_user).


# Financial Institutions
A CardSavr Financial Institution that can be associated with jobs and users.
## Get financial institution

```shell
curl -H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/financial_institutions/1622457924
```

```javascript
const financialinstitutions = await session.getFinancialInstitutions(1622457924);
```

```csharp
CardSavrResponse<FinancialInstitutions> financialinstitutions = await session.GetFinancialInstitutionsAsync(1622457924);
```

```java
JsonValue financialinstitutions = session.get("/financial_institutions", 1622457924, null, null);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 1622457924,
  "name": "KFuEaWOZXZRccBhXfANOoAPUfmFHnOYlrnwHbyqhiuzqMoDzfcXLTCCZkrFYFyh",
  "description": "zPLCFi",
  "lookup_key": "GUNiQTtHAjLtBpjCLalIrOsLgWCWVNwAeEonwLQQOUlukAOCiQlRQKWWxAwIPbY",
  "alternate_lookup_key": "tuCMYYJxcfblgonzTromtpZSkzIPpdsnHBUMHxQpGAQEgaASNSWjCxvgxumayyD",
  "config": {
    "yCGkbMtsLNHi": "z)LX(/",
    "QdGfzrLzlTiY": 16,
    "WazjsthyVRBD": false
  },
  "email_config": {
    "OAkvzvadNkaN": "T2I@5*w*1=ut7v*lbcq,3z",
    "roKWwxWYPYfb": 0,
    "iNaNOhIqPqRF": true
  },
  "created_on": "2011-08-23T03:25:59.818Z",
  "last_updated_on": "2016-05-14T00:18:05.274Z"
}
```

### Path

GET /financial_institutions **(batch)** or GET /financial_institutions/:id **(singular)**

### Description

Returns the financial institution specified by the provided ID

#### Batch GET requests

**Batch requests** return the first page of all viewable financial institutions, filtered by any [query filters](#get-filters) listed in the path.

**Example batch GET request path:**<br>`/financial_institutions?ids=1,2`

#### Singular GET requests

**Singular requests** only return the financial institution matching the id provided in the path.

**Example GET request path:**<br>`/financial_institutions/1622457924`

### <a name="response-financial_institution"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number | 
name | string | 
description | string | 
lookup_key | string | 
alternate_lookup_key | string | 
config | object | 
email_config | object | 
created_on | date | Date this integrator was created on
last_updated_on | date | Date this integrator was last updated on

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

### Filter parameters
- ids / id (in path)
- names
- lookup_key
- alternate_lookup_key
- created_on_min / created_on_max
- last_updated_on_min / last_updated_on_max

## Create financial institution

```javascript
const financialinstitution = await session.createFinancialInstitution({
  "name": "KFuEaWOZXZRccBhXfANOoAPUfmFHnOYlrnwHbyqhiuzqMoDzfcXLTCCZkrFYFyh",
  "description": "zPLCFi",
  "lookup_key": "GUNiQTtHAjLtBpjCLalIrOsLgWCWVNwAeEonwLQQOUlukAOCiQlRQKWWxAwIPbY",
  "alternate_lookup_key": "tuCMYYJxcfblgonzTromtpZSkzIPpdsnHBUMHxQpGAQEgaASNSWjCxvgxumayyD",
  "config": {
    "yCGkbMtsLNHi": "z)LX(/",
    "QdGfzrLzlTiY": 16,
    "WazjsthyVRBD": false
  },
  "email_config": {
    "OAkvzvadNkaN": "T2I@5*w*1=ut7v*lbcq,3z",
    "roKWwxWYPYfb": 0,
    "iNaNOhIqPqRF": true
  }
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "name", "KFuEaWOZXZRccBhXfANOoAPUfmFHnOYlrnwHbyqhiuzqMoDzfcXLTCCZkrFYFyh" },
	{ "description", "zPLCFi" },
	{ "lookup_key", "GUNiQTtHAjLtBpjCLalIrOsLgWCWVNwAeEonwLQQOUlukAOCiQlRQKWWxAwIPbY" },
	{ "alternate_lookup_key", "tuCMYYJxcfblgonzTromtpZSkzIPpdsnHBUMHxQpGAQEgaASNSWjCxvgxumayyD" }
};

CardSavrResponse<FinancialInstitution> financialinstitution = await http.CreateFinancialInstitutionAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("name", "KFuEaWOZXZRccBhXfANOoAPUfmFHnOYlrnwHbyqhiuzqMoDzfcXLTCCZkrFYFyh" )
	.add("description", "zPLCFi" )
	.add("lookup_key", "GUNiQTtHAjLtBpjCLalIrOsLgWCWVNwAeEonwLQQOUlukAOCiQlRQKWWxAwIPbY" )
	.add("alternate_lookup_key", "tuCMYYJxcfblgonzTromtpZSkzIPpdsnHBUMHxQpGAQEgaASNSWjCxvgxumayyD" )
	.build();
JsonValue financialinstitution = session.post("/financial_institutions", body, null, null);
```

```shell
curl -d "{\"name\":\"KFuEaWOZXZRccBhXfANOoAPUfmFHnOYlrnwHbyqhiuzqMoDzfcXLTCCZkrFYFyh\",\"description\":\"zPLCFi\",\"lookup_key\":\"GUNiQTtHAjLtBpjCLalIrOsLgWCWVNwAeEonwLQQOUlukAOCiQlRQKWWxAwIPbY\",\"alternate_lookup_key\":\"tuCMYYJxcfblgonzTromtpZSkzIPpdsnHBUMHxQpGAQEgaASNSWjCxvgxumayyD\",\"config\":{\"yCGkbMtsLNHi\":\"z)LX(/\",\"QdGfzrLzlTiY\":16,\"WazjsthyVRBD\":false},\"email_config\":{\"OAkvzvadNkaN\":\"T2I@5*w*1=ut7v*lbcq,3z\",\"roKWwxWYPYfb\":0,\"iNaNOhIqPqRF\":true}}"
-X POST -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/financial_institutions/
```

### Path

POST /financial_institutions

### Description

Create a financial institution and return the created object.

### Body parameters

Parameter | Type | Required | Description
-------- | ---- | --------- | ----------
name | string | yes
description | string | no
lookup_key | string | yes
alternate_lookup_key | string | no
config | object | no
email_config | object | no

See [financial institution response attributes](#response-financial_institution).


## Update financial institution

```javascript
const financialinstitution = await session.updateFinancialInstitution(1,{
  "name": "akzqwPiYwXobtVptfGmVmKiqvwHuHMcQQNhmkfNlAdVRCdnsiECtStohvvkhXLP",
  "description": "nCTEdYOAPHRPAXoQNNJBVs",
  "lookup_key": "jQsTvcUTWyVcSzNdBUFumyeRpmjJmpiyqzMHsKWkKfluYNMePbMRLcvQtJENlSg",
  "alternate_lookup_key": "sslIXBoIDdfDyIReZIFERlCjkZTRPnGkoIMgpeaPIcvDpcgOxYPkDKRXVUsfuih",
  "config": {
    "VwyailwOXePy": "o-Hb7Txs=zyBwNZaoXLil$Le/m",
    "UjRsAiCthLqa": 25,
    "HLIKdhXeyHsp": false
  },
  "email_config": {
    "PAPkTDkTxbHK": "}Fx*{Zvq!=.Bufkh",
    "kizYKNPnDDjN": 6,
    "iqRIaukRPkaS": true
  }
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "name", "akzqwPiYwXobtVptfGmVmKiqvwHuHMcQQNhmkfNlAdVRCdnsiECtStohvvkhXLP" },
	{ "description", "nCTEdYOAPHRPAXoQNNJBVs" },
	{ "lookup_key", "jQsTvcUTWyVcSzNdBUFumyeRpmjJmpiyqzMHsKWkKfluYNMePbMRLcvQtJENlSg" },
	{ "alternate_lookup_key", "sslIXBoIDdfDyIReZIFERlCjkZTRPnGkoIMgpeaPIcvDpcgOxYPkDKRXVUsfuih" }
};

CardSavrResponse<FinancialInstitution> financialinstitution = await http.UpdateFinancialInstitutionAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("name", "akzqwPiYwXobtVptfGmVmKiqvwHuHMcQQNhmkfNlAdVRCdnsiECtStohvvkhXLP" )
	.add("description", "nCTEdYOAPHRPAXoQNNJBVs" )
	.add("lookup_key", "jQsTvcUTWyVcSzNdBUFumyeRpmjJmpiyqzMHsKWkKfluYNMePbMRLcvQtJENlSg" )
	.add("alternate_lookup_key", "sslIXBoIDdfDyIReZIFERlCjkZTRPnGkoIMgpeaPIcvDpcgOxYPkDKRXVUsfuih" )
	.build();
JsonValue financialinstitution = session.put("/financial_institutions", body, null, null);
```

```shell
curl -d "{\"name\":\"akzqwPiYwXobtVptfGmVmKiqvwHuHMcQQNhmkfNlAdVRCdnsiECtStohvvkhXLP\",\"description\":\"nCTEdYOAPHRPAXoQNNJBVs\",\"lookup_key\":\"jQsTvcUTWyVcSzNdBUFumyeRpmjJmpiyqzMHsKWkKfluYNMePbMRLcvQtJENlSg\",\"alternate_lookup_key\":\"sslIXBoIDdfDyIReZIFERlCjkZTRPnGkoIMgpeaPIcvDpcgOxYPkDKRXVUsfuih\",\"config\":{\"VwyailwOXePy\":\"o-Hb7Txs=zyBwNZaoXLil$Le/m\",\"UjRsAiCthLqa\":25,\"HLIKdhXeyHsp\":false},\"email_config\":{\"PAPkTDkTxbHK\":\"}Fx*{Zvq!=.Bufkh\",\"kizYKNPnDDjN\":6,\"iqRIaukRPkaS\":true}}"
-X PUT -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/financial_institutions/1622457924
```

### Path

PUT /financial_institutions OR /financial_institutions/{id}

### Description

Update a financial institution and return the updated object.  An id is required on every update request.

### Body parameters

Parameter | Type | Description 
-------- | ---- | ---------
name | string |
description | string |
lookup_key | string |
alternate_lookup_key | string |
config | object |
email_config | object |

See [financial institution response parameters](#response-financial_institution).


## Delete financial institution

```shell
curl -X DELETE
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/financial_institutions/1622457924
```

```javascript
await session.deleteFinancialInstitution(1622457924);
```

```csharp
CardSavrResponse<FinancialInstitution> financialinstitution = await http.DeleteFinancialInstitutionAsync(1622457924);
```

```java
JsonValue financialinstitution = session.delete("/financial_institutions", 1622457924, null);
```

### Path

DELETE /financial_institutions/{id}

### Description

Delete a financial institution and purge its [related items](#cascading-delete).  An id is required on every delete request.

See [financial institution response parameters](#response-financial_institution).


# Integrators
An integrator object represents an integrator that implements CardSavr.
## Get integrator

```shell
curl -H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/integrators/1560055497
```

```javascript
const integrators = await session.getIntegrators(1560055497);
```

```csharp
CardSavrResponse<Integrators> integrators = await session.GetIntegratorsAsync(1560055497);
```

```java
JsonValue integrators = session.get("/integrators", 1560055497, null, null);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 1560055497,
  "name": "XTDjhUJpDfOrMOtKLNDwtsDfPhnllAzReEcFLwqdAaBnOThUy",
  "integrator_type": "application",
  "description": "WCdgUkYG",
  "last_key": "vqt3444Ku0FTHD2Q+XKrspTw7njcTATyLSXSUu8XRdQ=",
  "current_key": "PQY4sXhuHvEtrOt2b93sgYYRCHew245VOmER8g1rQv0=",
  "next_key": "cxXqkfrQ45ISFsQEQIMgJpOlMDxsrfxaNYx+u0WDbYs=",
  "key_lifetime": 14,
  "next_rotation_on": "1984-08-29T21:47:44.204Z",
  "created_on": "1977-05-02T11:43:07.143Z",
  "last_updated_on": "2006-06-16T18:10:37.089Z"
}
```

### Path

GET /integrators **(batch)** or GET /integrators/:id **(singular)**

### Description

Returns the integrator specified by the provided ID

#### Batch GET requests

**Batch requests** return the first page of all viewable integrators, filtered by any [query filters](#get-filters) listed in the path.

**Example batch GET request path:**<br>`/integrators?ids=1,2`

#### Singular GET requests

**Singular requests** only return the integrator matching the id provided in the path.

**Example GET request path:**<br>`/integrators/1560055497`

### <a name="response-integrator"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number | An integrator's unique identifier
name | string | An integrator's name
integrator_type | string | What type of integrator is this?
description | string | An integrator's description
last_key | string | 
current_key | string | 
next_key | string | 
key_lifetime | number | 
next_rotation_on | date | 
created_on | date | Date this integrator was created on
last_updated_on | date | Date this integrator was last updated on

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

### Filter parameters
- ids / id (in path)
- names
- name
- integrator_type
- integrator_types_include / integrator_types_exclude
- next_rotation_on_min / next_rotation_on_max
- created_on_min / created_on_max
- last_updated_on_min / last_updated_on_max

## Create integrator

```javascript
const integrator = await session.createIntegrator({
  "name": "XTDjhUJpDfOrMOtKLNDwtsDfPhnllAzReEcFLwqdAaBnOThUy",
  "integrator_type": "application",
  "description": "WCdgUkYG",
  "last_key": "vqt3444Ku0FTHD2Q+XKrspTw7njcTATyLSXSUu8XRdQ=",
  "current_key": "PQY4sXhuHvEtrOt2b93sgYYRCHew245VOmER8g1rQv0=",
  "next_key": "cxXqkfrQ45ISFsQEQIMgJpOlMDxsrfxaNYx+u0WDbYs=",
  "key_lifetime": 14,
  "next_rotation_on": "1984-08-29T21:47:44.204Z"
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "name", "XTDjhUJpDfOrMOtKLNDwtsDfPhnllAzReEcFLwqdAaBnOThUy" },
	{ "integrator_type", "application" },
	{ "description", "WCdgUkYG" },
	{ "last_key", "vqt3444Ku0FTHD2Q+XKrspTw7njcTATyLSXSUu8XRdQ=" },
	{ "current_key", "PQY4sXhuHvEtrOt2b93sgYYRCHew245VOmER8g1rQv0=" },
	{ "next_key", "cxXqkfrQ45ISFsQEQIMgJpOlMDxsrfxaNYx+u0WDbYs=" },
	{ "key_lifetime", 14 },
	{ "next_rotation_on", "1984-08-29T21:47:44.204Z" }
};

CardSavrResponse<Integrator> integrator = await http.CreateIntegratorAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("name", "XTDjhUJpDfOrMOtKLNDwtsDfPhnllAzReEcFLwqdAaBnOThUy" )
	.add("integrator_type", "application" )
	.add("description", "WCdgUkYG" )
	.add("last_key", "vqt3444Ku0FTHD2Q+XKrspTw7njcTATyLSXSUu8XRdQ=" )
	.add("current_key", "PQY4sXhuHvEtrOt2b93sgYYRCHew245VOmER8g1rQv0=" )
	.add("next_key", "cxXqkfrQ45ISFsQEQIMgJpOlMDxsrfxaNYx+u0WDbYs=" )
	.add("key_lifetime", 14 )
	.add("next_rotation_on", "1984-08-29T21:47:44.204Z" )
	.build();
JsonValue integrator = session.post("/integrators", body, null, null);
```

```shell
curl -d "{\"name\":\"XTDjhUJpDfOrMOtKLNDwtsDfPhnllAzReEcFLwqdAaBnOThUy\",\"integrator_type\":\"application\",\"description\":\"WCdgUkYG\",\"last_key\":\"vqt3444Ku0FTHD2Q+XKrspTw7njcTATyLSXSUu8XRdQ=\",\"current_key\":\"PQY4sXhuHvEtrOt2b93sgYYRCHew245VOmER8g1rQv0=\",\"next_key\":\"cxXqkfrQ45ISFsQEQIMgJpOlMDxsrfxaNYx+u0WDbYs=\",\"key_lifetime\":14,\"next_rotation_on\":\"1984-08-29T21:47:44.204Z\"}"
-X POST -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/integrators/
```

### Path

POST /integrators

### Description

Create a integrator and return the created object.

### Body parameters

Parameter | Type | Required | Description
-------- | ---- | --------- | ----------
name | string | yes
integrator_type | [string enum](#post-integrator-1)* | yes
description | string | no
last_key | string | no
current_key | string | no
next_key | string | no
key_lifetime | number | no
next_rotation_on | date | no

See [integrator response attributes](#response-integrator).

#### <a name="post-integrator-1"></a>string enum*
- application
- swch_internal
- cust_internal


## Update integrator

```javascript
const integrator = await session.updateIntegrator(1,{
  "name": "mzBYqBKKLrJJyLxJtzAkoiUGQkMnZUZoCDXdBuooxyjvXGhPZ",
  "integrator_type": "cust_internal",
  "description": "Swi",
  "last_key": "vYP0MfKwZfaZVui8ZkxPi/h7Nh0S3NRxOv73PuGfXuE=",
  "current_key": "16hcR0mqjCQi79sXo0XXPRCu5oHD9QPEBlWT7ZRkk5A=",
  "next_key": "+uzbFGRSma3bXe+a/s1JHOMMuGkSZlr//xwbu/P/7mw=",
  "key_lifetime": 103,
  "next_rotation_on": "1981-03-24T12:12:41.536Z"
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "name", "mzBYqBKKLrJJyLxJtzAkoiUGQkMnZUZoCDXdBuooxyjvXGhPZ" },
	{ "integrator_type", "cust_internal" },
	{ "description", "Swi" },
	{ "last_key", "vYP0MfKwZfaZVui8ZkxPi/h7Nh0S3NRxOv73PuGfXuE=" },
	{ "current_key", "16hcR0mqjCQi79sXo0XXPRCu5oHD9QPEBlWT7ZRkk5A=" },
	{ "next_key", "+uzbFGRSma3bXe+a/s1JHOMMuGkSZlr//xwbu/P/7mw=" },
	{ "key_lifetime", 103 },
	{ "next_rotation_on", "1981-03-24T12:12:41.536Z" }
};

CardSavrResponse<Integrator> integrator = await http.UpdateIntegratorAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("name", "mzBYqBKKLrJJyLxJtzAkoiUGQkMnZUZoCDXdBuooxyjvXGhPZ" )
	.add("integrator_type", "cust_internal" )
	.add("description", "Swi" )
	.add("last_key", "vYP0MfKwZfaZVui8ZkxPi/h7Nh0S3NRxOv73PuGfXuE=" )
	.add("current_key", "16hcR0mqjCQi79sXo0XXPRCu5oHD9QPEBlWT7ZRkk5A=" )
	.add("next_key", "+uzbFGRSma3bXe+a/s1JHOMMuGkSZlr//xwbu/P/7mw=" )
	.add("key_lifetime", 103 )
	.add("next_rotation_on", "1981-03-24T12:12:41.536Z" )
	.build();
JsonValue integrator = session.put("/integrators", body, null, null);
```

```shell
curl -d "{\"name\":\"mzBYqBKKLrJJyLxJtzAkoiUGQkMnZUZoCDXdBuooxyjvXGhPZ\",\"integrator_type\":\"cust_internal\",\"description\":\"Swi\",\"last_key\":\"vYP0MfKwZfaZVui8ZkxPi/h7Nh0S3NRxOv73PuGfXuE=\",\"current_key\":\"16hcR0mqjCQi79sXo0XXPRCu5oHD9QPEBlWT7ZRkk5A=\",\"next_key\":\"+uzbFGRSma3bXe+a/s1JHOMMuGkSZlr//xwbu/P/7mw=\",\"key_lifetime\":103,\"next_rotation_on\":\"1981-03-24T12:12:41.536Z\"}"
-X PUT -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/integrators/1560055497
```

### Path

PUT /integrators OR /integrators/{id}

### Description

Update a integrator and return the updated object.  An id is required on every update request.

### Body parameters

Parameter | Type | Description 
-------- | ---- | ---------
name | string |
integrator_type | [string enum](#post-integrator-1)* |
description | string |
last_key | string |
current_key | string |
next_key | string |
key_lifetime | number |
next_rotation_on | date |

See [integrator response parameters](#response-integrator).


## Delete integrator

```shell
curl -X DELETE
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/integrators/1560055497
```

```javascript
await session.deleteIntegrator(1560055497);
```

```csharp
CardSavrResponse<Integrator> integrator = await http.DeleteIntegratorAsync(1560055497);
```

```java
JsonValue integrator = session.delete("/integrators", 1560055497, null);
```

### Path

DELETE /integrators/{id}

### Description

Delete a integrator and purge its [related items](#cascading-delete).  An id is required on every delete request.

See [integrator response parameters](#response-integrator).


# Merchant sites
Merchant site objects contain information and images related to CardSavr-supported merchant sites.
## Get merchant site

```shell
curl -H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/merchant_sites/835639991
```

```javascript
const merchantsites = await session.getMerchantSites(835639991);
```

```csharp
CardSavrResponse<MerchantSites> merchantsites = await session.GetMerchantSitesAsync(835639991);
```

```java
JsonValue merchantsites = session.get("/merchant_sites", 835639991, null, null);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 835639991,
  "name": "cELCjggTuQVxHswykew",
  "host": "oTm",
  "images": [
    {
      "ipXPJIONPYmI": "u30i.5=uDO~",
      "ZWTKHUiAbIix": 38,
      "tPYlgsxqBWVZ": true
    },
    {
      "XedJgParkwmz": "t4",
      "jGKxCGPcJWdR": 70,
      "XuqAMtnQtClL": true
    },
    {
      "FpyqeqKXRBOD": "@qF>4B=(0po&CIcDbM/Fqtpkxnc)r*Y#",
      "ENMeOCxFhpXz": 98,
      "qmWQPdHjADsP": true
    }
  ],
  "mfa": true,
  "tags": "fmpXixHxyQOCZntvAus",
  "proxy_order": [
    "i80HbM",
    25,
    "s=~3/KV{3~77@L.%.mH07/sxezm^)H"
  ],
  "quick_start": true,
  "login": {
    "wvVKxXnlpJmL": "&^LwG8@+t",
    "avHYwUbITlnC": 54,
    "TneYGdklwCVm": true
  },
  "required_form_fields": [
    "dTr=llG/yue0hG7u4{@WI2^Mv[GV",
    62,
    "HK%N"
  ],
  "login_page": "bcetDkmMBEWlNAnEPgG",
  "forgot_password_page": "tkuo",
  "credit_card_page": "ODnTHbJlqXAUzOoHJvckZwsyrW"
}
```

### Path

GET /merchant_sites **(batch)** or GET /merchant_sites/:id **(singular)**

### Description

Returns the merchant site specified by the provided ID

#### Batch GET requests

**Batch requests** return the first page of all viewable merchant sites, filtered by any [query filters](#get-filters) listed in the path.

**Example batch GET request path:**<br>`/merchant_sites?ids=1,2`

#### Singular GET requests

**Singular requests** only return the merchant site matching the id provided in the path.

**Example GET request path:**<br>`/merchant_sites/835639991`

### <a name="response-merchant_site"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number | 
name | string | 
host | string | 
images | array | 
mfa | boolean | 
tags | string | 
proxy_order | array | 
quick_start | boolean | 
login | object | 
required_form_fields | array | 
login_page | string | 
forgot_password_page | string | 
credit_card_page | string | 

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

### Filter parameters
- ids / id (in path)
- exclude_ids
- top_ids
- name_starts_with
- hosts
- host
- exclude_hosts
- top_hosts
- host_starts_with
- tags

# Notifications
A notification record that defines how to take action on CardSavr events like jobs completing or sessions ending.
## Get notification

```shell
curl -H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/notifications/869048620
```

```javascript
const notifications = await session.getNotifications(869048620);
```

```csharp
CardSavrResponse<Notifications> notifications = await session.GetNotificationsAsync(869048620);
```

```java
JsonValue notifications = session.get("/notifications", 869048620, null, null);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 869048620,
  "name": "BBJptzVsXpEeaZqbElcaQBSXDkIMYcZegkNoaSUShRwltYxYQKVQZNyrFPpNGCS",
  "type": "webhook",
  "event": "webhook_error_summary",
  "config": {
    "mEwIpThsivEV": "!5mkdHKX3u9ITADd$9fIwZC",
    "jyLiELyGIcTp": 67,
    "QfTPUciwJcst": true
  },
  "html_template": "QsgLPOtrwrCleMMFQkagyfOzdPCtoLC",
  "text_template": "UcaVbCluPqbE",
  "created_on": "1993-12-03T04:57:58.741Z",
  "last_updated_on": "1999-09-20T01:05:57.686Z",
  "financial_institution_id": 1524956992
}
```

### Path

GET /notifications **(batch)** or GET /notifications/:id **(singular)**

### Description

Returns the notification specified by the provided ID

#### Batch GET requests

**Batch requests** return the first page of all viewable notifications, filtered by any [query filters](#get-filters) listed in the path.

**Example batch GET request path:**<br>`/notifications?ids=1,2`

#### Singular GET requests

**Singular requests** only return the notification matching the id provided in the path.

**Example GET request path:**<br>`/notifications/869048620`

### <a name="response-notification"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number | 
name | string | 
type | string | 
event | string | 
config | object | 
html_template | string | 
text_template | string | 
created_on | date | Date this notification was created on
last_updated_on | date | Date this notification was last updated on
financial_institution_id | number (fk) | 

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

### Filter parameters
- ids / id (in path)
- financial_institution_ids
- names
- type
- events
- event
- created_on_min / created_on_max
- last_updated_on_min / last_updated_on_max

## Create notification

```javascript
const notification = await session.createNotification({
  "financial_institution_id": 1524956992,
  "name": "BBJptzVsXpEeaZqbElcaQBSXDkIMYcZegkNoaSUShRwltYxYQKVQZNyrFPpNGCS",
  "type": "webhook",
  "event": "webhook_error_summary",
  "config": {
    "mEwIpThsivEV": "!5mkdHKX3u9ITADd$9fIwZC",
    "jyLiELyGIcTp": 67,
    "QfTPUciwJcst": true
  },
  "html_template": "QsgLPOtrwrCleMMFQkagyfOzdPCtoLC",
  "text_template": "UcaVbCluPqbE"
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "financial_institution_id", 1524956992 },
	{ "name", "BBJptzVsXpEeaZqbElcaQBSXDkIMYcZegkNoaSUShRwltYxYQKVQZNyrFPpNGCS" },
	{ "type", "webhook" },
	{ "event", "webhook_error_summary" },
	{ "html_template", "QsgLPOtrwrCleMMFQkagyfOzdPCtoLC" },
	{ "text_template", "UcaVbCluPqbE" }
};

CardSavrResponse<Notification> notification = await http.CreateNotificationAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("financial_institution_id", 1524956992 )
	.add("name", "BBJptzVsXpEeaZqbElcaQBSXDkIMYcZegkNoaSUShRwltYxYQKVQZNyrFPpNGCS" )
	.add("type", "webhook" )
	.add("event", "webhook_error_summary" )
	.add("html_template", "QsgLPOtrwrCleMMFQkagyfOzdPCtoLC" )
	.add("text_template", "UcaVbCluPqbE" )
	.build();
JsonValue notification = session.post("/notifications", body, null, null);
```

```shell
curl -d "{\"financial_institution_id\":1524956992,\"name\":\"BBJptzVsXpEeaZqbElcaQBSXDkIMYcZegkNoaSUShRwltYxYQKVQZNyrFPpNGCS\",\"type\":\"webhook\",\"event\":\"webhook_error_summary\",\"config\":{\"mEwIpThsivEV\":\"!5mkdHKX3u9ITADd$9fIwZC\",\"jyLiELyGIcTp\":67,\"QfTPUciwJcst\":true},\"html_template\":\"QsgLPOtrwrCleMMFQkagyfOzdPCtoLC\",\"text_template\":\"UcaVbCluPqbE\"}"
-X POST -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/notifications/
```

### Path

POST /notifications

### Description

Create a notification and return the created object.

### Body parameters

Parameter | Type | Required | Description
-------- | ---- | --------- | ----------
financial_institution_id | number | yes
name | string | yes
type | [string enum](#post-notification-1)* | yes
event | [string enum](#post-notification-2)** | yes
config | object | no
html_template | string | no
text_template | string | no

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
  "name": "rlAmrGBZByLkOegXHjCmKfnUFNJVejiABhJFesHmcaGKBxYiQVcwibaFCSpurAm",
  "type": "webhook",
  "event": "merchant_site_updates_all",
  "config": {
    "zMdrKYAYVeZe": "wb>YCyvvZy~p82(s/73",
    "UryhSradaJtG": 86,
    "MZDtYXrmxPES": true
  },
  "html_template": "kNtPfRjtGHQyNKYbCrSNzvVZRSLLxTDT",
  "text_template": "AIIHijfCBEuOiPsVOXjw"
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "name", "rlAmrGBZByLkOegXHjCmKfnUFNJVejiABhJFesHmcaGKBxYiQVcwibaFCSpurAm" },
	{ "type", "webhook" },
	{ "event", "merchant_site_updates_all" },
	{ "html_template", "kNtPfRjtGHQyNKYbCrSNzvVZRSLLxTDT" },
	{ "text_template", "AIIHijfCBEuOiPsVOXjw" }
};

CardSavrResponse<Notification> notification = await http.UpdateNotificationAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("name", "rlAmrGBZByLkOegXHjCmKfnUFNJVejiABhJFesHmcaGKBxYiQVcwibaFCSpurAm" )
	.add("type", "webhook" )
	.add("event", "merchant_site_updates_all" )
	.add("html_template", "kNtPfRjtGHQyNKYbCrSNzvVZRSLLxTDT" )
	.add("text_template", "AIIHijfCBEuOiPsVOXjw" )
	.build();
JsonValue notification = session.put("/notifications", body, null, null);
```

```shell
curl -d "{\"name\":\"rlAmrGBZByLkOegXHjCmKfnUFNJVejiABhJFesHmcaGKBxYiQVcwibaFCSpurAm\",\"type\":\"webhook\",\"event\":\"merchant_site_updates_all\",\"config\":{\"zMdrKYAYVeZe\":\"wb>YCyvvZy~p82(s/73\",\"UryhSradaJtG\":86,\"MZDtYXrmxPES\":true},\"html_template\":\"kNtPfRjtGHQyNKYbCrSNzvVZRSLLxTDT\",\"text_template\":\"AIIHijfCBEuOiPsVOXjw\"}"
-X PUT -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/notifications/869048620
```

### Path

PUT /notifications OR /notifications/{id}

### Description

Update a notification and return the updated object.  An id is required on every update request.

### Body parameters

Parameter | Type | Description 
-------- | ---- | ---------
name | string |
type | [string enum](#post-notification-1)* |
event | [string enum](#post-notification-2)** |
config | object |
html_template | string |
text_template | string |

See [notification response parameters](#response-notification).


## Delete notification

```shell
curl -X DELETE
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/notifications/869048620
```

```javascript
await session.deleteNotification(869048620);
```

```csharp
CardSavrResponse<Notification> notification = await http.DeleteNotificationAsync(869048620);
```

```java
JsonValue notification = session.delete("/notifications", 869048620, null);
```

### Path

DELETE /notifications/{id}

### Description

Delete a notification and purge its [related items](#cascading-delete).  An id is required on every delete request.

See [notification response parameters](#response-notification).


# Notification results
A notification result record that defines how to take action on CardSavr events like jobs completing or sessions ending.
## Get notification result

```shell
curl -H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/notification_results/518311414
```

```javascript
const notificationresults = await session.getNotificationResults(518311414);
```

```csharp
CardSavrResponse<NotificationResults> notificationresults = await session.GetNotificationResultsAsync(518311414);
```

```java
JsonValue notificationresults = session.get("/notification_results", 518311414, null, null);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 518311414,
  "last_attempt_date": "1988-06-20T11:18:29.526Z",
  "fi_lookup_key": "ESWKenIscnTMptNlgMduxCsDdoQbwDdCPjNAneFQYCIioZjxFmwpPoRTGFwkuwn",
  "cuid": "KdIzrSMKOBfrCIVQuBU",
  "status": "failure",
  "attempts": 991379916,
  "notification_data": {
    "NZdPtYtnUCJO": "*BBs7@*XKW0o=YXh0>nM%",
    "XzIPyINyUIFf": 50,
    "kyEWepmoAfKy": true
  },
  "created_on": "2003-01-29T22:36:03.742Z",
  "last_updated_on": "2001-11-17T10:37:56.012Z",
  "notification_id": 2001925646
}
```

### Path

GET /notification_results **(batch)** or GET /notification_results/:id **(singular)**

### Description

Returns the notification result specified by the provided ID

#### Batch GET requests

**Batch requests** return the first page of all viewable notification results, filtered by any [query filters](#get-filters) listed in the path.

**Example batch GET request path:**<br>`/notification_results?ids=1,2`

#### Singular GET requests

**Singular requests** only return the notification result matching the id provided in the path.

**Example GET request path:**<br>`/notification_results/518311414`

### <a name="response-notification_result"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number | 
last_attempt_date | date | Date of last attempt to post this notification result
fi_lookup_key | string | 
cuid | string | 
status | string | 
attempts | number | 
notification_data | object | 
created_on | date | Date this notification result was created on
last_updated_on | date | Date this notification result was last updated on
notification_id | number (fk) | 

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

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

## Create notification result

```javascript
const notificationresult = await session.createNotificationResult({
  "notification_id": 2001925646,
  "fi_lookup_key": "ESWKenIscnTMptNlgMduxCsDdoQbwDdCPjNAneFQYCIioZjxFmwpPoRTGFwkuwn",
  "cuid": "KdIzrSMKOBfrCIVQuBU",
  "status": "failure",
  "attempts": 991379916,
  "notification_data": {
    "NZdPtYtnUCJO": "*BBs7@*XKW0o=YXh0>nM%",
    "XzIPyINyUIFf": 50,
    "kyEWepmoAfKy": true
  }
});
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "notification_id", 2001925646 },
	{ "fi_lookup_key", "ESWKenIscnTMptNlgMduxCsDdoQbwDdCPjNAneFQYCIioZjxFmwpPoRTGFwkuwn" },
	{ "cuid", "KdIzrSMKOBfrCIVQuBU" },
	{ "status", "failure" },
	{ "attempts", 991379916 }
};

CardSavrResponse<NotificationResult> notificationresult = await http.CreateNotificationResultAsync(body);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("notification_id", 2001925646 )
	.add("fi_lookup_key", "ESWKenIscnTMptNlgMduxCsDdoQbwDdCPjNAneFQYCIioZjxFmwpPoRTGFwkuwn" )
	.add("cuid", "KdIzrSMKOBfrCIVQuBU" )
	.add("status", "failure" )
	.add("attempts", 991379916 )
	.build();
JsonValue notificationresult = session.post("/notification_results", body, null, null);
```

```shell
curl -d "{\"notification_id\":2001925646,\"fi_lookup_key\":\"ESWKenIscnTMptNlgMduxCsDdoQbwDdCPjNAneFQYCIioZjxFmwpPoRTGFwkuwn\",\"cuid\":\"KdIzrSMKOBfrCIVQuBU\",\"status\":\"failure\",\"attempts\":991379916,\"notification_data\":{\"NZdPtYtnUCJO\":\"*BBs7@*XKW0o=YXh0>nM%\",\"XzIPyINyUIFf\":50,\"kyEWepmoAfKy\":true}}"
-X POST -H "Content-Type: application/json"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/notification_results/
```

### Path

POST /notification_results

### Description

Create a notification result and return the created object.

### Body parameters

Parameter | Type | Required | Description
-------- | ---- | --------- | ----------
notification_id | number | yes
fi_lookup_key | string | yes
cuid | string | yes
status | [string enum](#post-notification_result-1)* | yes
attempts | number | yes
notification_data | object | no

See [notification result response attributes](#response-notification_result).

#### <a name="post-notification_result-1"></a>string enum*
- success
- failure

# Single-site jobs
A place_card_on_single_site_job object
## Get single-site job

```shell
curl -H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/place_card_on_single_site_jobs/1731098964
```

```javascript
const singlesitejobs = await session.getSingleSiteJobs(1731098964);
```

```csharp
CardSavrResponse<SingleSiteJobs> singlesitejobs = await session.GetSingleSiteJobsAsync(1731098964);
```

```java
JsonValue singlesitejobs = session.get("/place_card_on_single_site_jobs", 1731098964, null, null);
```

> Sample response - not all properties are available to all roles (200 OK):

```json
{
  "id": 1731098964,
  "card_id": 777524022,
  "card_placement_result_id": "ELkirUPicemQfhQbZIgRPWzuEfB",
  "status": "LOGIN_RESUBMITTED",
  "custom_data": {
    "kTMyimAQfhFl": "siE0h5QEFr>gttO",
    "ewCDBevcqezM": 65,
    "loesDfBEugiU": false
  },
  "failure_reason": "ceELpiltfLfAxZgLkKfEckK",
  "messaging_addresses": "wXEsRspi",
  "current_state": "KxGhaWdqjXkBIbGfVTeqUGnONJDnvOwKRsPCkIVuITcsIlSQgBjMXjPozXsEEQk",
  "notification_sent": false,
  "time_elapsed": 1497235508,
  "run_count": 550676684,
  "job_ready_on": "1979-01-16T16:01:48.713Z",
  "started_on": "2004-11-02T10:36:39.165Z",
  "completed_on": "2014-11-07T18:05:12.487Z",
  "expiration_date": "1986-06-25T04:52:15.543Z",
  "created_on": "1996-12-30T00:24:45.696Z",
  "last_updated_on": "2008-08-19T18:38:43.428Z",
  "cardholder_id": 2030885320,
  "account_id": 1775624062,
  "type": "TURBO_MODE"
}
```

### Path

GET /place_card_on_single_site_jobs **(batch)** or GET /place_card_on_single_site_jobs/:id **(singular)**

### Description

Returns the single-site job specified by the provided ID

#### Batch GET requests

**Batch requests** return the first page of all viewable single-site jobs, filtered by any [query filters](#get-filters) listed in the path.

**Example batch GET request path:**<br>`/place_card_on_single_site_jobs?ids=1,2`

#### Singular GET requests

**Singular requests** only return the single-site job matching the id provided in the path.

**Example GET request path:**<br>`/place_card_on_single_site_jobs/1731098964`

### <a name="response-place_card_on_single_site_job"></a>Response attributes

Attribute | Type | Description
------ | ---- | -----------
id | number | 
card_id | number (fk) | 
card_placement_result_id | string | 
status | string | 
custom_data | object | 
failure_reason | string | 
messaging_addresses | string | 
current_state | string | 
notification_sent | boolean | 
time_elapsed | number | 
run_count | number | 
job_ready_on | date | 
started_on | date | 
completed_on | date | 
expiration_date | date | 
created_on | date | Date this site was created on
last_updated_on | date | Date this site was last updated on
cardholder_id | number (fk) | 
account_id | number (fk) | 
type | string | 

NOTE: All foreign key parameters (fk) can be [hydrated](#hydration) and support [cascading delete](#cascading-delete).

### Filter parameters
- ids / id (in path)
- cardholder_ids
- card_ids
- account_ids
- card_placement_result_ids
- type
- status
- status_include / status_exclude
- current_state
- notification_sent
- time_elapsed_min / time_elapsed_max
- run_count_min / run_count_max
- job_ready_on_min / job_ready_on_max
- started_on_min / started_on_max
- completed_on_min / completed_on_max
- expiration_date_min / expiration_date_max
- created_on_min / created_on_max
- last_updated_on_min / last_updated_on_max

## Create single-site job

```javascript
const singlesitejob = await session.createSingleSiteJob({
  "cardholder_id": 2030885320,
  "card_id": 777524022,
  "account_id": 1775624062,
  "type": "TURBO_MODE",
  "status": "LOGIN_RESUBMITTED",
  "custom_data": {
    "kTMyimAQfhFl": "siE0h5QEFr>gttO",
    "ewCDBevcqezM": 65,
    "loesDfBEugiU": false
  },
  "failure_reason": "ceELpiltfLfAxZgLkKfEckK",
  "current_state": "KxGhaWdqjXkBIbGfVTeqUGnONJDnvOwKRsPCkIVuITcsIlSQgBjMXjPozXsEEQk",
  "notification_sent": false,
  "time_elapsed": 1497235508,
  "run_count": 550676684,
  "started_on": "2004-11-02T10:36:39.165Z",
  "completed_on": "2014-11-07T18:05:12.487Z",
  "expiration_date": "1986-06-25T04:52:15.543Z"
}, CARDHOLDER_SAFE_KEY);
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "cardholder_id", 2030885320 },
	{ "card_id", 777524022 },
	{ "account_id", 1775624062 },
	{ "type", "TURBO_MODE" },
	{ "status", "LOGIN_RESUBMITTED" },
	{ "failure_reason", "ceELpiltfLfAxZgLkKfEckK" },
	{ "current_state", "KxGhaWdqjXkBIbGfVTeqUGnONJDnvOwKRsPCkIVuITcsIlSQgBjMXjPozXsEEQk" },
	{ "notification_sent", false },
	{ "time_elapsed", 1497235508 },
	{ "run_count", 550676684 },
	{ "started_on", "2004-11-02T10:36:39.165Z" },
	{ "completed_on", "2014-11-07T18:05:12.487Z" },
	{ "expiration_date", "1986-06-25T04:52:15.543Z" }
};

CardSavrResponse<SingleSiteJob> singlesitejob = await http.CreateSingleSiteJobAsync(body, CARDHOLDER_SAFE_KEY);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("cardholder_id", 2030885320 )
	.add("card_id", 777524022 )
	.add("account_id", 1775624062 )
	.add("type", "TURBO_MODE" )
	.add("status", "LOGIN_RESUBMITTED" )
	.add("failure_reason", "ceELpiltfLfAxZgLkKfEckK" )
	.add("current_state", "KxGhaWdqjXkBIbGfVTeqUGnONJDnvOwKRsPCkIVuITcsIlSQgBjMXjPozXsEEQk" )
	.add("notification_sent", false )
	.add("time_elapsed", 1497235508 )
	.add("run_count", 550676684 )
	.add("started_on", "2004-11-02T10:36:39.165Z" )
	.add("completed_on", "2014-11-07T18:05:12.487Z" )
	.add("expiration_date", "1986-06-25T04:52:15.543Z" )
	.build();
JsonValue singlesitejob = session.post("/place_card_on_single_site_jobs", body, null, null);
```

```shell
curl -d "{\"cardholder_id\":2030885320,\"card_id\":777524022,\"account_id\":1775624062,\"type\":\"TURBO_MODE\",\"status\":\"LOGIN_RESUBMITTED\",\"custom_data\":{\"kTMyimAQfhFl\":\"siE0h5QEFr>gttO\",\"ewCDBevcqezM\":65,\"loesDfBEugiU\":false},\"failure_reason\":\"ceELpiltfLfAxZgLkKfEckK\",\"current_state\":\"KxGhaWdqjXkBIbGfVTeqUGnONJDnvOwKRsPCkIVuITcsIlSQgBjMXjPozXsEEQk\",\"notification_sent\":false,\"time_elapsed\":1497235508,\"run_count\":550676684,\"started_on\":\"2004-11-02T10:36:39.165Z\",\"completed_on\":\"2014-11-07T18:05:12.487Z\",\"expiration_date\":\"1986-06-25T04:52:15.543Z\"}"
-X POST -H "Content-Type: application/json"
-H "x-cardsavr-cardholder-safe-key: CARDHOLDER_SAFE_KEY"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/place_card_on_single_site_jobs/
```

### Path

POST /place_card_on_single_site_jobs

### Description

Create a single-site job and return the created object.

### Body parameters

Parameter | Type | Required | Description
-------- | ---- | --------- | ----------
cardholder_id | number | yes
card_id | number | no
account_id | number | yes
type | [string enum](#post-place_card_on_single_site_job-1)* | no
status | [string enum](#post-place_card_on_single_site_job-2)** | no
custom_data | object | no
failure_reason | string | no
current_state | string | no
notification_sent | boolean | no
time_elapsed | number | no
run_count | number | no
started_on | date | no
completed_on | date | no
expiration_date | date | no

See [single-site job response attributes](#response-place_card_on_single_site_job).

#### <a name="post-place_card_on_single_site_job-1"></a>string enum*
- CARD_PLACEMENT
- TURBO_MODE
- INTEGRATION_TEST
- API_TEST

#### <a name="post-place_card_on_single_site_job-2"></a>string enum**
- INITIATED
- REQUESTED
- IN_PROGRESS
- AUTH
- LOGIN_SUBMITTED
- PENDING_CREDS
- CREDS_RECEIVED
- PENDING_NEWCREDS
- NEWCREDS_RECEIVED
- PENDING_CARD
- LOGIN_RESUBMITTED
- PENDING_TFA
- TFA_CODE_RECEIVED
- TFA_SUBMITTED
- UPDATING
- QUEUED
- NETWORK_ISSUE
- CANCEL_REQUESTED
- CANCELLED
- CANCELLED_QUICKSTART
- ABANDONED
- ABANDONED_QUICKSTART
- KILLED
- ACCOUNT_NOT_SUPPORTED
- COUNTRY_NOT_SUPPORTED
- PREPAID_ACCOUNT
- INACTIVE_ACCOUNT
- INVALID_CARD
- INVALID_ADDRESS
- PASSWORD_RESET_REQUIRED
- BUNDLED_SUBSCRIPTION
- FREE_ACCOUNT
- ACCOUNT_LOCKED
- DUPLICATE_CARD
- INVALID_EXPIRATION_DATE
- EXPIRED_CARD
- INVALID_CVV
- INVALID_NETWORK
- MAX_LIMIT_OF_STORED_CARDS
- SUCCESSFUL
- TIMEOUT_CAPTCHA
- TIMEOUT_CREDENTIALS
- TIMEOUT_TFA
- TOO_MANY_LOGIN_FAILURES
- TOO_MANY_TFA_FAILURES
- UNSUCCESSFUL
- PROXY_PROBE_FAILED
- VBS_TIMEOUT
- VBS_ERROR

<aside class="notice">Update calls to /place_card_on_single_site_jobs require the cardholder's personal cardholder_safe_key header to encrypt and save the safe when Strivve does not manage keys for a customer (this is an environment setting). The safe keys are also not required if updating non-safe user properties.</aside>

## Update single-site job

```javascript
const singlesitejob = await session.updateSingleSiteJob(1,{
  "card_id": 1327445271,
  "status": "LOGIN_SUBMITTED",
  "custom_data": {
    "HEiPkGlCyLnW": "aBT$",
    "pYExolVgKpBE": 68,
    "OsvTLRGuMeTP": false
  },
  "failure_reason": "wCPwXWIxHLvpEMAhwoCLaXiQLAw",
  "current_state": "yTLoCYZPYvVOsukazWOeVDjiykKRMNVJbIDlsGmVrkweqvOVZtzbgiruqvazius",
  "notification_sent": false,
  "time_elapsed": 516400609,
  "run_count": 851878508,
  "started_on": "1988-05-04T06:45:27.558Z",
  "completed_on": "1997-07-06T22:43:37.488Z",
  "expiration_date": "1974-03-26T22:50:14.702Z"
}, CARDHOLDER_SAFE_KEY);
```

```csharp
PropertyBag body = new PropertyBag()
{
	{ "card_id", 1327445271 },
	{ "status", "LOGIN_SUBMITTED" },
	{ "failure_reason", "wCPwXWIxHLvpEMAhwoCLaXiQLAw" },
	{ "current_state", "yTLoCYZPYvVOsukazWOeVDjiykKRMNVJbIDlsGmVrkweqvOVZtzbgiruqvazius" },
	{ "notification_sent", false },
	{ "time_elapsed", 516400609 },
	{ "run_count", 851878508 },
	{ "started_on", "1988-05-04T06:45:27.558Z" },
	{ "completed_on", "1997-07-06T22:43:37.488Z" },
	{ "expiration_date", "1974-03-26T22:50:14.702Z" }
};

CardSavrResponse<SingleSiteJob> singlesitejob = await http.UpdateSingleSiteJobAsync(body, CARDHOLDER_SAFE_KEY);
```

```java
JsonObject body = Json.createObjectBuilder()
	.add("card_id", 1327445271 )
	.add("status", "LOGIN_SUBMITTED" )
	.add("failure_reason", "wCPwXWIxHLvpEMAhwoCLaXiQLAw" )
	.add("current_state", "yTLoCYZPYvVOsukazWOeVDjiykKRMNVJbIDlsGmVrkweqvOVZtzbgiruqvazius" )
	.add("notification_sent", false )
	.add("time_elapsed", 516400609 )
	.add("run_count", 851878508 )
	.add("started_on", "1988-05-04T06:45:27.558Z" )
	.add("completed_on", "1997-07-06T22:43:37.488Z" )
	.add("expiration_date", "1974-03-26T22:50:14.702Z" )
	.build();
JsonValue singlesitejob = session.put("/place_card_on_single_site_jobs", body, null, null);
```

```shell
curl -d "{\"card_id\":1327445271,\"status\":\"LOGIN_SUBMITTED\",\"custom_data\":{\"HEiPkGlCyLnW\":\"aBT$\",\"pYExolVgKpBE\":68,\"OsvTLRGuMeTP\":false},\"failure_reason\":\"wCPwXWIxHLvpEMAhwoCLaXiQLAw\",\"current_state\":\"yTLoCYZPYvVOsukazWOeVDjiykKRMNVJbIDlsGmVrkweqvOVZtzbgiruqvazius\",\"notification_sent\":false,\"time_elapsed\":516400609,\"run_count\":851878508,\"started_on\":\"1988-05-04T06:45:27.558Z\",\"completed_on\":\"1997-07-06T22:43:37.488Z\",\"expiration_date\":\"1974-03-26T22:50:14.702Z\"}"
-X PUT -H "Content-Type: application/json"
-H "cardholder-safe-key: CARDHOLDER_SAFE_KEY"
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/place_card_on_single_site_jobs/1731098964
```

### Path

PUT /place_card_on_single_site_jobs OR /place_card_on_single_site_jobs/{id}

### Description

Update a single-site job and return the updated object.  An id is required on every update request.

### Body parameters

Parameter | Type | Description 
-------- | ---- | ---------
card_id | number |
status | [string enum](#post-place_card_on_single_site_job-2)** |
custom_data | object |
failure_reason | string |
current_state | string |
notification_sent | boolean |
time_elapsed | number |
run_count | number |
started_on | date |
completed_on | date |
expiration_date | date |

See [single-site job response parameters](#response-place_card_on_single_site_job).

<aside class="notice">Update calls to /place_card_on_single_site_jobs require the cardholder's personal cardholder_safe_key header to encrypt and save the safe when Strivve does not manage keys for a customer (this is an environment setting). The safe keys are also not required if updating non-safe properties.</aside>

## Delete single-site job

```shell
curl -X DELETE
-H "x-cardsavr-trace:{\"key\": \"my_trace\"}" -b ~/_cookies -c ~/_cookies
https://api.INSTANCE.cardsavr.io/place_card_on_single_site_jobs/1731098964
```

```javascript
await session.deleteSingleSiteJob(1731098964);
```

```csharp
CardSavrResponse<SingleSiteJob> singlesitejob = await http.DeleteSingleSiteJobAsync(1731098964);
```

```java
JsonValue singlesitejob = session.delete("/place_card_on_single_site_jobs", 1731098964, null);
```

### Path

DELETE /place_card_on_single_site_jobs/{id}

### Description

Delete a single-site job and purge its [related items](#cascading-delete).  An id is required on every delete request.

See [single-site job response parameters](#response-place_card_on_single_site_job).

