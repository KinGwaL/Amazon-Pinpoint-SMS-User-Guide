# Amazon-Pinpoint-SMS-User-Guide

Difference between Amazon Pinpoint Push Notifications and Amazon Simple Notification Service (SNS)

* Amazon SNS is used by developers to send broadcast notifications based on a standard action taken by the end user. Amazon Pinpoint is a targeted notification service, enabling segmentation of users based on a variety of factors including end user device, end user location or recent transactions



* Suggest to create support case for China Short Code (Pinpoint (https://docs.aws.amazon.com/pinpoint/latest/userguide/channels-sms-awssupport-short-code.html) / SNS (https://docs.aws.amazon.com/sns/latest/dg/channels-sms-awssupport-short-code.html)). Explain described below
* We’re open to use Pinpoint / SNS at start depends on the workload from the team, but Pinpoint should be useful for better traffic handling & reduce migration effort. Explain described below
* Review supported countries (https://docs.aws.amazon.com/pinpoint/latest/userguide/channels-sms-countries.html) and check if your targeted country require senderID registration (https://docs.aws.amazon.com/pinpoint/latest/userguide/channels-sms-awssupport-sender-id.html) / need to purchase long code (https://docs.aws.amazon.com/pinpoint/latest/userguide/channels-sms-awssupport-long-code.html) (e.g. Philippines require support ticket to purchase long code / senderid registration), then you need to create support ticket one by one. Or the team can let us know the targeted countries so we can explain the next step



*Whether using SNS or Pinpoint?*

* SNS and Pinpoint has the same SMS delivery infrastructure, so the templated message is appliable for both services
* Moreover Pinpoint support multi-channel (sms, email, voice, notification) & create user segments, launch campaigns (event based, or scheduled) which should be benefit to the team for further implementation
* Implementation is pretty similar using API / SDK


*SMS to China*

* Long Code & SenderID is not natively supported in China because of the regulation policy, so when you enter SenderId / Long Code as a requested parameter, a random phone numbers or header will be shown as expected (https://docs.aws.amazon.com/pinpoint/latest/userguide/channels-sms-countries.html). To make it happen, short code is needed in order to display registered short number for better visibility and performance. It require to submit support ticket and estimated provision time is 3 weeks


*Technical - Throughput Rate (MPS = Message Per Second)*

* Short Code – Up to 100 MPS
* Long Code – 10 MPS (Soft Limit)
* SenderId – 10MPS (Soft Limit)


*Technical - Phone Number Handling Logic*

* If you have multiple numbers associated with your account, and you do not choose an originator though API call / console, AWS will choose an originator based on the following order: short code, 10DLC, long code/toll-free
* It will automatically switch to local originating number based on destination country. For example, if you own a US origination number you can send SMS message to US. If you sending message to HongKong Phone numbers and you do not have any dedicated Long code or Short code. It will fall back to using a shared set of random numbers / senderID to send SMS notifications
* Only include SenderID parameter for the countries that Supports Sender IDs, otherwise the above may not work & routed to shared traffic
* e.g. *NOTICE* senderID is used for HK SMS if 
    * No HK number in your account region
    * X SenderID described during API Call

*Technical - SMS Traffic Performance*

* The traffic speed sent to China should be similar to other countries after template registration, I would suggest the team to have a test though below API setting and submit developer support ticket for further investigation if needed

*Additional Reference*

* SNS Optout (https://docs.aws.amazon.com/sns/latest/dg/sms_manage.html)
* Pinpoint Optout (https://docs.aws.amazon.com/pinpoint/latest/userguide/channels-sms-limitations-opt-out.html)
* Throughput Rate (https://docs.aws.amazon.com/pinpoint/latest/developerguide/quotas.html#quotas-message-templates)
* Dedicated short codes (https://aws.amazon.com/pinpoint/pricing/#Channels)
* Supported Countries (https://docs.aws.amazon.com/pinpoint/latest/userguide/channels-sms-countries.html)

