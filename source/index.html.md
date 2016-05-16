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
  MessageBody: "Message Body"
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
     --data "{ \"MessageBody\": \"[messageBody]\" }"
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

**GET :** `/SendSMS.aspx?CellNumber=[destinationNumber]&AccountKey=[accountKey]&MessageBody=[messageBody]`


Parameter|Description|Location
------|------|-----
AccountKey|Your Swift SMS Gateway account key|URL
DestinationNumber|Cell number to receive the text message|URL
MessageBody|Body of the message to send|BODY


### Returns
`string`

Response|Description
-----|-----
Message queued successfully|Your message has been queued and will be sent
Cell number is invalid|The cell number was not supplied or was too short.
Message body was missing|No message was supplied. We do not permit sending blank SMS messages.
The account key parameter was not valid|The account key was not supplied or or was less than 9 characters.
This account is disabled|The specified account has been disabled by our administrator for violating one or more of our policies.
Account key not found|The specified account key cannot be found. Please verify the key and try again.
There are no messages remaining on this account|You will need to purchase additional messages.
No authorized credit plan found to match this phone number. Please check the number, and ensure you are authorized to send messages to this region|By default, accounts are authorized to send to certain countries only. Please contact us to find out how to send to other regions.
Credit rule not found|You attempted to send a message to a region you do not have permission to.  Please contact your account manager to check regions. - Message will not be sent
Message content is not acceptable, message not sent|Please contact us for details
Time of day at destination falls outside the established time restrictions for your account, message not sent.|For Enterprise level accounts only - optional time-of-day windows can be created to restrict sending.


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

Parameter|Description|Location
------|------|-----
AccountKey|Your Swift SMS Gateway account key|URL
DestinationNumber|Cell number to receive the text message|URL
MessageBody|Body of the message to send|BODY
Reference|Internal Reference ID|BODY

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

Parameter|Description|Location
------|------|-----
AccountKey|Your Swift SMS Gateway account key|URL
DestinationNumber|Cell number to receive the text message|URL
MessageBody|Body of the message to send|BODY
Reference|Internal Reference ID|BODY

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
POST: /services/message.svc/:accountKey/:destinationNumber/ViaDedicated

Parameter|Description|Location
------|------|-----
AccountKey|Your Swift SMS Gateway account key|URL
DestinationNumber|Cell number to receive the text message|URL
MessageBody|Body of the message to send|BODY
Reference|Internal Reference ID|BODY
SendingNumber|Sender ID (Long code number) to send the message via|BODY

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


Parameter|Description|Location
------|------|-----
AccountKey|Your Swift SMS Gateway account key|URL
DestinationNumber|Cell number to receive the text message|URL
MessageBody|Body of the message to send|BODY
Reference|Internal Reference ID|BODY
SendingNumber|Sender ID (Long code number) to send the message via|BODY

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
HTTP POST:
curl -H "Content-Type: application/json" -X POST \
     "http://smsgateway.ca/services/message.svc/[accountKey]/[destination]/priority/[priority]" \
     --data "{\"MessageBody\": \"[messageBody]\", \"Reference\": \"[reference]\" }"
```

```vb
Enum Priorities
    High = 1
    Normal = 2
    Low = 3
End Enum
Dim priority = Priorities.Normal

' Service Reference (SOAP)
Using client = New SwiftSMS.SendSMSSoapClient
    Dim response = client.SendMessageWithPriority(destinationNumber, messageBody,
                    accountKey, reference, Convert.ToInt32(priority))
End Using

' WebClient (REST)
Dim url = String.Format("http://smsgateway.ca/services/message.svc/{0}/{1}/priority/{2}",
                        accountKey, destinationNumber, Convert.ToInt32(priority))
Dim body = String.Format("{{ ""MessageBody"": ""{0}"", " & _
                            "   ""Reference"" : ""{1}"", " & _
                            "   ""SendingNumber"" : ""{2}"" }}",
                            messageBody, reference, sendingNumber)

Using wClient = New Net.WebClient
    wClient.Encoding = New UTF8Encoding()
    wClient.Headers.Add("content-type", "application/json")

    Dim wResponse = wClient.UploadString(url, body)
End Using

End Sub
```

Sends an SMS message to the given phone number. Queue priority is set based on Priority parameter - 1 gives high priority, 2 is normal, 3 gives low priority. 

Messages with a higher priority will be preferred over your normal messages. 

### HTTP Request
POST: /services/message.svc/:accountKey/:destinationNumber/priority/:priority

Parameter|Description|Location
------|------|-----
AccountKey|Your Swift SMS Gateway account key|URL
DestinationNumber|Cell number to receive the text message|URL
Prority|Priority of message.  1 = High  2 = Normal  3 = Low|URL
MessageBody|Body of the message to send|BODY
Reference|Internal Reference ID|BODY

### Returns
`string`

See [SendMessage](#sendmessage)

<aside class="notice">
 Available only on our API 2 and API 3 Plans.
</aside>

## SendMessageWithPriorityExtended
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
    var response = client.SendMessageWithPriorityExtended(destinationNumber, messageBody, accountKey,
        reference, (int)priority);

}

// Web Client / REST
dynamic body = new ExpandoObject();
body.MessageBody = "Message Body";
body.Reference = "Reference Number";

var url = string.Format("http://smsgateway.ca/services/message.svc/{0}/{1}/PriorityExtended/{2}", 
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
  + accountKey + "/" + destinationNumber + "/PriorityExtended/" + NormalPriority;
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

$Result = $client->SendMessageWithPriorityExtended($parameters);
?>
```

```shell
HTTP POST:
curl -H "Content-Type: application/json" -X POST \
     "http://smsgateway.ca/services/message.svc/[accountKey]/[destination]/PriorityExtended/[priority]" \
     --data "{\"MessageBody\": \"[messageBody]\", \"Reference\": \"[reference]\" }"
```

```vb
Enum Priorities
    High = 1
    Normal = 2
    Low = 3
End Enum
Dim priority = Priorities.Normal

' Service Reference (SOAP)
Using client = New SwiftSMS.SendSMSSoapClient
    Dim response = client.SendMessageWithPriorityExtended(destinationNumber, messageBody,
                    accountKey, reference, Convert.ToInt32(priority))
End Using

' WebClient (REST)
Dim url = String.Format("http://smsgateway.ca/services/message.svc/{0}/{1}/PriorityExtended/{2}",
                        accountKey, destinationNumber, Convert.ToInt32(priority))
Dim body = String.Format("{{ ""MessageBody"": ""{0}"", " & _
                            "   ""Reference"" : ""{1}"", " & _
                            "   ""SendingNumber"" : ""{2}"" }}",
                            messageBody, reference, sendingNumber)

Using wClient = New Net.WebClient
    wClient.Encoding = New UTF8Encoding()
    wClient.Headers.Add("content-type", "application/json")

    Dim wResponse = wClient.UploadString(url, body)
End Using

End Sub
```

Sends an SMS message to the given phone number. Queue priority is set based on Priority parameter - 1 gives high priority, 2 is normal, 3 gives low priority. 

Messages with a higher priority will be preferred over your normal messages. 

### HTTP Request
POST: /services/message.svc/:accountKey/:destinationNumber/PriorityExtended/:priority

Parameter|Description|Location
------|------|-----
AccountKey|Your Swift SMS Gateway account key|URL
DestinationNumber|Cell number to receive the text message|URL
Prority|Priority of message.  1 = High  2 = Normal  3 = Low|URL
MessageBody|Body of the message to send|BODY
Reference|Internal Reference ID|BODY


### Returns
`SMSSendMessageResponse`

See [SendMessageExtended](#sendmessageextended)

<aside class="notice">
 Available only on our API 2 and API 3 Plans.
</aside>

## SendMessageWithReference

```csharp
// Service Reference / SOAP
using (var client = new SwiftNew.SendSMSSoapClient())
{
    var response = client.SendMessageWithReference(destinationNumber, messageBody, accountKey,
        reference);

}

// Web Client / REST
dynamic body = new ExpandoObject();
body.MessageBody = messageBody;
body.Reference = reference;

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
  Reference: "reference"
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
    public $Reference;
}

$client = new SoapClient('http://www.smsgateway.ca/sendsms.asmx?WSDL');
$parameters = new SMSParam;

$parameters -> CellNumber = destinationNumber;
$parameters -> AccountKey = accountKey;
$parameters -> MessageBody = "This is a demonstration of SMSGateway.ca using PHP5.";
$parameters -> Reference = refrence;

$Result = $client->SendMessageWithReference($parameters);
?>

```

```shell
HTTP POST:
curl -H "Content-Type: application/json" -X POST \
     "http://smsgateway.ca/services/message.svc/[accountKey]/[destination]" \
     --data "{\"MessageBody\": \"[messageBody]\", \"Reference\": \"[reference]\"}"
```

```vb
' Service Reference (SOAP)
Using client = New SwiftSMS.SendSMSSoapClient
    Dim response = client.SendMessageWithReference(destinationNumber, messageBody,
                    accountKey, reference)
End Using

' WebClient (REST)
Dim url = String.Format("http://smsgateway.ca/services/message.svc/{0}/{1}",
                        accountKey, destinationNumber)
Dim body = String.Format("{{ ""MessageBody"": ""{0}"", " & _
                         "   ""Reference"" : ""{1}"" }}",
                            messageBody, reference)

Using wClient = New Net.WebClient
    wClient.Encoding = New UTF8Encoding()
    wClient.Headers.Add("content-type", "application/json")

    Dim wResponse = wClient.UploadString(url, body)
End Using
```

Sends an SMS message to the given phone number. Allows adding a "Reference" which can be used in the future to retrieve outgoing information or incoming replies.

### HTTP Request
POST: /services/message.svc/:accountKey/:destinationNumber

Parameter|Description|Location
------|------|-----
AccountKey|Your Swift SMS Gateway account key|URL
DestinationNumber|Cell number to receive the text message|URL
MessageBody|Body of the message to send|BODY
Reference|Internal Reference ID|BODY

### Returns
`string`

See [SendMessage](#sendmessage)

## SendMessageWithReferenceExtended


```csharp
// Service Reference / SOAP
using (var client = new SwiftNew.SendSMSSoapClient())
{
    var response = client.SendMessageWithReferenceExtended(destinationNumber, messageBody, accountKey,
        reference);

}

// Web Client / REST
dynamic body = new ExpandoObject();
body.MessageBody = messageBody;
body.Reference = reference;

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
  + accountKey + "/" + destinationNumber + "/Extended";
var body = JSON.stringify({
  MessageBody: "Message Body",
  Reference: "reference"
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
    public $Reference;
}

$client = new SoapClient('http://www.smsgateway.ca/sendsms.asmx?WSDL');
$parameters = new SMSParam;

$parameters -> CellNumber = destinationNumber;
$parameters -> AccountKey = accountKey;
$parameters -> MessageBody = "This is a demonstration of SMSGateway.ca using PHP5.";
$parameters -> Reference = refrence;

$Result = $client->SendMessageWithReferenceExtended($parameters);
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
    Dim response = client.SendMessageWithReferenceExtended(destinationNumber, messageBody,
                    accountKey, reference)
End Using

' WebClient (REST)
Dim url = String.Format("http://smsgateway.ca/services/message.svc/{0}/{1}/Extended",
                        accountKey, destinationNumber)
Dim body = String.Format("{{ ""MessageBody"": ""{0}"", " & _
                         "   ""Reference"" : ""{1}"" }}",
                         messageBody, reference)

Using wClient = New Net.WebClient
    wClient.Encoding = New UTF8Encoding()
    wClient.Headers.Add("content-type", "application/json")

    Dim wResponse = wClient.UploadString(url, body)
End Using
```

Sends an SMS message to the given phone number.  Allows adding a "Reference" which can be used in the future to retrieve outgoing information or incoming replies.

### HTTP Request
POST: /services/message.svc/:accountKey/:destinationNumber/Extended

Parameter|Description|Location
------|------|-----
AccountKey|Your Swift SMS Gateway account key|URL
DestinationNumber|Cell number to receive the text message|URL
MessageBody|Body of the message to send|BODY
Reference|Internal Reference ID|BODY

### Returns
`SMSSendMessageResponse`

See [SendMessageExtended](#sendmessageextended)

## SendMultiMessageWithReference

```csharp
// Service Reference / SOAP
using (var client = new SwiftNew.SendSMSSoapClient())
{
    var response = client.SendMultiMessageWithReference(destinationNumber, messageBody, accountKey,
        reference);

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
    public $Reference;
}

$client = new SoapClient('http://www.smsgateway.ca/sendsms.asmx?WSDL');
$parameters = new SMSParam;

$parameters -> CellNumber = destinationNumber;
$parameters -> AccountKey = accountKey;
$parameters -> MessageBody = "This is a demonstration of SMSGateway.ca using PHP5.";
$parameters -> Reference = reference;

$Result = $client->SendMultiMessageWithReference($parameters);
?>

```

```shell
HTTP POST:
### NOT CURRENTLY AVAILABLE ###
```

```vb
' Service Reference (SOAP)
Using client = New SwiftSMS.SendSMSSoapClient
    Dim response = client.SendMultiMessageWithReference(destinationNumber, messageBody,
                    accountKey, reference)
End Using

' WebClient (REST)
'** NOT CURRENTLY AVAILABLE **'
```

Sends an SMS message to the given phone number using two upsteam routes to maximize chances for delivery of extremely high priority messages.

Parameter|Description|Location
------|------|-----
AccountKey|Your Swift SMS Gateway account key|URL
DestinationNumber|Cell number to receive the text message|URL
MessageBody|Body of the message to send|BODY
Reference|Internal Reference ID|BODY

### Returns
`string`

See [SendMessage](#sendmessage)

# Sending Unicode SMS Messages

## SendUnicodeMessage

```csharp
// Service Reference / SOAP
using (var client = new SwiftSMS.SendSMSSoapClient())
{
    var response = client.SendUnicodeMessage(destinationNumber,
        messageBody, accountKey, reference);
}

// Web Client / REST
dynamic body = new ExpandoObject();
body.MessageBody = messageBody;
body.Reference = reference;

var url = string.Format("http://smsgateway.ca/services/message.svc/{0}/{1}/Unicode",
    accountKey, destinationNumber);

using (var wClient = new System.Net.WebClient())
{
    wClient.Encoding = Encoding.UTF8;
    wClient.Headers.Add("content-type", "application/json");

    var response = wClient.UploadString(url,
        Newtonsoft.Json.JsonConvert.SerializeObject(body));
}
```

```javascript
// uses JQuery library
var postUrl = "http://smsgateway.ca/services/message.svc/"
  + accountKey + "/" + destinationNumber = "/Unicode";
var body = JSON.stringify({
  MessageBody: "Message Body",
  Reference: "Reference"
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
    public $Reference;
}

$client = new SoapClient('http://www.smsgateway.ca/sendsms.asmx?WSDL');
$parameters = new SMSParam;

$parameters -> CellNumber = destinationNumber;
$parameters -> AccountKey = accountKey;
$parameters -> MessageBody = "This is a demonstration of SMSGateway.ca using PHP5.";
$parameters -> AccountKey = reference;

$Result = $client->SendUnicodeMessage($parameters);
?>

```

```shell
HTTP POST:
curl -H "Content-Type: application/json" -X POST \
     "http://smsgateway.ca/services/message.svc/[accountKey]/[destination]/Unicode" \
     --data "{\"MessageBody\": \"[messageBody]\", \"Reference\": \"[reference]\"}"
```

```vb
' Service Reference (SOAP)
Using client = New SwiftSMS.SendSMSSoapClient
    Dim response = client.SendUnicodeMessage(destinationNumber, messageBody,
                    accountKey, reference)
End Using

' WebClient (REST)
Dim url = String.Format("http://smsgateway.ca/services/message.svc/{0}/{1}/Unicode",
                        accountKey, destinationNumber)
Dim body = String.Format("{{ ""MessageBody"": ""{0}"", " & _
                            "   ""Reference"" : ""{1}"" }}",
                            messageBody, reference)

Using wClient = New Net.WebClient
    wClient.Encoding = New UTF8Encoding()
    wClient.Headers.Add("content-type", "application/json")

    Dim wResponse = wClient.UploadString(url, body)
End Using
```

Sends an SMS message containing Unicode characters to the given phone number. Limit of 70 characters per message. Useful for sending accented characters.

### HTTP Request
POST: /services/message.svc/:accountKey/:destinationNumber/Unicode 

Parameter|Description|Location
------|------|-----
AccountKey|Your Swift SMS Gateway account key|URL
DestinationNumber|Cell number to receive the text message|URL
MessageBody|Body of the message to send|BODY
Reference|Internal Reference ID|BODY

### Returns
`string`

See [SendMessage](#sendmessage)

## SendUnicodeMessageExtended

```csharp
// Service Reference / SOAP
using (var client = new SwiftSMS.SendSMSSoapClient())
{
    var response = client.SendUnicodeMessageExtended(destinationNumber,
        messageBody, accountKey, reference);
}

// Web Client / REST
dynamic body = new ExpandoObject();
body.MessageBody = messageBody;
body.Reference = reference;

var url = string.Format("http://smsgateway.ca/services/message.svc/{0}/{1}/UnicodeExtended",
    accountKey, destinationNumber);

using (var wClient = new System.Net.WebClient())
{
    wClient.Encoding = Encoding.UTF8;
    wClient.Headers.Add("content-type", "application/json");

    var response = wClient.UploadString(url,
        Newtonsoft.Json.JsonConvert.SerializeObject(body));
}
```

```javascript
// uses JQuery library
var postUrl = "http://smsgateway.ca/services/message.svc/"
  + accountKey + "/" + destinationNumber = "/UnicodeExtended";
var body = JSON.stringify({
  MessageBody: "Message Body",
  Reference: "Reference"
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
    public $Reference;
}

$client = new SoapClient('http://www.smsgateway.ca/sendsms.asmx?WSDL');
$parameters = new SMSParam;

$parameters -> CellNumber = destinationNumber;
$parameters -> AccountKey = accountKey;
$parameters -> MessageBody = "This is a demonstration of SMSGateway.ca using PHP5.";
$parameters -> AccountKey = reference;

$Result = $client->SendUnicodeMessageExtended($parameters);
?>

```

```shell
HTTP POST:
curl -H "Content-Type: application/json" -X POST \
     "http://smsgateway.ca/services/message.svc/[accountKey]/[destination]/UnicodeExtended" \
     --data "{\"MessageBody\": \"[messageBody]\", \"Reference\": \"[reference]\"}"
```

```vb
' Service Reference (SOAP)
Using client = New SwiftSMS.SendSMSSoapClient
    Dim response = client.SendUnicodeMessageExtended(destinationNumber, messageBody,
                    accountKey, reference)
End Using

' WebClient (REST)
Dim url = String.Format("http://smsgateway.ca/services/message.svc/{0}/{1}/UnicodeExtended",
                        accountKey, destinationNumber)
Dim body = String.Format("{{ ""MessageBody"": ""{0}"", " & _
                            "   ""Reference"" : ""{1}"" }}",
                            messageBody, reference)

Using wClient = New Net.WebClient
    wClient.Encoding = New UTF8Encoding()
    wClient.Headers.Add("content-type", "application/json")

    Dim wResponse = wClient.UploadString(url, body)
End Using
```

Sends an SMS message containing Unicode characters to the given phone number. Limit of 70 characters per message. Useful for sending accented characters. 

### HTTP Request
POST: /services/message.svc/:accountKey/:destinationNumber/UnicodeExtended

Parameter|Description|Location
------|------|-----
AccountKey|Your Swift SMS Gateway account key|URL
DestinationNumber|Cell number to receive the text message|URL
MessageBody|Body of the message to send|BODY
Reference|Internal Reference ID|BODY

### Returns
`SMSSendMessageResponse`

See [SendMessageExtended](#sendmessageextended)


## SendUnicodeMessageMulti

```csharp
// Service Reference / SOAP
using (var client = new SwiftSMS.SendSMSSoapClient())
{
    var response = client.SendUnicodeMessageMulti(destinationNumber,
        messageBody, accountKey, reference);
}

// Web Client / REST
dynamic body = new ExpandoObject();
body.MessageBody = messageBody;
body.Reference = reference;

var url = string.Format("http://smsgateway.ca/services/message.svc/{0}/{1}/MultiUnicode",
    accountKey, destinationNumber);

using (var wClient = new System.Net.WebClient())
{
    wClient.Encoding = Encoding.UTF8;
    wClient.Headers.Add("content-type", "application/json");

    var response = wClient.UploadString(url,
        Newtonsoft.Json.JsonConvert.SerializeObject(body));
}
```

```javascript
// uses JQuery library
var postUrl = "http://smsgateway.ca/services/message.svc/"
  + accountKey + "/" + destinationNumber = "/MultiUnicode";
var body = JSON.stringify({
  MessageBody: "Message Body",
  Reference: "Reference"
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
    public $Reference;
}

$client = new SoapClient('http://www.smsgateway.ca/sendsms.asmx?WSDL');
$parameters = new SMSParam;

$parameters -> CellNumber = destinationNumber;
$parameters -> AccountKey = accountKey;
$parameters -> MessageBody = "This is a demonstration of SMSGateway.ca using PHP5.";
$parameters -> AccountKey = reference;

$Result = $client->SendUnicodeMessageMulti($parameters);
?>

```

```shell
HTTP POST:
curl -H "Content-Type: application/json" -X POST \
     "http://smsgateway.ca/services/message.svc/[accountKey]/[destination]/MultiUnicode" \
     --data "{\"MessageBody\": \"[messageBody]\", \"Reference\": \"[reference]\"}"
```

```vb
' Service Reference (SOAP)
Using client = New SwiftSMS.SendSMSSoapClient
    Dim response = client.SendUnicodeMessageMulti(destinationNumber, messageBody,
                    accountKey, reference)
End Using

' WebClient (REST)
Dim url = String.Format("http://smsgateway.ca/services/message.svc/{0}/{1}/MultiUnicode",
                        accountKey, destinationNumber)
Dim body = String.Format("{{ ""MessageBody"": ""{0}"", " & _
                            "   ""Reference"" : ""{1}"" }}",
                            messageBody, reference)

Using wClient = New Net.WebClient
    wClient.Encoding = New UTF8Encoding()
    wClient.Headers.Add("content-type", "application/json")

    Dim wResponse = wClient.UploadString(url, body)
End Using
```

Sends a Unicode SMS message to the given phone number using two upsteam routes to maximize chances for delivery of extremely high priority messages.

### HTTP Request
POST: /services/message.svc/:accountKey/:destinationNumber/MultiUnicode 

Parameter|Description|Location
------|------|-----
AccountKey|Your Swift SMS Gateway account key|URL
DestinationNumber|Cell number to receive the text message|URL
MessageBody|Body of the message to send|BODY
Reference|Internal Reference ID|BODY

### Returns
`string`

See [SendMessage](#sendmessage)


# Sending a MMS

## SendMultimediaMessage

```csharp
// Service Reference / SOAP
using (var client = new SwiftSMS.SendSMSSoapClient())
{
    var response = var response = client.SendMultimediaMessage(destinationNumber,
        "http://location.of/mms_image.jpg", accountKey);
}

// Web Client / REST
dynamic body = new ExpandoObject();
body.URLOfContent = "http://location.of/mms_image.jpg";

var url = string.Format("http://smsgateway.ca/services/message.svc/{0}/{1}/MMS",
    accountKey, destinationNumber);

using (var wClient = new System.Net.WebClient())
{
    wClient.Encoding = Encoding.UTF8;
    wClient.Headers.Add("content-type", "application/json");

    var response = wClient.UploadString(url,
        Newtonsoft.Json.JsonConvert.SerializeObject(body));
}
```

```javascript
// uses JQuery library
var postUrl = "http://smsgateway.ca/services/message.svc/"
  + accountKey + "/" + destinationNumber = "/MMS";
var body = JSON.stringify({
    URLOfContent = "http://location.of/mms_image.jpg"
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
    public $URLOfContent;
}

$client = new SoapClient('http://www.smsgateway.ca/sendsms.asmx?WSDL');
$parameters = new SMSParam;

$parameters -> CellNumber = destinationNumber;
$parameters -> AccountKey = accountKey;
$parameters -> URLOfContent = "http://location.of/mms_image.jpg";

$Result = $client->SendMultimediaMessage($parameters);
?>

```

```shell
HTTP POST:
curl -H "Content-Type: application/json" -X POST \
     "http://smsgateway.ca/services/message.svc/[accountKey]/[destination]/MMS" \
     --data "{ \"URLOfContent\": \"http://location.of/mms_image.jpg\" }"
```

```vb
' Service Reference (SOAP)
Using client = New SwiftSMS.SendSMSSoapClient
    Dim response = client.SendMultimediaMessage(destinationNumber,
        "http://location.of/mms_image.jpg", accountKey)
End Using

' WebClient (REST)
Dim url = String.Format("http://smsgateway.ca/services/message.svc/{0}/{1}/MMS",
                        accountKey, destinationNumber)
Dim body = String.Format("{{ ""URLOfContent"": ""http://location.of/mms_image.jpg"" }}")

Using wClient = New Net.WebClient
    wClient.Encoding = New UTF8Encoding()
    wClient.Headers.Add("content-type", "application/json")

    Dim wResponse = wClient.UploadString(url, body)
End Using
```

An MMS message is a multimedia message such as an image, video or audio file. If the recipient's phone supports MMS, this rich content will appear in line with other text messages.

For us to send MMS, the content must be hosted on the Internet and you must supply a URL to retrieve the content. If you have an image you want to send but it's not currently hosted on the Internet, we can host the image for you prior to sending. [Click here for more details](http://smsgateway.ca/Instructions/MediaUploading.aspx). Please confirm the validity of the content before sending. If the content cannot be downloaded, the recipient will not receive the message. We are unable to determine this upon sending and will still need to charge for the message. 

### HTTP Request
POST: /services/message.svc/:accountKey/:destinationNumber/MMS 

Parameter|Description|Location
------|------|-----
AccountKey|Your Swift SMS Gateway account key|URL
DestinationNumber|Cell number to receive the text message|URL
URLOfContent|Fully qualified URL to the image to send via MMS|BODY


### Returns
`string`

See [SendMessage](#sendmessage)

This method may also return

Response|Description
-----|-----
Cannot send MMS outside Canada and US|At this time, we only support sending MMS to Canada and the United States

# Bulk SMS Sending

## SendBulkMessage

```csharp
// Create an "ArrayOfString" object with the numbers to receive the SMS message
var numbers = new SwiftSMS.ArrayOfString { destinationNumber };
 
// Service Reference / SOAP
using (var client = new SwiftSMS.SendSMSSoapClient())
{
    var response = client.SendBulkMessage(accountKey, messageBody, reference, numbers);
}

// Web Client / REST
dynamic body = new ExpandoObject();
body.MessageBody = messageBody;
body.Reference = reference;
body.CellNumbers = numbers;

var url = string.Format("http://smsgateway.ca/services/message.svc/{0}/Bulk",
    accountKey);

using (var wClient = new System.Net.WebClient())
{
    wClient.Encoding = Encoding.UTF8;
    wClient.Headers.Add("content-type", "application/json");

    var response = wClient.UploadString(url,
        Newtonsoft.Json.JsonConvert.SerializeObject(body));
}
```


```javascript
// uses JQuery library
var postUrl = "http://smsgateway.ca/services/message.svc/"
  + accountKey + "/Bulk";
var body = JSON.stringify({
  MessageBody: "Message Body",
  Reference: "Reference Number",
  CellNumbers: [destinationNumber, destinationNumber, ...]
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
    public $AccountKey;
    public $MessageBody;
    public $Reference;
    public $CellNumbers;
}

$client = new SoapClient('http://www.smsgateway.ca/sendsms.asmx?WSDL');
$parameters = new SMSParam;

$parameters -> AccountKey = accountKey;
$parameters -> MessageBody = "This is a demonstration of SMSGateway.ca using PHP5.";
$parameters -> Reference = reference;
$parameters -> CellNumber = (destinationNumber, destinationNumber, ...);

$Result = $client->SendBulkMessage($parameters);
?>
```

```shell

HTTP POST:
curl -H "Content-Type: application/json" -X POST \
     "http://smsgateway.ca/services/message.svc/[accountKey]/Bulk" \
     --data "{\"MessageBody\": \"[messageBody]\", \"Reference\": \"[reference]\", \"CellNumbers\": [\"destinationNumber\", ...]}"
```

```vb
Dim numbers = New ArrayOfString()
numbers.Add(destinationNumber)
' Service Reference (SOAP)
Using client = New SwiftSMS.SendSMSSoapClient
    Dim response = client.SendBulkMessage(accountKey, messageBody, reference, numbers)
End Using

' WebClient (REST)
Dim url = String.Format("http://smsgateway.ca/services/message.svc/{0}/Bulk",
                        accountKey)
Dim body = String.Format("{{ ""MessageBody"": ""{0}"", " & _
                            "   ""Reference"" : ""{1}"", " & _
                            "   ""CellNumbers"": [" & _
                                """" & destinationNumber & """, " & _
                                """" & destinationNumber & """, " & _
                                "..." & "] " & _
                            "}}",
                            messageBody, reference)

Using wClient = New Net.WebClient
    wClient.Encoding = New UTF8Encoding()
    wClient.Headers.Add("content-type", "application/json")

    Dim wResponse = wClient.UploadString(url, body)
End Using
```

Sends an SMS message to all the cell numbers provided. Returns the number of messages successfully queued, or an error message on failure.

### HTTP Request
POST: /services/message.svc/:accountKey/Bulk 

Parameter|Description|Location
------|------|-----
AccountKey|Your Swift SMS Gateway account key|URL
MessageBody|Body of the message to send|BODY
Reference|Internal Reference ID|BODY
CellNumbers|Array of cell numbers to deliver SMS messages to|BODY

### Returns
`string`

If successful, will return "x messages queued successfully"

If unsuccessful, will return an error message: See [SendMessage](#sendmessage)



<aside class="notice">
 Available only on our API 2 and API 3 Plans.
</aside>

## SendBulkMessageWithOptions

```csharp
// Create an "ArrayOfString" object with the numbers to receive the SMS message
var numbers = new SwiftSMS.ArrayOfString { destinationNumber };
var options = new SwiftSMS.ArrayOfString { "MsgContentType=Unicode", "SenderId=" + sendingNumber }
 
// Service Reference / SOAP
using (var client = new SwiftSMS.SendSMSSoapClient())
{
    var response = client.SendBulkMessageWithOptions(accountKey, messageBody, reference, numbers, options);
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
    public $AccountKey;
    public $MessageBody;
    public $Reference;
    public $CellNumbers;
    public $Options;
}

$client = new SoapClient('http://www.smsgateway.ca/sendsms.asmx?WSDL');
$parameters = new SMSParam;

$parameters -> AccountKey = accountKey;
$parameters -> MessageBody = "This is a demonstration of SMSGateway.ca using PHP5.";
$parameters -> Reference = reference;
$parameters -> CellNumber = (destinationNumber, destinationNumber, ...);
$parameters -> Options = ("MsgContentType=Unicode", "SenderId=" + sendingNumber);

$Result = $client->SendBulkMessageWithOptions($parameters);
?>
```

```shell

HTTP POST:
# NOT CURRENTLY AVAILABLE #
```

```vb
Dim numbers = New ArrayOfString()
numbers.Add(destinationNumber)

Dim options = new ArrayOfString()
options.Add("MsgContentType=ASCII")
options.Add("SenderId=" & sendingNumber)

' Service Reference (SOAP)
Using client = New SwiftSMS.SendSMSSoapClient
    Dim response = client.SendBulkMessage(accountKey, messageBody, reference, numbers, options)
End Using

' WebClient (REST)
'** NOT CURRENTLY AVAILABLE **
```

Sends an SMS message to all the cell numbers provided. Returns the number of messages successfully queued, or an error message on failure.



Parameter|Description|Location
------|------|-----
AccountKey|Your Swift SMS Gateway account key|URL
MessageBody|Body of the message to send|BODY
Reference|Internal Reference ID|BODY
CellNumbers|Array of cell numbers to deliver SMS messages to|BODY
Options|Array of strings with each containing [key]=[value]|BODY


### Options
Parameter|Value|Description|Is Default
-----|-----|-----|-----
MsgContentType| |Send message as ASCII or Unicode| 
 |Unicode|Send Unicode Message (allowing the extended character set|
 |ASCII|Send messages using only ASCII characters|Yes

Parameter|Value|Description|Is Default
-----|-----|-----|-----
SenderId| |Phone number of dedicated long code to send your messages from|

Parameter|Value|Description|Is Default
-----|-----|-----|-----
Reference2| |Secondary Reference field.|
 | |If this is an email address, any replies will be send to this address.  This OVERRIDES account settings


### Returns
`string`

If successful, will return "x messages queued successfully"

If unsuccessful, will return an error message: See [SendMessage](#sendmessage)



<aside class="notice">
 Available only on our API 2 and API 3 Plans.
</aside>

## SendBulkUnicodeMessage
```csharp
var numbers = new SwiftSMS.ArrayOfString { destinationNumber, destinationNumber };
// Service Reference / SOAP
using (var client = new SwiftSMS.SendSMSSoapClient())
{
    var response = client.SendBulkUnicodeMessage(accountKey, messageBody, reference, numbers);
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
    public $AccountKey;
    public $MessageBody;
    public $Reference;
    public $CellNumbers;
}

$client = new SoapClient('http://www.smsgateway.ca/sendsms.asmx?WSDL');
$parameters = new SMSParam;

$parameters -> AccountKey = accountKey;
$parameters -> MessageBody = "This is a demonstration of SMSGateway.ca using PHP5.";
$parameters -> Reference = reference;
$parameters -> CellNumber = (destinationNumber, destinationNumber, ...);

$Result = $client->SendBulkUnicodeMessage($parameters);
?>
```

```shell
HTTP POST:
# NOT CURRENTLY AVAILABLE #
```

```vb
Dim numbers = New ArrayOfString()
numbers.Add(destinationNumber)
numbers.Add(destinationNumber)
' Service Reference (SOAP)
Using client = New SwiftSMS.SendSMSSoapClient
    Dim response = client.SendBulkUnicodeMessage(accountKey, messageBody, reference, numbers)
End Using

' WebClient (REST)
' NOT CURRENTLY AVAILABLE
```

Sends an SMS Unicode enabled message to all the cell numbers provided. Returns the number of messages successfully queued, or an error message on failure.

Parameter|Description|Location
------|------|-----
AccountKey|Your Swift SMS Gateway account key|URL
MessageBody|Body of the message to send|BODY
Reference|Internal Reference ID|BODY
CellNumbers|Array of cell numbers to deliver SMS messages to|BODY

### Returns
`string`

If successful, will return "x messages queued successfully"

If unsuccessful, will return an error message: See [SendMessage](#sendmessage)

<aside class="notice">
 Available only on our API 2 and API 3 Plans.
</aside>

## SendDistinctBulkMessages
```csharp
var numbers = new SwiftSMS.ArrayOfString { destinationNumber, destinationNumber };
var messageBodies = new SwiftSMS.ArrayOfString {"Message to recipient 1", "Message to recipient 2"};
// Service Reference / SOAP
using (var client = new SwiftSMS.SendSMSSoapClient())
{
    var response = client.SendDistinctBulkMessages(accountKey, messageBody, numbers, messageBodies);
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
    public $AccountKey;
    public $Reference;
    public $CellNumbers;
    public $MessageBodies;
}

$client = new SoapClient('http://www.smsgateway.ca/sendsms.asmx?WSDL');
$parameters = new SMSParam;

$parameters -> AccountKey = accountKey;
$parameters -> Reference = reference;
$parameters -> CellNumber = (destinationNumber, destinationNumber, ...);
$parameters -> MessageBodies = ("Message to first recipient", "Message to second recipient", ...);

$Result = $client->SendDistinctBulkMessages($parameters);
?>
```

```shell
HTTP POST:
# NOT CURRENTLY AVAILABLE #
```

```vb
Dim numbers = New ArrayOfString()
numbers.Add(destinationNumber)
numbers.Add(destinationNumber)
Dim messageBodies = New ArrayOfString()
messageBodies.Add("Message to first recipient")
messageBodies.Add("Message to second recipient")
' Service Reference (SOAP)
Using client = New SwiftSMS.SendSMSSoapClient
    Dim response = client.SendDistinctBulkMessages(accountKey, reference, numbers, messageBodies)
End Using

' WebClient (REST)
' NOT CURRENTLY AVAILABLE
```

Sends a unique SMS message to each cell numbers provided. Returns the number of messages successfully queued, or an error message on failure.

Parameter|Description|Location
------|------|-----
AccountKey|Your Swift SMS Gateway account key|BODY
Reference|Internal Reference ID|BODY
CellNumbers|Array of cell numbers to deliver SMS messages to|BODY
MessageBodies|Array of messages to deliver to the recipients.  Must have the same number of elements as CellNumbers|BODY

### Returns
`string`

If successful, will return "x messages queued successfully"

If unsuccessful, will return an error message: See [SendMessage](#sendmessage)


<aside class="notice">
 Available only on our API 2 and API 3 Plans.
</aside>

## SendDistinctBulkMessagesViaDedicatedNumber
```csharp
var numbers = new SwiftSMS.ArrayOfString { destinationNumber, destinationNumber };
var messageBodies = new SwiftSMS.ArrayOfString {"Message to recipient 1", "Message to recipient 2"};
// Service Reference / SOAP
using (var client = new SwiftSMS.SendSMSSoapClient())
{
    var response = client.SendDistinctBulkMessagesViaDedicatedNumber(accountKey, messageBody, 
        senderNumber, numbers, messageBodies);
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
    public $AccountKey;
    public $Reference;
    public $SenderNumber;
    public $CellNumbers;
    public $MessageBodies;
}

$client = new SoapClient('http://www.smsgateway.ca/sendsms.asmx?WSDL');
$parameters = new SMSParam;

$parameters -> AccountKey = accountKey;
$parameters -> Reference = reference;
$parameters -> SenderNumber = senderNumber;
$parameters -> CellNumber = (destinationNumber, destinationNumber, ...);
$parameters -> MessageBodies = ("Message to first recipient", "Message to second recipient", ...);

$Result = $client->SendDistinctBulkMessagesViaDedicatedNumber($parameters);
?>
```

```shell
HTTP POST:
# NOT CURRENTLY AVAILABLE #
```

```vb
Dim numbers = New ArrayOfString()
numbers.Add(destinationNumber)
numbers.Add(destinationNumber)
Dim messageBodies = New ArrayOfString()
messageBodies.Add("Message to first recipient")
messageBodies.Add("Message to second recipient")
' Service Reference (SOAP)
Using client = New SwiftSMS.SendSMSSoapClient
    Dim response = client.SendDistinctBulkMessagesViaDedicatedNumber(accountKey, _
        reference, senderNumber, numbers, messageBodies)
End Using

' WebClient (REST)
' NOT CURRENTLY AVAILABLE
```

Sends a unique SMS message to each cell numbers provided via the given dedicated number. Returns the number of messages successfully queued, or an error message on failure.

Parameter|Description|Location
------|------|-----
AccountKey|Your Swift SMS Gateway account key|BODY
Reference|Internal Reference ID|BODY
SenderNumber|Dedicated number to deliver the given messages|BODY
CellNumbers|Array of cell numbers to deliver SMS messages to|BODY
MessageBodies|Array of messages to deliver to the recipients.  Must have the same number of elements as CellNumbers|BODY

### Returns
`string`

If successful, will return "x messages queued successfully"

If unsuccessful, will return an error message: See [SendMessage](#sendmessage)

<aside class="notice">
 Available only on our API 2 and API 3 Plans.
</aside>

## SendTemplatedBulkMessageWithOptions
```csharp
var numbers = new SwiftSMS.ArrayOfString { destinationNumber, destinationNumber };

var options = new SwiftSMS.ArrayOfString { "MsgContentType=Unicode", "SenderID=" + senderNumber };
var templateBody = "Hello <1>, you have an appointment at <2>";
SwiftSMS.ArrayOfString[] args = new ArrayOfString[2];
args[0] = new ArrayOfString {"John", "10:30am"};
args[0] = new ArrayOfString {"Linda", "3:45am"};
// Service Reference / SOAP
using (var client = new SwiftSMS.SendSMSSoapClient())
{
    var response = client.SendTemplatedBulkMessageWithOptions(accountKey,
        templateBody, reference, numbers, args, options);
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
    /** Please contact support@swiftsmsgateway.com for sample **/
?>
```

```shell
HTTP POST:
# NOT CURRENTLY AVAILABLE #
```

```vb
Const templateBody As String = "Hello <1>, you have an appointment at <2>"

Dim numbers = New ArrayOfString()
numbers.AddRange({destinationNumber, destinationNumber})

Dim args(2) As ArrayOfString
args(0) = New ArrayOfString()
args(0).AddRange({"John", "10:30am"})
args(1).AddRange({"Linda", "3:45pm"})

Dim options = New ArrayOfString()
options.Add("MsgContentType=ASCII")
options.Add("SenderId=" & senderNumber)

' Service Reference (SOAP)
Using client = New SwiftSMS.SendSMSSoapClient
    Dim response = client.SendTemplatedBulkMessageWithOptions(accountKey, _
        templateBody, reference, numbers, args, options)
End Using

' WebClient (REST)
' NOT CURRENTLY AVAILABLE
```

Sends an SMS message to all the cell numbers provided. Message can contain parameters arrays in a format (eg. <1>, or <2>). 
Args is an array of arrays with each row having the same number of columns as cell numbers. 
Supported options are the following MsgContentType=Unicode | Ascii.


Returns the number of messages successfully queued, or an error message on failure.

Parameter|Description|Location
------|------|-----
AccountKey|Your Swift SMS Gateway account key|BODY
Reference|Internal Reference ID|BODY
TemplateBody|The template to use when sending the message.  Using <1>, <2>, etc in the template will use values from Args|BODY
CellNumbers|Array of cell numbers to deliver SMS messages to|BODY
Args|Array of ArrayOfString objects with values for the parameters in the template body|BODY
Options|Array of strings with each containing [key]=[value]|BODY


### Options
Parameter|Value|Description|Is Default
-----|-----|-----|-----
MsgContentType| |Send message as ASCII or Unicode| 
 |Unicode|Send Unicode Message (allowing the extended character set|
 |ASCII|Send messages using only ASCII characters|Yes

Parameter|Value|Description|Is Default
-----|-----|-----|-----
SenderId| |Phone number of dedicated long code to send your messages from|

Parameter|Value|Description|Is Default
-----|-----|-----|-----
Reference2| |Secondary Reference field.|
 | |If this is an email address, any replies will be send to this address.  This OVERRIDES account settings

### Returns
`string`

If successful, will return "x messages queued successfully"

If unsuccessful, will return an error message: See [SendMessage](#sendmessage)


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
