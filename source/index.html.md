---
title: API Reference
language_tabs:
  - csharp
  - javascript
  - php
  - perl
  - vb
  - http
toc_footers:
  - "<a href='#'>Sign Up for a Developer Key</a>"
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
// Service Reference
using (var client = new SwiftSMS.SendSMSSoapClient())
{
  string messageResponse = client.SendMessage(cellNumber,
    messageBody, accountKey);
}

// Web Client
dynamic body = new ExpandoObject();
body.MessageBody = "Message Body";
body.Reference = "Reference Number";

var url = string.Format("http://smsgateway.ca/services/message.svc/{0}/{1}",
  accountKey, destinationNumber);

using (var wClient = new System.Net.WebClient())
{
    wClient.Encoding = Encoding.UTF8;
    wClient.Headers.Add("content-type", "application/json");

    string messageResponse = wClient.UploadString(url,
      Newtonsoft.Json.JsonConvert.SerializeObject(body));

}
```


```javascript
// uses JQuery library
var postUrl = "http://smsgateway.ca/services/message.svc/"
  + accountKey + "/" + cellNumber
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

$parameters -> CellNumber = cellNumber;
$parameters -> AccountKey = accountKey;
$parameters -> MessageBody = "This is a demonstration of SMSGateway.ca using PHP5.";

$Result = $client->SendMessage($parameters);
?>
```

Sends an SMS message to the given phone number. Returns 'Message queued successfully' on success, or an error message on fail.

### HTTP Request
**POST :** `/services/message.svc/:accountKey/:destinationNumber`


Parameter|Description|Location
------|------|-----
accountKey|Your Swift SMS Gateway account key|URL
destinationNumber|Cell number to receive the text message|URL
MessageBody|Body of the message to send|BODY
Reference|Internal reference number|BODY

### Returns
`string`

Response|Description
-----|-----
Message queued successfully|Your message has been queued and will be sent
Account key was not found|Your account key was missing - Message will not be sent
Credit rule not found|You attempted to send a message to a region you do not have permission to.  Please contact your account manager to check regions. - Message will not be sent
Insufficient Credits|You do not have enough credits to send this message - Message will not be sent

## SendMessageExtended
Sends an SMS message to the given phone number. Returns an instance of an SMSSendMessageResponse

## SendMessageMultiRoute
Sends an SMS message to the given phone number using two upstream routes to maximize chances for delivery of extremely high priority messages. Returns 'Message queued successfully' on success, or an error message on fail.

## SendMessageViaDedicatedNumber
Sends an SMS message to the given phone number from the specified sender number. The SenderNumber must be a dedicated longcode associated with your account. Returns 'Message queued successfully' on success, or an error message on fail.

## SendMessageViaDedicatedNumberExtended
Sends an SMS message to the given phone number from the specified sender number. The SenderNumber must be a dedicated longcode associated with your account. Returns 'Message queued successfully' on success, or an error message on fail.

## SendMessageWithPriority
Sends an SMS message to the given phone number. Queue priority is set based on Priority parameter - 1 gives high priority, 2 is normal, 3 gives low priority. Returns 'Message queued successfully' on success, or an error message on fail.
<aside class="notice">
 Available only on our API 2 and API 3 Plans.
</aside>

## SendMessageWithPriorityExtended
Sends an SMS message to the given phone number. Queue priority is set based on Priority parameter - 1 gives high priority, 2 is normal, 3 gives low priority. Returns an instance of an SMSSendMessageResponse
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
