
## API documentation
[Screenshot](docs/site/img/nibl.jpg)
<br>

#### **Version History**
<table>
<thead>
<tr>
      <th>Date</th>
      <th>Version</th>
      <th>Author</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>28-04-2021</td>
      <td>1.0</td>
      <td>Ronika Sthapit</td>
      <td>Initial documentation</td>
    </tr>
    <tr>
      <td>28-04-2021</td>
      <td>1.1</td>
      <td>Ronika Sthapit</td>
      <td>Added HMAC generation techniques</td>
    </tr>
</tbody>
</tbody>
</table>
<br>
       
#### **About Us**
<p style="text-align:justify">F1Soft International is a company working in the field of software development and IT services. Being a
pioneer in introducing mobile banking and mobile financial services in Nepal, we have been duly
recognized by national and international bodies and awarded with the 2013 FNCCI Service Excellence
Award and the 2014 International Business Awards for our innovative technological solutions.
We have devoted a considerable amount of energy and time on developing mobile and SMS based
applications, internet banking platforms, card management solutions, payment gateways, and various
software systems. E-Sewa, Nepal’s first and leading online payment gateway, is one of our popular and
acclaimed products. Today, the online payment gateway is used by around 300k customers where they
can conveniently pay for a host of services including airlines, movies and bus tickets and also receive and
send money digitally via its web or mobile based platform.
We have a set of skilled engineers and staff who have an in-depth understanding of developing and
deploying software’s tailored to meet the needs of our clients. We lead the market when it comes to
transaction banking products with almost 90% of Nepal’s financial institutions using at least one of our
transaction banking products. Our clients include financial institutions, corporate and media houses,
industrial firms, telecoms, travel agencies and other organizations which bear a name in their own field.
Established in 2004, the company currently employs 210 people with combined expertise and
competence in technology and management. F1Soft is focused on the continuous innovation and
improvement of its transaction banking products.
</p>     
 
#### **Important Parameters:**


<table>
<thead>
<tr>
      <th>PARAMETER NAME</th>
      <th>PARAMETER VALUE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>< algorithm></td>
      <td>HmacSHA512</td>
    </tr>
    <tr>
      <td> < apikey ></td>
      <td>test@test.com.np</td>
    </tr>
        <tr>
      <td>< apisecret ></td>
      <td>dhjkloipyur5fhjusdnbhadsf</td>
    </tr>
        <tr>
      <td>< delimiter ></td>
      <td>“ ” (single space/whitespace)</td>
    </tr>
        <tr>
      <td>< nonce ></td>
      <td>Random alphanumeric value (e.g. uuid)</td>
    </tr>
</tbody>
</tbody>
</table>


<br>

<h4><b>Response Status Code:</b></h4>
<table>
<thead>
<tr>
      <th>SYSTEM CODE</th>
      <th>DESCRIPTION</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Success</td>
    </tr>
      <tr>
      <td>-1</td>
      <td>Failure</td>
    </tr>
    </tbody>
</tbody>
</table>


#### **Signature generation mechanism:**

~~~
The client needs to generate HMAC hash by preparing below raw string form:
Create HMAC token using <algorithm>

* Prepare your signature data based on this format

<delimiter><apiKey><delimiter><nonce><delimiter><requestpayload><delimiter>
(Note: Please observe that delimiter(whitespace) is required in between the data.
Furthermore, it is also placed at the start and end of the string form.)
Here API username will be shared by F1Soft, nonce must be unique for each request (can be
used as unique transaction id or timestamp), request body is payload for API invocation. The
client needs to do HMAC SHA512 hashing to above raw details and perform base64 encoding
to produce binary byte data. The final base64 encoded form is referred as signature hash.

* Encode the signature using Base64
~~~

<br>

## **Send SMS**

This API is used by the third party to send SMS to the mobile users. The API is secured with HMAC
authentication.


<table>
<thead>
<tbody>
<tr>
      <td>URL:</td>
      <td>[https://smsapi.f1soft.com/sms/send][1]
      
      </td>
    </tr>
    </tbody>
  </thead>
  </table>


  URL:         [https://smsapi.f1soft.com/sms/send][1] 

[1]:https://smsapi.f1soft.com/sms/send        

#### **Request method:**
~~~
HTTP METHOD: POST
~~~


#### **Headers:**

<table>
<thead>
<tbody>
<tr>
      <td>CONTENT TYPE</td>
      <td>application/json</td>
    </tr>
    <tr>
      <td>AUTHORIZATION</td>
      <td>< algorithm > < apikey >:< nonce >:< signature ></td>
    </tr>
    <tr>
      <td>AUTHORIZATION-TYPE</td>
      <td>HMAC</td>
    </tr>
    <t/body>
  </thead>
  </table>
<br>



**Authorization example:**
~~~
HmacSHA512 test@test.com.np:29206090-9a88-4fd7-9285-bbcb2510d204:
SHAd50a54bc92ae8c657adgf272c5a7aaf41d1978e635z7e9oba64c2504baa22d1c9da4ac72b22pfc2080402b6ca5
37ad63bfe6703becac8213a59cebfd85f30f58
~~~

#### **Request body parameters:**
<table>
  <thead>
    <tr>
      <th>PARAMETER NAME</th>
      <th>Type</th>
      <th>MANDATORY</th>
      <th>REMARKS</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>mobileNumber</td>
      <td>String</td>
      <td>Yes</td>
      <td>Valid telco subscriber mobile no.</td>
    </tr>
    <tr>
      <td>message</td>
      <td>String</td>
      <td>No</td>
      <td>Message to send
[ Unicode message also supported]</td>
    </tr>
     <tr>
      <td>Password</td>
      <td>String</td>
      <td>yes</td>
      <td>otp/alert</td>
    </tr>
     <tr>
      <td>RequestId</td>
      <td>String</td>
      <td>yes</td>
      <td>Unique id for every sms transaction</td>
    </tr>
  </tbody>
</table>

#### **Sample request body:**
~~~
{"mobileNumber":"98xxxxxxxx",
"message":"Message to send",
“type":"otp",
"uniqueId":"F1-1001"}
~~~
```
*NOTE: REQUEST BODY SHOULD NOT HAVE ANY SPACE IN IT .
```
<br>
### EXAMPLE:


#### **1. Response body parameters:**

<table>
  <thead>
    <tr>
      <th>PARAMETER NAME</th>
      <th>Type</th>
      <th>REMARKS</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>status</td>
      <td>boolean</td>
      <td>Success/Failure flag</td>
    </tr>
    <tr>
      <td>message</td>
      <td>String</td>
      <td>Api result description</td>
    </tr>
     <tr>
      <td>code</td>
      <td>Object</td>
      <td>System success/failure code</td>
    </tr>
     <tr>
      <td>data</td>
      <td>String</td>
      <td>Response actual data</td>
    </tr>
    <tr>
      <td>httpStatus</td>
      <td>String</td>
      <td>Api status code</td>
    </tr>
  </tbody>
</table>

#### **2. Data**

<table>
  <thead>
    <tr>
      <th>PARAMETER NAME</th>
      <th>Type</th>
      <th>REMARKS</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>mobileNumber</td>
      <td>string</td>
      <td>SMS received mobile number</td>
    </tr>
    <tr>
      <td>msgId</td>
      <td>string</td>
      <td>SMS sent unique id</td>
    </tr>
 
  </tbody>
</table>


#### **Responses:** 
<b>Success response:</b>

~~~

{
"status": true,
"message": "SMS delivered successfully",
"code": "0",
"data": {
"mobileNumber": "98xxxxxxxx",
"msgId": "MN-1553144161875"
},
"httpStatus": 200
}
~~~

**Authentication failed:**
~~~
{
"timestamp": 1522047604846,
"status": 403,
"error": "Forbidden",
"message": "Invalid authorization data",
"path": "/sms/send"
}
~~~


**SMPP Error:**

~~~
{
"code": "-1",
"developerMessage": "Failed to submit to the SMSC.",
"link": "string",
"message": "SMS delivery failed",
"status": false,
"httpStatus": 406
}
~~~
**Delivery failed:**

~~~
{
"code": "-1",
"developerMessage": "Failed to submit to the SMSC.",
"link": "string",
"message": "SMS delivery failed",
"status": false,
"httpStatus": 406
}
~~~
<br>

## Receive SMS callback:

SMS Aggregator system receives SMS, sent to client’s short-codes. This system triggers callback
notification to client’s system, if this setting is configured. The client’s system needs to develop callback
API based on the specifications below:

#### **Request method:**
~~~
HTTP METHOD: POST
~~~

#### **Headers:**
<table>
  <tbody>
    <tr>
      <td>CONTENT TYPE</td>
      <td>application/json</td>
    </tr>
    <tr>
      <td>AUTHORIZATION</td>
      <td>< algorithm > < apikey >:< nonce >:< signature ></td>
    </tr>
      <tr>
      <td>AUTHORIZATION-TYPE</td>
      <td>HMAC</td>
    </tr>
 
  </tbody>
</table>

**Authorization example:**
~~~
HmacSHA512 test@test.com.np:29206090-9a88-4fd7-9285-bbcb2510d204:
SHAd50a54bc92ae8c657adgf272c5a7aaf41d1978e635z7e9oba64c2504baa22d1c9da4ac72b22pfc2080402b6ca5
37ad63bfe6703becac8213a59cebfd85f30f58
~~~


**Note:** We will send HMAC in Authorization for this API.

#### **Request body parameter:**

<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Type</th>
      <th>Mandatory</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>boid</td>
      <td>string</td>
      <td>Yes</td>
      <td>Boid Provided by Bank</td>
    </tr>
    <tr>
      <td>username</td>
      <td>String</td>
      <td>Yes</td>
      <td>Client username</td>
    </tr>
     <tr>
      <td>Password</td>
      <td>String</td>
      <td>yes</td>
      <td>Client Password</td>
    </tr>
     <tr>
      <td>RequestId</td>
      <td>String</td>
      <td>yes</td>
      <td>Unique Request Id</td>
    </tr>
  </tbody>
</table>

#### **Response Parameter**

<table>
  <thead>
    <tr>
      <th>PARAMETER NAME</th>
      <th>DESCRIPTION</th>
      <th>DATA TYPE</th>
      <th>MANDATORY</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>message</td>
      <td>SMS text received from customer as SMS message</td>
      <td>String</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>resultDescription</td>
       <td>Mobile number of SMS Sender</td>
      <td>String</td>
      <td>Yes</td>
    </tr> 
      <tr>
      <td>boid</td>
       <td>SMS received date</td>
      <td>String</td>
      <td>Yes</td>
    </tr>
     <tr>
      <td>name</td>
       <td>Trace ID to uniquely identify SMS received
transaction id</td>
     <td>String</td>
      <td>Yes</td>
    </tr>
    <td>totalAmount</td>
       <td>SMS shortcode where user sends SMS from app</td>
       <td>String</td>
      <td>Yes</td>
  </tbody>
</table>


#### **Sample Request body:**
~~~
{"message":"BALANCE","mobileNumber":"98xxxxxxxx","receivedDate":"2021-04-28 16:52:20","traceid":"CNP-
1001","shortCode":"XXXX"}
~~~
~~~
*NOTE:  REQUEST BODY SHOULD NOT HAVE ANY SPACE IN IT .
~~~
**Example:**
~~~
{
“message”: “BALANCE”,
“mobileNumber”: “98xxxxxxxx”,
“receivedDate”: “2021-04-28 16:52:20”,
“traceid”: “CNP-1001”
"shortCode": "XXXX"
}
~~~
#### **Response Parameter:**
<table>
  <thead>
    <tr>
      <th>PARAMETER NAME</th>
      <th>Type</th>
      <th>REMARKS</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>code</td>
      <td>string</td>
      <td>Response status of the response</td>
    </tr>
    <tr>
      <td>message</td>
      <td>string</td>
      <td>Description of the response</td>
    </tr>
 
  </tbody>
</table>

#### **Response sample:**
~~~
{
“code”: “0”,
“message”: “Notified successfully.”
}
~~~

#### **Code Samples:
~~~
<?php
$apiKey = '<apikey shared to client>';
$apiSecret = '<apisecret shared to client>';
$nonce = '1234567';
$requestData = ['mobileNumber'=> '98xxxxxxxx', 'message'=> 'Message to send', 'type'=>'otp', 'uniqueId'=>'F1-
1001'];
$url = 'https://smsapi.f1soft.com/sms/send';
$delimiter = ' ';
$digestString = $delimiter
. $apiKey. $delimiter
. $nonce. $delimiter
. json_encode($requestData) . $delimiter;
$digest = hash_hmac('SHA512', $digestString, $apiSecret, true);
$headers = ['Authorization: HmacSHA512 '. $apiKey . ':' . $nonce . ':' . base64_encode($digest), 'Content-Type:
application/json'];
$ch = curl_init();
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($requestData));
$curlOptions = [
CURLOPT_URL => $url,
CURLOPT_RETURNTRANSFER => true,
CURLOPT_FOLLOWLOCATION => true,
CURLOPT_MAXREDIRS => 10,
CURLOPT_HTTPHEADER => $headers,
CURLOPT_HEADER => false,
];
curl_setopt_array($ch, $curlOptions);
$res = curl_exec($ch);
echo $res;
~~~

**Java**
~~~
public class Main {
public static void main(String[] args)
throws
NoSuchAlgorithmException,
InvalidKeyException {
String apiKey = "<apikey shared to client>”;
String apiSecret = "<apiSecret shared to client>";
String delimiter = " ";
String nonce = "29206090-9a88-4fd7-9285-bbcb2510d204";
String requestPayload = "{"mobileNumber\":\"98xxxxxxxx\",\"message\":\"Message to
send\",\"type\":\"otp\",\"uniqueId\":\"F1-1001\"}";
String signatureBase = delimiter + apiKey + delimiter + nonce + requestPayload + delimiter;
Mac hasher = Mac.getInstance("HmacSHA512");
hasher.init(new SecretKeySpec(apiSecret.getBytes(), "HmacSHA512"));
byte[] hash = hasher.doFinal(signatureBase.getBytes());
String signature = DatatypeConverter.printBase64Binary(hash);
String header = "HmacSHA512" + " " + apiKey + ":" + nonce + ":" + signature;
System.out.println(header);
}
}
~~~

**.NET**
~~~
using System;
using System.Security.Cryptography;
using System.Text;
public class Program{
public static void Main(){
String apiKey = "<apikey shared to client>”;";
String apiSecret = "<apiSecret shared to client>";
String delimiter = " ";
String nonce = "29206090-9a88-4fd7-9285-bbcb2510d204";
String requestPayload = "{"mobileNumber\":\"98xxxxxxxx\",\"message\":\"Message to
send\",\"type\":\"otp\",\"uniqueId\":\"F1-1001\"}";
String signatureBase = delimiter+apiKey+delimiter+nonce+requestPayload+delimiter;
String signature = HMAC_SHA512(apiSecret, signatureBase);
String header = "HmacSHA512"+ " "+ apiKey+":"+nonce+":"+signature;
Console.WriteLine(header);
}
public static string HMAC_SHA512(string keyString, string message){
byte[] key = Encoding.ASCII.GetBytes(keyString);
HMACSHA512 sha = new HMACSHA512(key);
byte[] input = Encoding.ASCII.GetBytes(message);
return BitConverter.ToString(sha.ComputeHash(input)).Replace("-", "").ToLower();
}
}
~~~