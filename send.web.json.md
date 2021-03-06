title: Pepipost API Docs v1.0
---

## Send Email - JSON (<a href="https://github.com/Pepipost/docs/edit/master/send.web.json.md" target="_blank">  Edit </a>)

JSON/Email send – this API can be use to send emails.

## Basic example

```
Host: https://api.pepipost.com
```

```
Content-Type: application/json
```

```
POST /api/web.send.json HTTP/1.1
{
    "api_key": "string",
    "email_details": {
        "fromname": "yourfromname",
        "subject": "this is test email subject",
        "from": "from@example.com",
        "content": "<p> hi, this is a test email sent via Pepipost JSON API.</p>"
    },
    "recipients": [
        "recipient@example.com"
    ]
}

```
**<a href="https://docs.pepipost.com/console/#!/Email/post_api_web_send_json" target="_blank"> Click here </a> to try the above example with our online API console**


### Example Response 

```
HTTP/1.1 200 OK
{"message":"SUCCESS","errorcode": "0" ,"errormessage":""}
```

## Example with attributes

### Example of sending content personalized email

In order to send personalized content email using Pepipost API, you need to first provide the attribute in your API call along with the place-holders used inside of your HTML content. Like below given example:

**Your API Call**
```
POST /api/web.send.json HTTP/1.1
{
    "api_key":"yourapikey",
     "email_details":{
      "fromname":"sender name",
      "subject":"test email subject",
      "from":"from@example.com",
      "content":"<p>Hi [%NAME%], your current balance as on today is [%ACCOUNT_BAL%].</p>"
      },
     "recipients":["mike@example.com","joe@example.com"],
      "attributes":{
      "NAME":["Mike","Joe"],
      "ACCOUNT_BAL":["100","200"]
      }
}
```
**<a href="https://docs.pepipost.com/console/#!/Email/post_api_web_send_json" target="_blank"> Click here </a> to try the above example with our online API console**

**Mail received by Mike **

```
<p>Hi Mike, your current balance as on today is 100.</p>
```

**Mail received by Joe **

```
<p>Hi Joe, your current balance as on today is 200.</p>
```


## Advance example

```
Host: https://api.pepipost.com
```

```
Content-Type: application/json
```

```
POST /api/web.send.json HTTP/1.1
{
    "api_key":"yourapikey",
    "email_details":{
          "fromname":"sender name",
          "subject":"test email subject",
          "from":"from@example.com",
          "replytoid": "replytoid@example.com",
          "content":"<p>Hi [%NAME%], This is a test email sent using Pepipost JSON/Email API</p>"
      },
     "tags": "AccountDeactivation, Verification", 
     "X-APIHEADER": ["ID3","ID2"],
     "settings":{
          "footer":"1",
          "clicktrack":"1",
          "opentrack":"1",
          "unsubscribe":"1",
          "bcc":"sac@test.com",
          "attachmentid":"1,3,4",
          "template":"101",
     },
     "recipients":["recipient1@example.com","recipient2@example.com"],
     "attributes":{
          "NAME":["NameOfFirstRecipient","NameOfSecondRecipient"],
          "AGE":["20","30"]
      },
      "files": {
          "attachment_example1.txt": "VGhpcyBpcyB0aGUgY29udGVudCBvZiBhIHRlc3QgZmlsZS4K",
          "attachment_example2.txt": "VGhpcyBpcyB0aGUgY29udGVudCBvZiBhIHRlc3QgZmlsZSAyLgo="
      }
}
```

**<a href="https://docs.pepipost.com/console/#!/Email/post_api_web_send_json" target="_blank"> Click here </a> to try the above example with our online API console**

** NOTES **

* The fields "NAME" and "AGE" are user defined. One can use any alphanumeric attribute name.
* The fields "attachment_example1.txt" and "attachment_example2.txt" are user defined. One can use any alphanumeric filename.
* The value of field "files" needs to be encoded in base64 encoding format. You can attach various types of files including pdf, png, etc in the same as shown above. However, the above example uses txt file example becauase the base64 for other file types (like pdf) will be large and make the example unreadable.

### Example Response

```
HTTP/1.1 200 OK
{"message":"SUCCESS","errorcode": "0" ,"errormessage":""}
```

### Parameters
Name | Required | In | Type | Description
--- | --- | --- | --- | ---
api_key |Yes| query | string | Your API Key
data| Yes | body | [Data](#Data) | Data in JSON format

### Fields
Name | Type | Required | Description
--- | --- | --- | ---
api_key | string | Yes | Your secret API Key
email_details | struct | Yes | <table>    <thead>    <tr>                <th>Name</th>        <th>Type</th>                <th>Required</th>        <th>description</th>            </tr>    </thead>    <tbody>    <tr>                <td>fromname</td>        <td>string</td>                <td>No</td>                <td>Email Sender name</td>        </tr>    <tr>                <td>subject</td>        <td>string</td>                <td>Yes</td>                <td>subject of the email</td>    </tr>    <tr>                <td>from</td>        <td>string</td>             <td>Yes</td>                   <td>sender email address.</td>        </tr>    <tr>                <td>replytoid</td>        <td>string</td>             <td>No</td>                   <td>email address where recipients reply will be received.</td>        </tr>    <tr>                <td>tags</td>        <td>string</td>                <td>No</td>                <td>This can be use by user to tag/label their emails, in order to categorize for reports and other purposes. Use comma to separate multiple values. </td>        </tr>    <tr>                <td>content</td>        <td>string</td>                <td>Yes</td>                <td></td>        </tr>    </tbody></table>
X-APIHEADER | array[string] | No | This is the user defined ids in order to uniquely identify each emails.
settings | struct | No | <table>    <thead>    <tr>                <th>Name</th>        <th>Type</th>                <th>Required</th>        <th>description</th>            </tr>    </thead>    <tbody>    <tr>                <td>footer</td>        <td>boolean</td>                <td>No</td>                <td>To turn on/off the footer addition in the email. User can define footer using dashboard after login.</td>        </tr>    <tr>                <td>clicktrack</td>        <td>boolean</td>           <td>No</td>                     <td>To turn on/off the click tracking of your recipients.</td>        </tr>    <tr>                <td>opentrack</td>        <td>boolean</td>           <td>No</td>                     <td>To turn on/off the open tracking of your recipients.</td>        </tr>    <tr>                <td>unsubscribe</td>        <td>boolean</td>           <td>No</td>                     <td>To turn on/off the unsubscribe link addition in the email.</td>        </tr>    <tr>                <td>bcc</td>        <td>string</td>            <td>No</td>                    <td>Blind Cardbon Copy - a copy of the email will be sent to the email address mentioned here.</td>        </tr>    <tr>                <td>attachmentid</td>        <td>string</td>            <td>No</td>                    <td>To add attachment to the email. User can add attachment using dashboard after login.</td>        </tr>    <tr>                <td>template</td>        <td>integer</td>                <td>No</td>                <td>Template ID of the HTML template which user has created using dashboard, after login.</td>    </tr>    </tbody></table>
recipients | array[string] | Yes | Array of recipients email addresses, to whom the mail will be sent.
attributes | struct | No | <table>    <thead>    <tr>                <th>Name</th>        <th>Type</th>                <th>Required</th>                <th>description</th>        </tr>    </thead>    <tbody>    <tr>                <td>NAME</td>        <td>string</td>                <td>No</td>                <td>The key "NAME" is user defined and not fixed. You can put any valid alphanumeric name eg: FIRST_NAME. This needs to be defined per recipients.</td>        </tr>    <tr>                <td>AGE</td>        <td>string</td>                <td>No</td>                <td>The key "AGE" is user defined and not fixed. You can put any valid alphanumeric name eg: FIRST_NAME. This needs to be defined per recipients.</td>        </tr>    </tbody></table>
files | struct | No | <table>    <thead>    <tr>                <th>Name</th>        <th>Type</th>                <th>Required</th>            <th>description</th>        </tr>    </thead>    <tbody>    <tr>                <td>your_attachment1.txt</td>        <td>string</td>                <td>No</td>                <td>The key "your_attachment1.txt" is user defined and not fixed. You can put any valid alphanumeric filename for attachment. This needs NOT to be defined per recipients.</td>        </tr>    <tr>                <td>your_attachment2.txt</td>        <td>string</td>            <td>No</td>                    <td>The key "your_attachment2.txt" is user defined and not fixed. You can put any valid alphanumeric filename for attachment. This needs NOT to be defined per recipients.</td>        </tr>    </tbody></table>

	
### Responses format
Name | Description
--- | --- 
message | Its can have only 2 values - "SUCCESS" or "ERROR"
errorcode | Pepipost API error code. Its value will be - 0 (zero) in case of success. In case of error it will be non-zero integer value.
errormessage | Error specific error messages. 

## Integrating with PHP

Its recommended to use Peipost SDK for PHP in order to integrate Pepipost services with applications written in PHP. You can get Pepipost SDK for PHP by <a href="https://github.com/pepipost/pepipost-sdk-php" target="_blank">  clicking here </a> .

### Basic Example

```php
<?php

require_once __DIR__.'/vendor/autoload.php';

use PepipostAPIV10Lib\Controllers\Email;

$email = new Email();

$data = array(
    'api_key'        =>  'yoursecretapikey',
    'recipients'    =>  array('recipient@example.com'),
    'email_details' => array(
        'content'       =>  'this mail is sent via PHP SDK',
        'from'          =>  'from@example.com',
        'subject'       =>  'this mail is sent via PHP SDK',
        'fromname'      =>  'SDK Sender Name ',    
    )
);

try {
    $response = $email->sendJson( $data );
    if(empty($response->errorcode)){
        print "Email sent successfully.\n";
    }
    else {
        print "Email sent Failed.\n";
        print "errormessage(" . $response->errormessage . ") \n";
        print "errorcode(" . $response->errorcode . ").\n";
    }
}
catch(Exception $e){
    print 'Call failed due to unhandled exception/error('. $e->getMessage().')'."\n";
}
```

### Advance Example

```php
<?php

require_once __DIR__.'/vendor/autoload.php';

use PepipostAPIV10Lib\Controllers\Email;

$email = new Email();

$data = array(
    'api_key'   =>  'yoursecretkey',
    'recipients'    =>  array('recipient1@example.com','recipient2@example.com'),
    'email_details' => array(
        'from'          =>  'from@example.com',
        'subject'       =>  'Hi [% NAME %], here is your account balance.',
        'content'       =>  '<p>Hi [%NAME%],</p><p>Your account balance is [% ACCOUNT_BAL %].</p>',
        'fromname'      =>  'SDK Sender Name ',
        'replytoid'     =>  'replyto@example.com',
    ),
    'tags'          	=>  'AccountDeactivation, Verification',
    'X-APIHEADER' => array('UserID1','UserID2'),
    'settings' => array(
        'footer'        =>  true,
        'clicktrack'    =>  true,
        'opentrack'     =>  true,
        'unsubscribe'   =>  true,
        'bcc'           =>  'bcc@example.com',
    ),
    'attributes' => array(
        'NAME'          => array('NameOfRecipient1','NameOfRecipient2'),
        'ACCOUNT_BAL'   => array('100','200'),
    ),    
    'files' => array(
        'example_attachment1.txt' => base64_encode(trim(file_get_contents('/path/to/file.txt'))),
        'example_attachment2.pdf' => base64_encode(trim(file_get_contents('/path/to/file.pdf'))),
    ),  
);

try {
    $response = $email->sendJson( $data );
    //var_dump($response);
    if(empty($response->errorcode)){
        print "Email sent successfully.\n";
    }
    else {
        print "Email sent Failed.\n";
        print "errormessage(" . $response->errormessage . ") \n";
        print "errorcode(" . $response->errorcode . ").\n";
    }
}
catch(Exception $e){
    print 'Call failed due to unhandled exception/error('. $e->getMessage().')'."\n";
}
```


## Integrating with Python

Its recommended to use Peipost SDK for Python in order to integrate Pepipost services with applications written in Python. You can get Pepipost SDK for Python by <a href="https://github.com/pepipost/pepipost-sdk-python" target="_blank">  clicking here </a> .

### Basic Example

```python
from PepipostAPIV10Lib.Controllers.Email import *
import json

controller = Email()

#data = ()
data = { 
    'api_key' : 'yoursecretapikey',
    'recipients' : ['recipient1@example.com','recipient2@example.com'],
    'email_details' : { 
        'fromname' : 'sender name',
        'subject' : 'test email subject sent using Pepipost SDK - Python',
        'from' : 'from@example.com',
        'content' : '<p>This is a test email sent using Pepipost JSON/Email Python SDK</p>'
    }   
}

response = controller.send(data)

print response
```

## Integrating with Ruby

Its recommended to use Peipost SDK for Ruby in order to integrate Pepipost services with applications written in Ruby. You can get Pepipost SDK for Ruby by <a href="https://github.com/pepipost/pepipost-sdk-ruby" target="_blank">  clicking here </a> .

### Basic Example

```ruby
require 'pepipost_apiv_10'

data = {
    "api_key"=>"yoursecretapikey",
    "recipients"=> ["recipient1@example.com","recipient2@example.com"],
    "email_details" => {
        "fromname" => "sender name",
        "subject" => "This is a test email sent usig Pepipost SDK for Ruby",
        "from" => "from@example.com",
        "content" => "<p>This is a test email sent using Pepipost SDK for Ruby</p>",
    }
}


email = PepipostApiv10::Email.new
response = email.send data

print response

```

## Integrating with NodeJS

Its recommended to use Peipost SDK for NodeJS in order to integrate Pepipost services with applications written in NodeJS. 

You can install it using npm "npm install pepipost-sdk-nodejs". 

You can get its source code by <a href="https://github.com/pepipost/pepipost-sdk-nodejs" target="_blank">  clicking here </a> .

### Basic Example

```js
var PepipostSDK = require('pepipost-sdk-nodejs');

var Email = PepipostSDK.EmailController;

var data = {
    "api_key": "yoursecretapikey",
    "email_details": {
        "fromname": "yourfromname",
        "subject": "this is test email subject",
        "from": "from@example.com",
        "content": "<p> hi, this is a test email sent via Pepipost JSON API.</p>"
    },
    "recipients": [
        "recipient@example.com"
    ]
};

Email.send(data,callback_mail_sent);

function callback_mail_sent(err_msg,parsed,context){
    if(parsed.errorcode==0){
        console.log("mail sent successfully.\n");
    }
    else{
        console.log("Email sent Failed.\n");
        console.log("errormessage("+parsed.errormessage+")\n");
        console.log("errorcode("+parsed.errorcode+")\n");
    }    
}
```

## Integrating with NodeJS - Nodemailer

Nodemailer is a famous NodeJS library to send email. 

You can know more about Nodemailer by <a href="https://github.com/nodemailer/nodemailer" target="_blank">  clicking here </a> .

Please follow the below steps, in order to integerate Pepipost with Nodemailer:

You can install it using npm "npm install nodemailer". 


### Basic Example for Nodemailer version above v0.7.1

```js
var nodemailer = require('nodemailer');
//below var smtpTransport not required for Nodemailer version equal or below v0.7.1
var smtpTransport = require("nodemailer-smtp-transport");

// Create a SMTP transport object
var transport = nodemailer.createTransport(smtpTransport( {
        host: "smtp.pepipost.com",
        port: 2525,
        auth: {
            user: "yoursmtpusername",
            pass: "yoursmtppassword"
        }
    }));
/*
//Use this code for Nodemailer version equal or below v0.7.1
var transport = nodemailer.createTransport("SMTP", {
        //service: 'Pepipost',
        host: "smtp.pepipost.com",
        port: 2525,
        auth: {
            user: "yoursmtpusername",
            pass: "yoursmtppassword"
        }
    });
*/
console.log('SMTP Configured');

// Message object
var message = { 

    // sender info
    from: 'Sender Name <sender@example.com>',

    // Comma separated list of recipients
    to: '"Receiver Name" <recipient@example.com>',

    // Subject of the message
    subject: 'Nodemailer is unicode friendly ✔', 

    // plaintext body
    text: 'Test mail sent using Nodemailer with Pepipost',

    // HTML body
    html:'<p><b>Hello</b> Test mail sent using Nodemailer with Pepipost</p>'+
         '<p>Thank you.</p>'

    //For adding X-APIHEADER, uncomment the blow lines
    /**
    ,headers: {
        'X-APIHEADER':'userid1'
    }   
    */
};

console.log('Sending Mail');
transport.sendMail(message, function(error){
  if(error){
      console.log('Error occured');
      console.log(error.message);
      return;
  }
  console.log('Message sent successfully!');

  // if you don't want to use this transport object anymore, uncomment following line
  //transport.close(); // close the connection pool
});

```

## Integrating with Java

Its recommended to use Peipost SDK for Java in order to integrate Pepipost services with applications written in Java. You can get Pepipost SDK for Java by <a href="https://github.com/pepipost/pepipost-sdk-java" target="_blank">  clicking here </a> .

### Basic Example

```java
import io.swagger.client.*;
import io.swagger.client.auth.*;
import io.swagger.client.model.*;
import io.swagger.client.api.EmailApi;

import java.io.File;
import java.util.*;

public class Example {

    public static void main(String[] args) {
        //Getting the SDK object
        EmailApi pepipostSDK = new EmailApi();

        //Getting the data object
        Emailv1 data = new Emailv1(); // Emailv1 | Data in JSON format

        //setting the apikey
        data.setApiKey("yoursecretapikey");

        //setting the data
        EmailDetails email_details = new EmailDetails(); // Emailv1 | Data in JSON format
        email_details.setFromname("yourfromname");
        email_details.setFrom("from@example.com");
        email_details.subject("This is the test email subject sent via Pepipost Java SDK");
        email_details.setContent("<p> hi, this is a test email sent via Pepipost Java SDK using its JSON API.</p>");
        data.setEmailDetails(email_details);

        //adding recipients
        List<String> recipients = new ArrayList<String>();
        recipients.add("to@example.com");
        data.setRecipients(recipients);

        //making the call
        try {
            pepipostSDK.apiWebSendJsonPost(data);
            System.out.println("Email sent successfully.");
        } catch (ApiException e) {
            System.out.println("Exception occurred while calling Pepipost API");
            System.out.println("Errormessage("+e.getMessage()+")");
            System.out.println("Errorcode("+e.getCode()+")");
            //e.printStackTrace();
        }
    }
}

```

## Integrating with Perl

Its recommended to use Peipost SDK for Perl in order to integrate Pepipost services with applications written in Perl. You can get Pepipost SDK for Perl by <a href="https://github.com/pepipost/pepipost-sdk-perl" target="_blank">  clicking here </a> .

### Basic Example

```perl
#!/usr/bin/perl
use lib 'lib';
use strict;
use warnings;
# load the API package
use WWW::Pepipost::EmailApi;

# load the models
use WWW::Pepipost::Object::Attributes;
use WWW::Pepipost::Object::EmailDetails;
use WWW::Pepipost::Object::Emailv1;
use WWW::Pepipost::Object::Files;
use WWW::Pepipost::Object::Settings;

# for displaying the API response data
use Data::Dumper;

my $email = WWW::Pepipost::EmailApi->new();
my $data = WWW::Pepipost::Object::Emailv1->new(); # Emailv1 | Data in JSON format

$data->{'api_key'} = 'yoursecretkey';
$data->{'recipients'} = ['recipient@example.com'];
$data->{'email_details'}{'subject'} = 'This is a test email subject sent using Pepipost SDK for Perl';
$data->{'email_details'}{'from'} = 'from@example.com';
$data->{'email_details'}{'content'} = 'This is a test email content sent using Pepipost SDK for Perl';


eval {
    my $response = $email->send(data => $data);
    print "response($response)\n";
};
if ($@) {
    warn "Exception when calling EmailApi->send: $@\n";
}

```

## Integrating with C# #

Its recommended to use Peipost SDK for C# in order to integrate Pepipost services with applications written in C#. You can get Pepipost SDK for C# by <a href="https://github.com/pepipost/pepipost-sdk-csharp" target="_blank">  clicking here </a> .

### Basic Example

```java
using System;
using IO.Swagger.Api;
using IO.Swagger.Client;
using IO.Swagger.Model;
using Newtonsoft.Json;

namespace youconsoleapp
{
    class MainClass
    {
        public static void Main (string[] args)
        {
            //Prepare the data
            Emailv1 data = new Emailv1 ();
            data.ApiKey = "yoursecretapikey";


            //email_details Model
            EmailDetails email_details = new EmailDetails ();
            email_details.Fromname = "sender name";
            email_details.From = "from@example.com";
            email_details.Subject = "Test email sent using Pepiopst Csharp SDK";
            email_details.Content = "<p>This email is sent using Pepipost CSharp SDK</p>";

            System.Collections.Generic.List<string> recipients = new System.Collections.Generic.List<string> {"recipient@example.com"};

            //Combine all
            data.Recipients = recipients;
            data.EmailDetails = email_details;

            //Call the API method
            EmailApi email = new EmailApi ();

            //For debug print outgoing json
            //String data_json = JsonConvert.SerializeObject (data);
            //System.Console.WriteLine ("Data JSON "+ data_json);

            var response = email.CreateApiWebSendJson (data);
            System.Console.WriteLine ("response"+response.ToString());
        }
    }
}

```
