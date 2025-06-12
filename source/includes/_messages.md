# Client Messages

## Subscribe to Status Updates

> Before you can listen to a channel, you must first subscribe.  Unlike credential requests, multiple clients can listen to messages for the same job.

```javascript
const session = this.getSession(username);
const subscription = await session.registerForJobStatusUpdates(job_id);
//this key is necessary for all future requests
const key = subscription.body.access_key;
```

```csharp
//not implemented
```

```java
//not implemented
```

```shell
#session must first be started, and must have permissions
curl -iv 
  -H "Content-Type: application/json" "https://api.INSTANCE.cardsavr.io/messages/place_card_on_single_site_jobs/123/broadcasts/registrations" 
  -H "x-cardsavr-trace: {\"key\": \"my_trace\"}"  -H "x-cardsavr-session-jwt: {{JWT_TOKEN}}"
```

> access_key is required for all future requests for status updates.  Messages are returned as an array.  status is always job_status

```json
{
    "access_key": "erz5nk219FPZNWGv3AbHdA=="
}
```

### Path
GET /messages/place_card_on_single_site_jobs/job_id:/broadcasts/registrations

### Description
Registers a client to a broadcast message channel.  Messages are saved for an hour waiting for the client to poll.  Generally clients poll every 3-5 seconds.  Multiple clients can poll for messages for the same job, so each client has its own access key.  

Note: Creating a place_card_on_single_site_job will automatically create a subscription to a job and return an access_key.  Thereforce explicit subscription is only for higher privileged agents that didn't actually create the job.

<aside class="notice">
See the <a href="https://developers.strivve.com/resources/job-progress/">Messaging system documention</a> for more details on how the messaging system is architected.  Although these apis can be used to handle messaging, CardSavr provides easier mechanisms for receiving and posting messages via the <a href="#single_site_jobs">job</a> and <a href="#accounts">account</a> apis.
</aside>

## Get Job Status Updates

> The unique access key is returned for every broadcast message poll request

```javascript
const broadcast_probe = setInterval(async () => { 
    const update = await session.getJobStatusUpdate(job_id, subscription.body.access_key);
    if (update.status_code == 401) {
        clearInterval(broadcast_probe);
    } else if (update.body) {
        update.body.map((item: any) => {
            callback(item);   //process message "item"
            if (item.type === "job_status") {
                if (item.message.termination_type || item.message.percent_complete == 100) { //job is completed, stop probing
                    clearInterval(broadcast_probe);
                }
            }
        });
    }
}, 5000);
```

```csharp
Not implemented yet
```

```shell
curl -iv -H "Content-Type: application/json" 
  "https://api.INSTANCE.cardsavr.io/messages/place_card_on_single_site_jobs/123/broadcasts/" 
  -H "cardsavr-messaging-access-key: erz5nk219FPZNWGv3AbHdA=="
  -H "x-cardsavr-trace: {\"key\": \"my_trace\"}"  -H "x-cardsavr-session-jwt: {{JWT_TOKEN}}"
```

> Response is an array, as mutliple messages may be generated between polls.

```json
[
    {
        "type": "job_status",
        "message": {
            "job_timeout": 856058,
            "percent_complete": 30,
            "status": "AUTH"            
        },
        "job_id": 123
    },
    {
        "type": "job_status",
        "message": {
            "job_timeout": 855737,
            "percent_complete": 54,
            "status": "UPDATING"            
        },
        "job_id": 123
    }
]
```

### Path
GET /messages/place_card_on_single_site_jobs/job_id:/broadcasts

### Description
Grabs the status messages for this job.  If there are no messages, none are returned.  Since multiple messages may be returned, the body is an array of messages.  When jobs complete, the final message will have a "termination_type" with values:

Termination type | Description
---------------- | -----------
BILLABLE | Job completed successfully
USER_DATA_FAILURE | There was an issue with data supplied by the cardholder like a TFA code or password
SITE_INTERACTION_FAILURE | Cardsavr was unable to definitively place the card on the site
PROCESS_FAILURE | There was an internal system failure - these happen very rarely and should be escallated immediately


## Get Cardholder Status Updates

> The unique access key is returned for every broadcast message poll request

```javascript
const messages = await session.getCardholderMessages(cardholder_id);
if (messages.body) {
    messages.body.map(async (item) => {
        if (item.type === "job_status") { 
            conssole.log(item.status);
        }
    });
}
```

```csharp
Not implemented yet
```

```java
Not implemented yet
```

```shell
curl -iv -H "Content-Type: application/json" 
  "https://api.INSTANCE.cardsavr.io/messages/cardholders/123/" 
  -H "x-cardsavr-trace: {\"key\": \"my_trace\"}"  -H "x-cardsavr-session-jwt: {{JWT_TOKEN}}"
```

> Response is an array, as mutliple messages from multiple jobs may be generated between polls.

```json
[
    {
        "job_id": "1585",
        "type": "job_status",
        "message": {
            "status": "AUTH",
            "job_timeout": 781440,
            "percent_complete": 5
        }
    },
    {
        "job_id": "1586",
        "type": "job_status",
        "message": {
            "status": "AUTH",
            "job_timeout": 781254,
            "percent_complete": 5
        }
    }
]
```

### Path
GET /messages/cardholders/cardholder_id

### Description
Grabs the status messages for this cardholder.  If there are no messages, none are returned.  When runniung multiple jobs, this is much more efficient mechanism for retrieving messaages.  You do not need to manage acceess_keys since the permissions are managed via the cardholder agent's permissions.  Since multiple job and messages may be returned, the body is an array of messages.  As jobs complete, the final message for each job will have a "termination_type" with values:

Termination type | Description
---------------- | -----------
BILLABLE | Job completed successfully
USER_DATA_FAILURE | There was an issue with data supplied by the cardholder like a TFA code or password
SITE_INTERACTION_FAILURE | Cardsavr was unable to definitively place the card on the site
PROCESS_FAILURE | There was an internal system failure - these happen very rarely and should be escallated immediately

## Get Credential Requests

> Credential requests must be polled for using the job_id.  Permissions are established based on the role and the owner of the job.

```javascript
const request_probe = setInterval(async () => { 
    const request = await session.getJobInformationRequest(job_id);
    if (request.body) {
        callback(request.body); //callback is a function that processes the message.
    }
}, 5000);
```

```csharp
//not implemented
```

```java
// not implemented
```

```shell
# With a shell, you must first establish a sessionby logging in.
# All calls must be accompanied by the session token.  This only works on a dev
# server with authentication optional. 
curl "https://api.INSTANCE.cardsavr.io/messages/place_card_on_single_site_jobs/123/broadcasts" 
  -H "x-cardsavr-trace: {\"key\": \"my_trace\"}"  -H "x-cardsavr-session-jwt: {{JWT_TOKEN}}" 
```


> The response contains a unique request envelope id which must be returned with the response.

```json
{
  "type": "tfa_request",
  "job_id": 101,
  "envelope_id": "uHsa6mI3GYO2ZwOf82SuaA=="
}
```

### Path

GET /messages/place_card_on_single_site_jobs/job_id:/credential_requests

### Description

Polls the server for requests from the virtual browser session.  This might be new credentials or a TFA code.  You must use the envelope_id that was returned with the initial request message.

## Post Credential Response

> Jobs wiill wait until a credential response is posted.

```javascript
const session = this.getSession(username); //session should already be loaded
session.sendJobInformation(job_id, envelope_id, "tfa_response", "1234");
```

```csharp
//not implemented
```

```shell
#session must first be started
curl -iv -X POST -d "{\"envelope_id\": \"uHsa6mI3GYO2ZwOf82SuaA==\", \"type\": \"tfa_request\", \"message\": \"1234\"}" 
  -H "Content-Type: application/json" "https://api.INSTANCE.cardsavr.io/messages/place_card_on_single_site_jobs/123/credential_responses" 
  -H "x-cardsavr-trace: {\"key\": \"my_trace\"}" -H "x-cardsavr-session-jwt: {{JWT_TOKEN}}"
```

> The response returns a 200 if the post succeeds correctly.  There are better mechanisms for posting credentials using
hydrated api calls outlined in the <a href="https://developers.strivve.com/resources/job-progress/">Messaging system documentation</a> 

```json
{
  "type": "credential_response",
  "job_id": 101,
  "envelope_id": "uHsa6mI3GYO2ZwOf82SuaA==",
  "message": "submitted"
}
```

### Path

POST /messages/place_card_on_single_site_jobs/job_id:/credential_responses

### Description

Post the response to a TFA request or a bad credential request

<aside class="notice">
Credential resubmission messages notify the virtual browser session that credentials have been updated. The client application still needs to save the new credentials in the job safe by updating the account.
</aside>

### Body parameters

Parameter | Type | Required | Desription
-------- | ---- | --------- | ----------
envelope_id | string | yes | unique key associated with the original request
type | string | yes | credential_request or tfa_request
message | string | yes | "success" for credential resubmissions, and the tfa code entered by the cardholder for TFA responses
