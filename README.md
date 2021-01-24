# Noria SMS API Documentation

- [Introduction](#introduction)
- [Sending SMS](#send-sms)
    - [Single SMS (One or More Contacts)](#single-sms)
    - [Customized SMS](#customized-sms)
- [Sent SMS](#sent-sms)
- [Failed SMS](#failed-sms)
- [SMS Delivery Status](#sms-delivery)
- [SMS balance](#sms-balance)

<a name="introduction"></a>
## Introduction
**Noria SMS API** is a minimal Bulk SMS API for Developers. You are not a developer? We have a **End-user SMS portal** for you.

This SMS API currently has the following functionalities:
- Send single SMS to one or more contacts
- Send customized SMS to multiple contacts
- Check the messages sent over time
- Check failed messages
- Check SMS delivery status
- Check SMS balance
- Have multiple developers under single account

In all of the above cases, a personal access token is th only requirement. This token can be obtained from [Profile section](#profile) in the SMS portal.

<a name="send-sms"></a>
## Sending SMS
<a name="single-sms"></a>
### Single SMS (One or More Contacts)
> Relpace `{ApiToken}` with your valid token as obtained from the SMS portal.

**METHOD: POST**

**URL: [http://noriasms.test/api/v1/sms/send](http://noriasms.test/api/v1/sms/send)**

**Headers:**

```
["Authorization: Bearer {APIToken}", "Content-Type: application/json", "Accept: application/json"]
```

**Request Body:**
```
{
    "message": "your message here..."
    "contacts": ["07xxxxxxxx", "07xxxxxxxx", ....]
}
```

#### Sample odes
> The sample codes provided are the ones tested and verified to work. They are just a guidance and can be tweaked to work with any programming language.
##### Laravel
```
...
use Illuminate\Support\Facades\Http;
...

$_URL = "http://noriasms.test/api/v1/sms/send";
$_Token = "{ApiToken}";
$response = Http::withHeaders([
        "Authorization: Bearer $_Token",
        "Content-Type: application/json",
        "Accept: application/json"
    ])->post($_URL, [
        "message" => "Your message here....",
        "contacts" => ["07xxxxxxxx", "07xxxxxxxx", ...]
    ]);
```

#### Python
```
import requests
  
access_token = "{APIToken}"
api_url = "http://noriasms.test/api/v1/sms/send"
headers = {"Authorization": f"Bearer {access_token}", "Content-Type": "application/json", "Accept": "application/json"}
request_data = {
    "message": "Your message here....",
    "contacts": ["07xxxxxxxx", "07xxxxxxxx", ...]
}

response = requests.post(api_url, json = request_data, headers=headers)
```

#### Successful Response
```
{
    "message": "success",
    "code": 200
}
```


<a name="customized-sms"></a>
### Customized SMS
> Relpace `{ApiToken}` with your valid token as obtained from the SMS portal.

**METHOD: POST**

**URL: [http://noriasms.test/api/v1/sms/bulk_send](http://noriasms.test/api/v1/sms/bulk_send)**

**Headers:**

```
["Authorization: Bearer {APIToken}", "Content-Type: application/json", "Accept: application/json"]
```

**Request Body:**
```
{
    "messageList": [
        {
            "message": "Custom message here...",
            "recipient": "07xxxxxxxx"
        },
        {
            "message": "Another custom message....",
            "recipient": "07xxxxxxxx"
        }
    ]
}
```

#### Sample odes
> The sample codes provided are the ones tested and verified to work. They are just a guidance and can be tweaked to work with any programming language.


##### Laravel
```
...
use Illuminate\Support\Facades\Http;
...

$_URL = "ttp://noriasms.test/api/v1/sms/bulk_send";
$_Token = "{ApiToken}";
$response = Http::withHeaders([
        "Authorization: Bearer $_Token",
        "Content-Type: application/json",
        "Accept: application/json"
    ])->post($_URL, [
        "messageList": [
            {
                "message": "Custom message here...",
                "recipient": "07xxxxxxxx"
            },
            {
                "message": "Another custom message....",
                "recipient": "07xxxxxxxx"
            }
        ]
    ]);
```

##### Python
```
import requests
  
access_token = "{APIToken}"
api_url = "http://noriasms.test/api/v1/sms/bulk_send"
headers = {"Authorization": f"Bearer {access_token}", "Content-Type": "application/json", "Accept": "application/json"}
request_data = {
    "messageList": [
        {
            "message": "Custom message here...",
            "recipient": "07xxxxxxxx"
        },
        {
            "message": "Another custom message....",
            "recipient": "07xxxxxxxx"
        }
    ]
}

response = requests.post(api_url, json = request_data, headers=headers)
```

#### Successful Response
```
{
    "message": "success",
    "code": 200
}
```

<a name="sent-sms">
## Sent Messages
All Messages sent are stored in cloud server so that one can be able to track delivery reports and any other relevant data as appropriate. Below is a quick API description to get the sent messages.

> Relpace `{ApiToken}` with your valid token as obtained from the SMS portal.

**METHOD: GET**

**URL: [http://noriasms.test/api/v1/sms/sent](http://noriasms.test/api/v1/sms/sent)**

**Headers:**

```
["Authorization: Bearer {APIToken}", "Content-Type: application/json", "Accept: application/json"]
```

**Request Body: None**

### Sample odes
> The sample codes provided are the ones tested and verified to work. They are just a guidance and can be tweaked to work with any programming language.


#### Laravel
```
...
use Illuminate\Support\Facades\Http;
...

$_URL = "http://noriasms.test/api/v1/sms/sent";
$_Token = "{ApiToken}";
$response = Http::withHeaders([
        "Authorization: Bearer $_Token",
        "Content-Type: application/json",
        "Accept: application/json"
    ])->get($_URL);
```

#### Python
```
import requests
  
access_token = "{APIToken}"
api_url = "http://noriasms.test/api/v1/sms/sent"
headers = {"Authorization": f"Bearer {access_token}", "Content-Type": "application/json", "Accept": "application/json"}

response = requests.get(api_url, headers=headers)
```

#### Successful Response
```
{
    "data": [
        {
            "message_id": "xxxxxxxx",
            "message": "message here...",
            "units": 1,
            "status": "200",
            "response": "success",
            "recipient": "2547xxxxxxxx",
            "date_sent": "23rd Jan, 2021 7:44 PM UTC",
            "date_sent_local": "23rd Jan, 2021 10:44 PM EAT"
        },
        {
            "message_id": "xxxxxxxx",
            "message": "Another message...",
            "units": 1,
            "status": "200",
            "response": "success",
            "recipient": "2547xxxxxxxx",
            "date_sent": "23rd Jan, 2021 7:44 PM UTC",
            "date_sent_local": "23rd Jan, 2021 10:44 PM EAT"
        },
    ]
}
```

<a name="failed-sms">
## Failed Messages
If sending an SMS fail for any reason not caption in the API exceptions, it will saved in the **Failed Messages**. This gives you an opportunity to review the message alongside the cause of failure, as well as resend the messages once the issue is resolved. Below is a quick API description to get the failed messages.

> Relpace `{ApiToken}` with your valid token as obtained from the SMS portal.

**METHOD: GET**

**URL: [http://noriasms.test/api/v1/sms/failed](http://noriasms.test/api/v1/sms/failed)**

**Headers:**

```
["Authorization: Bearer {APIToken}", "Content-Type: application/json", "Accept: application/json"]
```

**Request Body: None**

### Sample odes
> The sample codes provided are the ones tested and verified to work. They are just a guidance and can be tweaked to work with any programming language.


#### Laravel
```
...
use Illuminate\Support\Facades\Http;
...

$_URL = "http://noriasms.test/api/v1/sms/failed";
$_Token = "{ApiToken}";
$response = Http::withHeaders([
        "Authorization: Bearer $_Token",
        "Content-Type: application/json",
        "Accept: application/json"
    ])->get($_URL);
```

#### Python
```
import requests
  
access_token = "{APIToken}"
api_url = "http://noriasms.test/api/v1/sms/failed"
headers = {"Authorization": f"Bearer {access_token}", "Content-Type": "application/json", "Accept": "application/json"}

response = requests.get(api_url, headers=headers)
```

#### Successful Response
```
{
    "data": [
        {
            "id": xx,
            "message": "Message here...",
            "units": 1,
            "status": "400",
            "response": "Bad request",
            "recipient": "07xxxxxxxx",
            "date_failed": "23rd Jan, 2021 8:20 PM UTC",
            "date_failed_local": "23rd Jan, 2021 11:20 PM EAT"
        },
        {
            "id": xx,
            "message": "Another message here...",
            "units": 1,
            "status": "400",
            "response": "Bad request",
            "recipient": "07xxxxxxxx",
            "date_failed": "23rd Jan, 2021 8:20 PM UTC",
            "date_failed_local": "23rd Jan, 2021 11:20 PM EAT"
        }
    ]
}
```

<a name="sms-delivery">
## SMS Delivery Reports
Since all the messages sent are stored in cloud, it is possible to query delivery reports for any message at any given time. Below is a bisic API description to query SMS delivery report.
> Relpace `{ApiToken}` with your valid token as obtained from the SMS portal.

**METHOD: GET**

**URL: [http://noriasms.test/api/v1/sms/delivery](http://noriasms.test/api/v1/sms/delivery)**

**Headers:**

```
["Authorization: Bearer {APIToken}", "Content-Type: application/json", "Accept: application/json"]
```

**Request Body:**
```
{
    "messageID": "53328658"
}
```

### Sample odes
> The sample codes provided are the ones tested and verified to work. They are just a guidance and can be tweaked to work with any programming language.


#### Laravel
```
...
use Illuminate\Support\Facades\Http;
...

$_URL = "http://noriasms.test/api/v1/sms/delivery";
$_Token = "{ApiToken}";
$response = Http::withHeaders([
        "Authorization: Bearer $_Token",
        "Content-Type: application/json",
        "Accept: application/json"
    ])->get($_URL, [
        "messageID": "xxxxxxxx"
    ]);
```

#### Python
```
import requests
  
access_token = "{APIToken}"
api_url = "http://noriasms.test/api/v1/sms/delivery"
headers = {"Authorization": f"Bearer {access_token}", "Content-Type": "application/json", "Accept": "application/json"}
request_data = {
    "messageID": "xxxxxxxx"
}

response = requests.get(api_url, json = request_data, headers=headers)
```

#### Successful Response
```
{
    "status_code": 200,
    "message_id": "xxxxxxxx",
    "recepient": "2547xxxxxxxx",
    "send_time": "2021-01-23 22:45:01",
    "sender_name": "xxxxxx",
    "status": "DeliveredToTerminal"
}
```

<a name="sms-balance">
## SMS Balance
You can check your SMS units balance at any give tion. Below is a quick API description to get the sms units balance for your account.
> Relpace `{ApiToken}` with your valid token as obtained from the SMS portal.

**METHOD: GET**

**URL: [http://noriasms.test/api/v1/sms/balance](http://noriasms.test/api/v1/sms/balance)**

**Headers:**

```
["Authorization: Bearer {APIToken}", "Content-Type: application/json", "Accept: application/json"]
```

**Request Body: None**

### Sample odes
> The sample codes provided are the ones tested and verified to work. They are just a guidance and can be tweaked to work with any programming language.


#### Laravel
```
...
use Illuminate\Support\Facades\Http;
...

$_URL = "http://noriasms.test/api/v1/sms/balance";
$_Token = "{ApiToken}";
$response = Http::withHeaders([
        "Authorization: Bearer $_Token",
        "Content-Type: application/json",
        "Accept: application/json"
    ])->get($_URL);
```

#### Python
```
import requests
  
access_token = "{APIToken}"
api_url = "http://noriasms.test/api/v1/sms/balance"
headers = {"Authorization": f"Bearer {access_token}", "Content-Type": "application/json", "Accept": "application/json"}

response = requests.get(api_url, headers=headers)
```

#### Successful Response
```
{
    "balance": 1389
    "code": 200
}
```
