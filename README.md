## aerogear-unified-push-php-client

A PHP API for sending Push Notifications with the [AeroGear UnifiedPush Sender](https://github.com/aerogear/aerogear-unified-push-server).

### Usage
The main class, SenderClient, is what handles the message formatting and sending to the server. It also can return two responses from the server: the HTTP response code (as ```getResponseCode()```), and the body of the HTTP response (as ```getResponseText()```). This data can determine whether a message send was successful or not.
SenderClient supports all parameters that can be sent with a message payload, and will encode them as necessary to be sent. It also handles server authentication with ```pushApplicationId``` and ```masterSecret```.

The class can be used with a database backend, being fed data from a database, form, or other request. For demonstration purposes, there is an included webapp, which shows off a form which can handle multiple messages and all other current Aerogear features.

### Webapp
There is a mini-webapp included within /webapp/. This demonstrates how you can use ```SenderClient``` to interface with a web form for sending a message.

```index.php``` is the actual HTML for the user, and allows a Selected or Broadcast send to be chosen. If selected send is used, then more options (i.e. variants, aliases, etc) are available for submission. If broadcast is chosen, only the required options are shown. 
For values that have key-value pairs, such as ```message``` and ```simplePush```, the form allows for dymanic creation of more key-value pairs as needed.

```toArray.php``` holds one function to help convert ```<textarea>``` elements into PHP-parseable arrays. These are eventually encoded and send to SenderClient.


```processForm.php``` is the target of the form in ```index```. This script takes the HTTP POST data, parses it into a usable form for SenderClient, and sends it to SenderClient. The most complex part of this involves ```toArray``` to change the ```<textarea>``` lines into PHP arrays. It also adds they key-value pairs of message and simplePush to the SenderClient.
Upon completion, the script outputs the HTTP response code and the HTTP response text (ideally `Job Submitted`)
