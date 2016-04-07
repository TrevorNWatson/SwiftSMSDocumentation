---
title: API Reference
language_tabs:
  - javascript
  - javascript : node.js 
  - php
  - vb : vb.net
  - shell: cURL
  - csharp : C#
toc_footers:
  - "<a href='http://smsgateway.ca'>Sign up for an account</a>"
  - "<a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>"
includes:
  - errors
search: true
---

# Introduction
Welcome to the Swift SMS Gateway API! You can use our API to send SMS messages anywhere in the world.

We have language bindings in C#, javascript, php, perl, and VB! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/tripit/slate). Feel free to edit it and use it as a base for your own API's documentation.

To use the Swift SMS Gateway API, please sign up for an account at [http://smsgateway.ca](http://smsgateway.ca)

# Sending a SMS message
## SendMessage

```csharp
// Service Reference / SOAP
using (var client = new SwiftSMS.SendSMSSoapClient())
{
  string response = client.SendMessage(destinationNumber,
    messageBody, accountKey);
}

// Web Client / REST
dynamic body = new ExpandoObject();
body.MessageBody = "Message Body";
body.Reference = "Reference Number";

var url = string.Format("http://smsgateway.ca/services/message.svc/{0}/{1}",
  accountKey, destinationNumber);

using (var wClient = new System.Net.WebClient())
{
    wClient.Encoding = Encoding.UTF8;
    wClient.Headers.Add("content-type", "application/json");

    string response = wClient.UploadString(url,
      Newtonsoft.Json.JsonConvert.SerializeObject(body));

}
```


```javascript
// uses JQuery library
var postUrl = "http://smsgateway.ca/services/message.svc/"
  + accountKey + "/" + destinationNumber
var body = JSON.stringify({
  MessageBody: "Message Body",
  Reference: "Reference Number"
});
$.ajax({
    url: postUrl,
    method: "POST",
    contentType: "application/json;charset=UTF-8",
    data: body
}).done(function(response) {
  alert(response);
}).error(function (xhr, textStatus, errorThrown) {
  alert (xhr.responseText);
});
```

```php
<?php
// using SOAP Module - http://ca3.php.net/soap

class SMSParam {
    public $CellNumber;
    public $AccountKey;
    public $MessageBody;
}

$client = new SoapClient('http://www.smsgateway.ca/sendsms.asmx?WSDL');
$parameters = new SMSParam;

$parameters -> CellNumber = destinationNumber;
$parameters -> AccountKey = accountKey;
$parameters -> MessageBody = "This is a demonstration of SMSGateway.ca using PHP5.";

$Result = $client->SendMessage($parameters);
?>
```

```shell
Simple HTTP GET:
curl "http://smsgateway.ca/SendSMS.aspx?CellNumber=[destinationNumber]&AccountKey=[accountKey]&MessageBody=[messageBody]"

HTTP POST:
curl -H "Content-Type: application/json" -X POST \
     "http://smsgateway.ca/services/message.svc/[accountKey]/[destination]" \
     --data "{\"MessageBody\": \"[messageBody]\", \"Reference\": \"[reference]\"}"
```

```vb
'Using Service Reference (SOAP)
Using client = New SwiftSMS.SendSMSSoapClient
    Dim response = client.SendMessage(destinationNumber, messageBody, accountKey)
End Using

'Using Webclient (REST)    
Dim url = String.Format("http://smsgateway.ca/services/message.svc/{0}/{1}", accountKey, destinationNumber)
Dim body = String.Format("{{ ""MessageBody"": ""{0}"", ""Reference"" : ""{1}"" }}", messageBody, reference)

Using wClient = New Net.WebClient
    wClient.Encoding = New UTF8Encoding()
    wClient.Headers.Add("content-type", "application/json")

    Dim wResponse = wClient.UploadString(url, body)
End Using
```

Sends an SMS message to the given phone number. Returns 'Message queued successfully' on success, or an error message on fail.

### HTTP Request
**POST :** `/services/message.svc/:accountKey/:destinationNumber`


Parameter|Description|Location
------|------|-----
accountKey|Your Swift SMS Gateway account key|URL
destinationNumber|Cell number to receive the text message|URL
messageBody|Body of the message to send|BODY
reference|Internal reference number|BODY

### Returns
`string`

Response|Description
-----|-----
Message queued successfully|Your message has been queued and will be sent
Account key was not found|Your account key was missing - Message will not be sent
Credit rule not found|You attempted to send a message to a region you do not have permission to.  Please contact your account manager to check regions. - Message will not be sent
Insufficient Credits|You do not have enough credits to send this message - Message will not be sent
Message body was missing|Your message contained no content to send - Message will not be sent

## SendMessageExtended
```csharp
// Service Reference / SOAP
using (var client = new SwiftNew.SendSMSSoapClient())
{
    var response = client.SendMessageExtended(destinationNumber, messageBody, accountKey);
}

// Web Client / REST
dynamic body = new ExpandoObject();
body.MessageBody = "Message Body";
body.Reference = "Reference Number";

var url = string.Format("http://smsgateway.ca/services/message.svc/{0}/{1}/Extended", 
    accountKey, destinationNumber);

using (var wClient = new System.Net.WebClient())
{
    wClient.Encoding = Encoding.UTF8;
    wClient.Headers.Add("content-type", "application/json");

    string response = wClient.UploadString(url,
        Newtonsoft.Json.JsonConvert.SerializeObject(body));
}
```


```javascript
// uses JQuery library
var postUrl = "http://smsgateway.ca/services/message.svc/"
    + accountKey + "/" + destinationNumber + "/Extended"
var body = JSON.stringify({
  MessageBody: "Message Body",
  Reference: "Reference Number"
});
$.ajax({
    url: postUrl,
    method: "POST",
    contentType: "application/json;charset=UTF-8",
    data: body
}).done(function(response) {
  alert(response);
}).error(function (xhr, textStatus, errorThrown) {
  alert (xhr.responseText);
});

```

```php
<?php
// using SOAP Module - http://ca3.php.net/soap

class SMSParam {
    public $CellNumber;
    public $AccountKey;
    public $MessageBody;
}

$client = new SoapClient('http://www.smsgateway.ca/sendsms.asmx?WSDL');
$parameters = new SMSParam;

$parameters -> CellNumber = destinationNumber;
$parameters -> AccountKey = accountKey;
$parameters -> MessageBody = "This is a demonstration of SMSGateway.ca using PHP5.";

$Result = $client->SendMessageExtended($parameters);
?>
```

```shell
HTTP POST:
curl -H "Content-Type: application/json" -X POST \
     "http://smsgateway.ca/services/message.svc/[accountKey]/[destination]/Extended" \
     --data "{\"MessageBody\": \"[messageBody]\", \"Reference\": \"[reference]\"}"
```

```vb
' Service Reference (SOAP)
Using client = New SwiftSMS.SendSMSSoapClient
    Dim response = client.SendMessageExtended(destinationNumber, messageBody, accountKey)
End Using

' WebClient (REST)
Dim url = String.Format("http://smsgateway.ca/services/message.svc/{0}/{1}/Extended",
                        accountKey, destinationNumber)
Dim body = String.Format("{{ ""MessageBody"": ""{0}"", ""Reference"" : ""{1}"" }}",
                            messageBody, reference)

Using wClient = New Net.WebClient
    wClient.Encoding = New UTF8Encoding()
    wClient.Headers.Add("content-type", "application/json")

    Dim wResponse = wClient.UploadString(url, body)
End Using
```

Sends an SMS message to the given phone number. Returns an instance of an SMSSendMessageResponse

### HTTP Request
POST: /services/message.svc/:accountKey/:destinationNumber/Extended 

### Returns
`SMSSendMessageResponse`

Field|Type|Description
-----|-----|-----
ErrorMessage|string|Empty if successful, description (see [SendMessage](#sendmessage)) if failure
MessageID|long|Unique Message ID of queued message
MessagesRemaining|int|Credits remaining on your account
QueuedSuccessfully|boolean|True if message was queued


## SendMessageMultiRoute

```csharp
// Service Reference / SOAP
using (var client = new SwiftSMS.SendSMSSoapClient())
{
  string response = client.SendMessageMultiRoute(destinationNumber,
    messageBody, accountKey);
}

// Web Client / REST
dynamic body = new ExpandoObject();
body.MessageBody = "Message Body";
body.Reference = "Reference Number";

var url = string.Format("http://smsgateway.ca/services/message.svc/{0}/{1}/Multi",
  accountKey, destinationNumber);

using (var wClient = new System.Net.WebClient())
{
    wClient.Encoding = Encoding.UTF8;
    wClient.Headers.Add("content-type", "application/json");

    string response = wClient.UploadString(url,
      Newtonsoft.Json.JsonConvert.SerializeObject(body));

}
```


```javascript
// uses JQuery library
var postUrl = "http://smsgateway.ca/services/message.svc/"
  + accountKey + "/" + destinationNumber + "/Multi";
var body = JSON.stringify({
  MessageBody: "Message Body",
  Reference: "Reference Number"
});
$.ajax({
    url: postUrl,
    method: "POST",
    contentType: "application/json;charset=UTF-8",
    data: body
}).done(function(response) {
  alert(response);
}).error(function (xhr, textStatus, errorThrown) {
  alert (xhr.responseText);
});
```

```php
<?php
// using SOAP Module - http://ca3.php.net/soap

class SMSParam {
    public $CellNumber;
    public $AccountKey;
    public $MessageBody;
}

$client = new SoapClient('http://www.smsgateway.ca/sendsms.asmx?WSDL');
$parameters = new SMSParam;

$parameters -> CellNumber = destinationNumber;
$parameters -> AccountKey = accountKey;
$parameters -> MessageBody = "This is a demonstration of SMSGateway.ca using PHP5.";

$Result = $client->SendMessageMultiRoute($parameters);
?>
```

```shell

HTTP POST:
curl -H "Content-Type: application/json" -X POST \
     "http://smsgateway.ca/services/message.svc/[accountKey]/[destination]/ViaDedicated" \
     --data "{\"MessageBody\": \"[messageBody]\", \"Reference\": \"[reference]\"}"
```

```vb
'Using Service Reference (SOAP)
Using client = New SwiftSMS.SendSMSSoapClient
    Dim response = client.SendMessageMultiRoute(destinationNumber, messageBody, accountKey)
End Using

'Using Webclient (REST)    
Dim url = String.Format("http://smsgateway.ca/services/message.svc/{0}/{1}/Multi", accountKey, destinationNumber)
Dim body = String.Format("{{ ""MessageBody"": ""{0}"", ""Reference"" : ""{1}"" }}", messageBody, reference)

Using wClient = New Net.WebClient
    wClient.Encoding = New UTF8Encoding()
    wClient.Headers.Add("content-type", "application/json")

    Dim wResponse = wClient.UploadString(url, body)
End Using
```

Sends an SMS message to the given phone number using two upstream routes to maximize chances for delivery of extremely high priority messages.

### HTTP Request
POST: /services/message.svc/:accountKey/:destinationNumber/Multi 

### Returns
`string`

See [SendMessage](#sendmessage)

## SendMessageViaDedicatedNumber
```csharp
// Service Reference / SOAP
using (var client = new SwiftNew.SendSMSSoapClient())
{
    var response = client.SendMessageViaDedicatedNumber(destinationNumber, messageBody, accountKey,
        reference, sendingNumber);

}

// Web Client / REST
dynamic body = new ExpandoObject();
body.MessageBody = "Message Body";
body.Reference = "Reference Number";
body.SenderNumber = sendingNumber;

var url = string.Format("http://smsgateway.ca/services/message.svc/{0}/{1}/ViaDedicated", 
    accountKey, destinationNumber);

using (var wClient = new System.Net.WebClient())
{
    wClient.Encoding = Encoding.UTF8;
    wClient.Headers.Add("content-type", "application/json");

    string response = wClient.UploadString(url,
        Newtonsoft.Json.JsonConvert.SerializeObject(body));
}
```


```javascript
// uses JQuery library
var postUrl = "http://smsgateway.ca/services/message.svc/"
  + accountKey + "/" + destinationNumber + "/ViaDedicated";
var body = JSON.stringify({
  MessageBody: "Message Body",
  Reference: "Reference Number",
  SendingNumber: "[sendingNumber]"
});
$.ajax({
    url: postUrl,
    method: "POST",
    contentType: "application/json;charset=UTF-8",
    data: body
}).done(function(response) {
  alert(response);
}).error(function (xhr, textStatus, errorThrown) {
  alert (xhr.responseText);
});
```

```php
<?php
// using SOAP Module - http://ca3.php.net/soap

class SMSParam {
    public $CellNumber;
    public $AccountKey;
    public $MessageBody;
    public $SendingNumber;
}

$client = new SoapClient('http://www.smsgateway.ca/sendsms.asmx?WSDL');
$parameters = new SMSParam;

$parameters -> CellNumber = destinationNumber;
$parameters -> AccountKey = accountKey;
$parameters -> MessageBody = "This is a demonstration of SMSGateway.ca using PHP5.";
$parameters -> SendingNumber = sendingNumber;

$Result = $client->SendMessageViaDedicatedNumber($parameters);
?>

```

```shell
HTTP POST:
curl -H "Content-Type: application/json" -X POST \
     "http://smsgateway.ca/services/message.svc/[accountKey]/[destination]/ViaDedicated" \
     --data "{\"MessageBody\": \"[messageBody]\", \"Reference\": \"[reference]\", \"SendingNumber\", \"[sendingNumber]\"}"
```

```vb
' Service Reference (SOAP)
Using client = New SwiftSMS.SendSMSSoapClient
    Dim response = client.SendMessageViaDedicatedNumber(destinationNumber, messageBody,
                    accountKey, reference, sendingNumber)
End Using

' WebClient (REST)
Dim url = String.Format("http://smsgateway.ca/services/message.svc/{0}/{1}/ViaDedicated",
                        accountKey, destinationNumber)
Dim body = String.Format("{{ ""MessageBody"": ""{0}"", " & _
                         "   ""Reference"" : ""{1}"", " & _
                         "   ""SendingNumber"" : ""{2}"" }}",
                         messageBody, reference, sendingNumber)

Using wClient = New Net.WebClient
    wClient.Encoding = New UTF8Encoding()
    wClient.Headers.Add("content-type", "application/json")

    Dim wResponse = wClient.UploadString(url, body)
End Using
```

Sends an SMS message to the given phone number from the specified sender number. The SenderNumber must be a dedicated longcode associated with your account.  View your dedicated numbers in your control panel at [http://smsgateway.ca](http://smsgateway.ca)

### HTTP Request
POST: /services/message.svc/{0}/{1}/ViaDedicated

### Returns
`string`

See [SendMessage](#sendmessage)

## SendMessageViaDedicatedNumberExtended

```csharp
// Service Reference / SOAP
using (var client = new SwiftNew.SendSMSSoapClient())
{
    var response = client.SendMessageViaDedicatedNumberExtended(destinationNumber, messageBody, accountKey,
        reference, sendingNumber);

}

// Web Client / REST
/** NOT CURRENTLY AVAILABLE **/
```


```javascript
// uses JQuery library
/** NOT CURRENTLY AVAILABLE **/
```

```php
<?php
// using SOAP Module - http://ca3.php.net/soap

class SMSParam {
    public $CellNumber;
    public $AccountKey;
    public $MessageBody;
    public $SendingNumber;
}

$client = new SoapClient('http://www.smsgateway.ca/sendsms.asmx?WSDL');
$parameters = new SMSParam;

$parameters -> CellNumber = destinationNumber;
$parameters -> AccountKey = accountKey;
$parameters -> MessageBody = "This is a demonstration of SMSGateway.ca using PHP5.";
$parameters -> SendingNumber = sendingNumber;

$Result = $client->SendMessageViaDedicatedNumberExtended($parameters);
?>

```

```shell
HTTP POST:
### NOT CURRENTLY AVAILABLE ###
```

```vb
' Service Reference (SOAP)
Using client = New SwiftSMS.SendSMSSoapClient
    Dim response = client.SendMessageViaDedicatedNumberExtended(destinationNumber, messageBody,
                    accountKey, reference, sendingNumber)
End Using

' WebClient (REST)
'** NOT CURRENTLY AVAILABLE **'
```

Sends an SMS message to the given phone number from the specified sender number. The SenderNumber must be a dedicated longcode associated with your account.

### Returns
`SMSSendMessageResponse`

See [SendMessageExtended](#sendmessageextended)

## SendMessageWithPriority
```csharp
// Priority Enum
private enum Priorities
{
    High = 1,
    Normal = 2,
    Low = 3
}

const Priorities priority = Priorities.Normal;

// Service Reference / SOAP
using (var client = new SwiftNew.SendSMSSoapClient())
{
    var response = client.SendMessageWithPriority(destinationNumber, messageBody, accountKey,
        reference, (int)priority);

}

// Web Client / REST
dynamic body = new ExpandoObject();
body.MessageBody = "Message Body";
body.Reference = "Reference Number";

var url = string.Format("http://smsgateway.ca/services/message.svc/{0}/{1}/priority/{2}", 
    accountKey, destinationNumber, (int)priority);

using (var wClient = new System.Net.WebClient())
{
    wClient.Encoding = Encoding.UTF8;
    wClient.Headers.Add("content-type", "application/json");

    string response = wClient.UploadString(url,
        Newtonsoft.Json.JsonConvert.SerializeObject(body));
}
```


```javascript
const HighPriority = 1;
const NormalPriority = 2;
const LowPriority = 3;

// uses JQuery library
var postUrl = "http://smsgateway.ca/services/message.svc/"
  + accountKey + "/" + destinationNumber + "/priority/" + NormalPriority;
var body = JSON.stringify({
  MessageBody: "Message Body",
  Reference: "Reference Number"
});
$.ajax({
    url: postUrl,
    method: "POST",
    contentType: "application/json;charset=UTF-8",
    data: body
}).done(function(response) {
  alert(response);
}).error(function (xhr, textStatus, errorThrown) {
  alert (xhr.responseText);
});

```

```php
<?php
// using SOAP Module - http://ca3.php.net/soap
const HighPriority = 1;
const NormalPriority = 2;
const LowPriority = 3;

class SMSParam {
    public $CellNumber;
    public $AccountKey;
    public $MessageBody;
    public $Priority;
}

$client = new SoapClient('http://www.smsgateway.ca/sendsms.asmx?WSDL');
$parameters = new SMSParam;

$parameters -> CellNumber = destinationNumber;
$parameters -> AccountKey = accountKey;
$parameters -> MessageBody = "This is a demonstration of SMSGateway.ca using PHP5.";
$parameters -> Priority = NormalPriority;

$Result = $client->SendMessageWithPriority($parameters);
?>
```

```shell

```

```vb
  
```

Sends an SMS message to the given phone number. Queue priority is set based on Priority parameter - 1 gives high priority, 2 is normal, 3 gives low priority. 

Messages with a higher priority will be preferred over your normal messages. 

### Returns
`string`

See [SendMessage](#sendmessage)

<aside class="notice">
 Available only on our API 2 and API 3 Plans.
</aside>

## SendMessageWithPriorityExtended
Sends an SMS message to the given phone number. Queue priority is set based on Priority parameter - 1 gives high priority, 2 is normal, 3 gives low priority. 

Messages with a higher priority will be preferred over your normal messages. 

### Returns
`SMSSendMessageResponse`

See [SendMessageExtended](#sendmessageextended)

<aside class="notice">
 Available only on our API 2 and API 3 Plans.
</aside>

## SendMessageWithReference
Sends an SMS message to the given phone number. Returns 'Message queued successfully' on success, or an error message on fail.

## SendMessageWithReferenceExtended
Sends an SMS message to the given phone number. Returns an instance of an SMSSendMessageResponse

## SendMultiMessageWithReference
Sends an SMS message to the given phone number using two upsteam routes to maximize chances for delivery of extremely high priority messages.

# Sending Unicode SMS Messages

## SendUnicodeMessage
Sends an SMS message containing Unicode characters to the given phone number. Limit of 70 characters per message. Useful for sending accented characters. Returns 'Message queued successfully' on success, or an error message on fail.

## SendUnicodeMessageExtended
Sends an SMS message to the given phone number. Returns an instance of an SMSSendMessageResponse

## SendUnicodeMessageMulti
Sends an SMS message to the given phone number using two upsteam routes to maximize chances for delivery of extremely high priority messages.

# Sending a MMS

## SendMultimediaMessage
Sends an MMS message to the given phone number. Returns 'Message queued successfully' on success, or an error message on fail.


# Bulk SMS Sending

## SendBulkMessage
Sends an SMS message to all the cell numbers provided. Returns the number of messages successfully queued, or an error message on failure.

<aside class="notice">
 Available only on our API 2 and API 3 Plans.
</aside>

## SendBulkMessageWithOptions
Sends an SMS message to all the cell numbers provided. Supported options are the following MsgContentType=Unicode | Ascii, AllowMessageSplit=True | False (Ascii and False being default if no arguments are passed), SenderID=. Returns the number of messages successfully queued, or an error message on failure.

<aside class="notice">
 Available only on our API 2 and API 3 Plans.
</aside>

## SendBulkUnicodeMessage
Sends an SMS message to all the cell numbers provided. Returns the number of messages successfully queued, or an error message on failure.

<aside class="notice">
 Available only on our API 2 and API 3 Plans.
</aside>

## SendDistinctBulkMessages
Sends distinct SMS messages to all the cell numbers provided. Returns the number of messages successfully queued, or an error message on failure.

<aside class="notice">
 Available only on our API 2 and API 3 Plans.
</aside>

## SendDistinctBulkMessagesViaDedicatedNumber
Sends distinct SMS messages to all the cell numbers provided from the dedicated numbers requested. Returns the number of messages successfully queued, or an error message on failure.

<aside class="notice">
 Available only on our API 2 and API 3 Plans.
</aside>

## SendTemplatedBulkMessageWithOptions
 Sends an SMS message to all the cell numbers provided. Message can contain parameters arrays in a format (eg. <1>, or <2>). Args is an array of arrays with each row having the same number of columns as cell numbers. Supported options are the following MsgContentType=Unicode | Ascii, AllowMessageSplit=True | False (Ascii and False being default if no arguments are passed). Returns the number of messages successfully queued, or an error message on failure.

 <aside class="notice">
  Available only on our API 2 and API 3 Plans.
 </aside>

# Retrieve Incoming Messages

## GetIncomingMessages
Get a list of incoming messages

## GetIncomingMessagesAfterID
Get a list of incoming messages which arrived after the message with the given ID.

## GetIncomingMessagesAfterIDExtended
Get a list of incoming messages which arrived after the message with the given ID. Includes destination phone number.

## GetIncomingMessagesByReference
Get a list of incoming messages which match the given reference

## GetIncomingMessagesByReferenceAfterID
Get a list of incoming messages with the given Reference which arrived after the message with the given ID.

## GetRepliesToMessage
Get a list of incoming messages which have been matched to the given outbound message ID.


# Account Information

##  GetCreditsUsedInDateRange
Get a count of message credits used by an account between the given dates

## GetRemainingMessageCount
Returns the number of messages currently waiting in queue at our gateway. Returns -1 on error.

## GetRemainingMessageCount
Get a count of remaining message credits on the given account

## MoveCreditsToClient
Available only on our Enterprise Service Plan. Move message credits from a master account to a client account

<aside class="notice">
 Available only on our API 3 Plans.
</aside>

# Get the status of a message

## GetOutgoingMessage
Get the status of an outgoing message by suppying the message ID and account key

# Get the status of a sent message

## GetSentMessages
Returns an array of the X most recently sent SMS Messages

## GetSentMessagesAfterID
Returns an array of (at most 1000) sent SMS Messages with IDs greater than the given one.

## GetSentMessagesAfterIDSimple
Returns an array of (at most 1000) sent SMS Messages with IDs greater than the given one in strings with fields separated by the tilde (~) character. Field order is MessageID~CellNumber~MessageBody~SentDate~Success~Reference.

## GetSentMessagesByReference
Returns an array of (at most 1000) sent SMS Messages with the given reference value.

## GetSentMessagesByReferenceAfterID
Returns an array of (at most 1000) sent SMS Messages with the given reference value which also have IDs greater than the given one.

# Get the status of an Unsent Message

## GetUnsentMessages
Returns an array of unsent SMS Messages queued between the given dates


# Lookup Number Information


## HLRLookup
Returns details about the carrier of the given North American phone number.

<aside class="notice">
 Available only on our API 2 and API 3 Plans.
</aside>

## HLRLookupBulk
Returns details about the carrier of the given North American phone number.

<aside class="notice">
 Available only on our API 2 and API 3 Plans.
</aside>

## LRNLookup
Returns details about the carrier of the given North American phone number.

<aside class="notice">
 Available only on our API 2 and API 3 Plans.
</aside>

## LRNLookupBulk
Returns details about the carrier of the given North American phone number.

<aside class="notice">
 Available only on our API 2 and API 3 Plans.
</aside>

## LookupNumber
Please use LRNLookup or HLRLookup

<aside class="notice">
 Available only on our API 2 and API 3 Plans.
</aside>

## LookupNumberThenSend
Performs a lookup on the given number and only if the number is wireless, an SMS is sent. Returns 'Message queued successfully' on successful send, or an error message on fail.

<aside class="notice">
 Available only on our API 2 and API 3 Plans.
</aside>


# Authentication
> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`
<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Kittens
## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request
`GET http://example.com/api/kittens`

### Query Parameters

Parameter    | Default | Description
------------ | ------- | --------------------------------------------------------------------------------
include_cats | false   | If set to true, the result will also include cats.
available    | true    | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.
<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request
`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | --------------------------------
ID        | The ID of the kitten to retrieve
