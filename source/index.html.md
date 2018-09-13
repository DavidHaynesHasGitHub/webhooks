---
title: Zaui Web-Hook and Remote Target API

language_tabs: # must be one of https://git.io/vQNg
  - json


toc_footers:
  - <a href='https://api.zaui.io/signup'>Sign Up for a Developer Key</a>
  - <a href='https://davidhayneshasgithub.github.io/ZauiWebApi/'>See our Web API Documentation</a>
  - <a href='https://davidhayneshasgithub.github.io/ZauiIOAPI'>See our IO API Documentation</a>

search: true
---

# Zaui Web-Hook and Remote Target API

## Preface

The typical user of this manual is a power user of Zaui Software who wishes to have real-time access to data as it is created, edited or removed from the system.

# Web-Hooks Overview

## What is a Web-Hook?

Web-hooks are an easy way to push notifications from Zaui to any remote system you wish. Web-hooks are triggered from within workflows in Zaui, to deliver data to a remote system. A web-hook is like and inverted API endpoint. Instead of making a call to our API, you define a callback URL (endpoint) to which we will HTTP POST information when events occur in Zaui. Your callback URL can then execute code based on the POST data.

You can think of it as defining an API endpoint for your application that will receive output from Zaui, when events occur within Zaui.

Examples of triggers could be when a booking is created or edited or when a customer record is create or amended. These events would then deliver the changed data to your endpoint, where your code could do something with that such as update your external CRM system.

# Web-Hook Setup

## Initial Setup

1. Log into your Zaui system
2. On the menu system go to Settings->Manage Notifications->Web-Hooks (Remote Targets)
3. Create your new web-hook, for example "On Booking Creation". For the "Remote Target URL", put in the Bin URL, that you obtain from the RequestBin setup.

## Trigger Event in Zaui

1. Trigger the event in Zaui (such as a new booking).
2. Refresh the RequestBin browser window, and your request data payload from Zaui will appear

# Debugging Web-Hooks

If you need to see what kind of response you’re going to get from our web-hooks, or you need to tunnel directly to your development environment, there is a selection of tools out there to help you. Here is a short list of some great tools on the market, but we will only go into detail with RequestBin.

## Tools

1. RequestBin – simple tool for insight into web-hook data payloads in real-time. Its Free!
2. <a href="https://ngrok.com/" target="_blank"_>Ngrok</a> – tool for creating a local tunnel into your machine, it makes testing web-hooks locally very easy.
3. <a href="https://www.runscope.com/" target="_blank"_>Runscope</a> – a tool for debugging API’s. It acts a proxy, collecting all data sent to it and passes it on to another point.

## Debugging Zaui Web-Hooks Using RequestBin
### RequestBin Setup

1. In your browser, go to <a href="https://requestb.in" target="_blank"_>RequestBin</a>
2. Click on "Create a RequestBin"
3. You will be given a "Bin URL". This URL will be used as the configured endpoint in setting up the endpoint URL in Zaui.

  **NOTE** _do not close this browser window, RequestBin requires this session to capture the inbound data requests._

# Caveats and Notes to Web-Hooks
1. Your servers need to be robust enough to handle a large number of requests from Zaui web-hooks, especially if you have configured many web-hooks that cascade from event to event.

2. Sending data from Zaui to your endpoint can be a blocking call in our system, and can result in up to a 2 sec delay. Our systems will abandon the call after 2 seconds, and will no wait for return data coming back from your servers. If your using multiple web-hooks, for example, to be trigger at the time of making a new booking, the time required to process the booking will be delayed up to 2 secs for each web-hook.

# Remote Targets and Web-Hooks

We’ll get to what each of these mean in a moment, but in general there are 2 parts to delivery of real-time data from your system:
<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1. A remote target. This is where you wish to have the data sent, when an event occurs in Zaui
<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2. A web-hook that is triggered when an event happens determines what data to be sent when &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;the event occurs in Zaui

## What is a Web-Hook

A web-hook can be thought of as a **"Simplified API"**. So even if you’re not a programmer, the concept of using a web-hook will be easy to understand. You will likely need a program, however, to work with the data that a web-hook delivers. Web-hooks are a server to server connection method.
<br>
<br>
Since, this is a server to server method of data delivery, the server that your sending data, must be capable of:
<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;• Receiving POST data
<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;• Must be a web-server
<br>
<br>
In the simplest form:
<br>
<br>
**_"A web-hook is a method of notification when something has changed in your Zaui system. Notifications based on events that occur, and allows sending data, one-way, to a URL of your choice, upon that event"_**

## Why a Web-Hook

A web-hook allows you the following:
<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;• Allows you to collect information about events as they happen in real-time, when data changes in &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Zaui
<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;• Notify any system, capable to receiving data, via a web POST
<br>
<br>
Web-hooks are simple way of receiving data in real-time. You can create and manage different web-hooks from within Zaui, shuttle data to your URL. It’s that simple!

## Data Formats
Zaui supports both **JSON** and **XML** formats.

## When is Data Delivered
Each web-hook can be configured to deliver data to an URL of your choice. Web-hooks are event driven. Zaui handles the following events:

| Event | Triggered | Description | Data Payload |
| ----- | --------- | ----------- | ------------ |
| Bookings | Creation | There are various channels that allow booking creation, including the back office, online, and the API | Booking Data |
| Bookings | Amendment | Anytime the booking is changed, we will notify your URL | Booking Data |
| Bookings | Cancellation | Anytime the booking is cancelled, we will notify your URL | Booking Data |
| Customers | Creation | When a new customer is created | Customer Data |
| Customers | Amendment | When an existing customer is changed | Customer Data |
| Customers | Removal | When an existing customer is removed | Customer Data |
| Accounts | Creation | Anytime a new account is created | Account Data |
| Accounts | Amendment | When an existing account is changed | Account Data |
| Accounts | Removal | When an existing account is removed | Account Data |
| Contacts | Creation | Anytime a new contact in an account is created | Contact Data |
| Contacts | Amendment | When an existing contact is changed | Contact Data |
| Contacts | Removal | When an existing contact is removed | Contact Data |
| Employees | Creation | Anytime a new employee is created | Employee Data |
| Employees | Amendment | When an existing employee is changed | Employee Data |
| Employees | Removal | When an existing employee is removed | Employee Data |
| Guest Check-In | On Checkin | Any ticket scan event, or check-in event | Check-In Data |
| Package | Creation | When a new package is created | Package Data |
| Package | Amendment | When a package is changed | Package Data |
| Package | Remove | When a package is removed | Package Data |
| Activity | Creation | When a new activity is created | Activity Data |
| Activity | Amendment | When an activity is changed | Activity Data |
| Activity | Remove | When an activity is removed | Activity Data |
| Product | Creation | When a new product is created | Product Data |
| Product | Amendment | When a product is changed | Product Data |
| Product | Remove | When a product is removed | Product Data |

# Event Payloads

## Event Notification Payload

> Example Event Notification Payload

```json
{
"eventNotificationCompanyName":"",
"eventNotificationCompanyIdentifier":"",
"eventNotificationGroupId":"",
"eventNotificationTypeId":"",
"eventNotificationId":"",
"eventNotificationName":"",
"eventNotificationDateTime":"",
"eventNotificationType":"",
"eventData":{ }
}

```


Web-hook event payloads contain 2 broad sets of data:
<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;• Event Notification Payload – describes the type of notification, and when it occurred
<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;• Event Data Payload – contains the event specific data
Payloads describe the data that is delivered &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;to your URL, for each web-hook notification, based on your configuration.
<br>
<br>
As part of every notification data payload that is sent, whether that is booking data, or customer data, our system will tell you which event triggered the delivery.

| Field | Description |
| ----- | ----------- |
| eventNotificationCompanyName | String value describing the name of the company install |
| eventNotificationCompanyUniqueIdentifier | Hash value that describes a unique company install value |
| EventNotificationGroupId | The overall group for which this notification belongs. See the section that describes all possible event groups in the system |
| EventNotificationTypeId | The sub type classification within the even group. See the section that describes all possible groups and group types in the system |
| EventNotificationId | Contains a unique ID for the event as configured within Zaui |
| EventNotificationName | The name of the event as configured with in Zaui |
| EventNotificationDateTime | Date and time stamp of when the notification was generated and delivered |
| EventNotificationType | Type of notification |
| EventData | The event specific data payload |

## Booking Data Payload

> Example of Delivered Payload

```json
{
   "eventNotificationId":"8",
  "eventNotificationName":"on booking create",
   "eventNotificationType":"Booking Creation",
   "eventNotificationDateTime":"2016-04-26 16:53:15",
   "eventData":{
        "booking":{
            "bookingId":"353",
          "bookingSaleDateTime":"2016-09-08 03:54:54",
          "bookingCloseDateTime":"2016-10-20 23:59:59",
          "bookingRevenue":{
                "bookingSubTotal":"1090",
                "bookingSubTotal_formated":"$1,090.00",
                "bookingTax":"0",
                "bookingTax_formated":"$0.00",
                "bookingTotal":"1090",
                "bookingTotal_formated":"$1,090.00"
          },
          "customers":{
             "customer":[
                   {
                   "customerId":"1101",
                   "firstName":"Cindy",
                   "lastName":"Smith",
                   "birthDate":"N\/A",
                   "homePhone":"530",
                   "mobilePhone":"5305254274",
                   "email":"test@zaui.com",
                   "addressLine1":"PO Box 970",
                   "addressLine2":{},
                   "city":"Truckee",
                   "state":"CA",
                   "zipCode":"96162",
                   "country":"United States",
                   "username":"test@zaui.com",
                   "newsLetterOptIn":"false",
                   "loyaltyProgramOptIn":"false",
                   "allowsPrivateDataSharing":"true"                                  
                },
              ]                      
            },
          "activities":{
             "activity":[
                  {
                   "activityId":"9",
                   "packageId":"0",
                   "activityName":"Hamilton to Raglan",
                   "activityDate":"Tuesday April 26 2016",
                   "activityTime":"00:00:00",
                   "activityType":"Rental",
                   "activityIsMultidayRental":"true",
                   "activityIsRental":"true",
                   "activityRentalDuration_Hours":"1",
                   "activityRentalStartDateTime":"2018-01-19 10:50:00",
                   "activityRentalEndDateTime":"2018-01-19 11:50:00",
                   "equipmentAssignmentId":"0",
                   "activityNotes":"",
                   "activityStatus":"Active",
                   "activitySubTotal":"$0.00",
                   "activityTax":"$0.00",
                   "passengers":{
                      "seniors":"0",
                      "adults":"1",
                      "students":"0",
                      "children":"0",
                      "infants":"0"                                        
                }                                  
              },
            ]                      
          },
       "products":{}                
    }          
  }    
}{
    "eventNotificationId":"8",
    "eventNotificationName":"on booking create",
    "eventNotificationType":"Booking Creation",
    "eventNotificationDateTime":"2016-04-26 16:53:15",
    "eventData":{
       "booking":{
         "bookingId":"353",
        "bookingSaleDateTime":"2016-09-08 03:54:54",
        "bookingCloseDateTime":"2016-10-20 23:59:59",
        "bookingRevenue":{
        "bookingSubTotal":"1090",
        "bookingSubTotal_formated":"$1,090.00",
        "bookingTax":"0",
        "bookingTax_formated":"$0.00",
        "bookingTotal":"1090",
        "bookingTotal_formated":"$1,090.00"
        },
          "customers":{
             "customer":[
                  {
                   "customerId":"1101",
                   "firstName":"Cindy",
                   "lastName":"Smith",
                   "birthDate":"N\/A",
                   "homePhone":"530",
                   "mobilePhone":"5305254274",
                   "email":"test@zaui.com",
                   "addressLine1":"PO Box 970",
                   "addressLine2":{},
                   "city":"Truckee",
                   "state":"CA",
                   "zipCode":"96162",
                   "country":"United States",
                   "username":"test@zaui.com",
                   "newsLetterOptIn":"false",
                   "loyaltyProgramOptIn":"false",
                   "allowsPrivateDataSharing":"true"                                  
                },
              ]                      
            },
          "activities":{
             "activity":[
                {
                   "activityId":"9",
                   "packageId":"0",
                   "activityName":"Hamilton to Raglan",
                   "activityDate":"Tuesday April 26 2016",
                   "activityTime":"00:00:00",
                   "activityType":"Rental",
                   "activityIsMultidayRental":"true",
                   "activityIsRental":"true",
                   "activityRentalDuration_Hours":"1",
                   "activityRentalStartDateTime":"2018-01-19 10:50:00",
                   "activityRentalEndDateTime":"2018-01-19 11:50:00",
                   "equipmentAssignmentId":"0",
                   "activityNotes":"",
                   "activityStatus":"Active",
                   "activitySubTotal":"$0.00",
                   "activityTax":"$0.00",
                   "passengers":{
                      "seniors":"0",
                      "adults":"1",
                      "students":"0",
                      "children":"0",
                      "infants":"0"                                        
                    }                                  
                  },
                ]                      
              },
          "products":{}                
    }          
  }    
}
```

**Event Category Trigger**
<br>
• Booking
<br>
**Event Trigger**
<br>
• Create
<br>
• Edit
<br>
• Cancellation

## Customer Data Payload

> Example Customer Data Payload

```json
{
  "eventNotificationId":"7",
  "eventNotificationName":"customer update",
  "eventNotificationType":"Customer Amendment",
  "eventNotificationDateTime":"2016-04-26 16:33:17",
  "eventData":{
    "customer":{ "customerId":"1099",
      "firstName":"Wanna",
      "lastName":"Bet",
      "birthDate":"N\/A",
      "homePhone":{ }, "mobilePhone":{ },
      "email":"wanna@zaui.com",
      "addressLine1":{ },
      "addressLine2":{ },
      "city":{ },
      "state":{ },
      "zipCode":{ },
      "country":{ },
      "username":"wanna@zaui.com",
      "newsLetterOptIn":"false",
      "loyaltyProgramOptIn":"false",
      "allowsPrivateDataSharing":"false"
    }
  }
}
```

**Event Category Trigger**
<br>
• Customer
<br>
**Event Trigger**
<br>
• Create
<br>
• Edit
<br>
• Removal

## Account Data Payload

> Example Account Data Payload

```json
{
  "eventNotificationId":"9",
  "eventNotificationName":"Account has changed",
  "eventNotificationType":"Account Amendment",
  "eventNotificationDateTime":"2016-04-26 17:06:34",
  "eventData":{
      "account":{
          "accountId":"703",
          "accountName":"4 SightSeeing Information & Bookings",
          "accountGroupName":"4 SightSeeing Information & Bookings",
          "accountGroupId":"113",
          "phone":{ },
          "website":"www.zaui.com",
          "fax":{ },
          "otherPhone":"N\/A",
          "employees":{ },
          "manager":{ },
          "email":"accounts@zaui.com",
          "businessNumber":{ },
          "annaulRevenue":{ },
          "industry":"NZ AGENT",
          "accountType":"New Zealand",
          "accountRateType":"Wholesale (Discount\/Invoice)",
          "primaryAddress":"12 Queen Street",
          "primaryCity":"Auckland",
          "primaryState":{ },
          "primaryZip":{ },
          "primaryCountry":"New Zealand",
          "description":"This company is so much fun to work with."
        }
    }
}
```

**Event Category Trigger**
<br>
• Account
<br>
**Event Trigger**
<br>
• Create
<br>
• Edit
<br>
• Removal

## Contact Data Payload

> Example Contact Data Payload

```json
{
  "eventNotificationId":"3",
  "eventNotificationName":"A contact has been updated",
  "eventNotificationType":"Contact Amendment",
  "eventNotificationDateTime":"2016-04-26 17:08:43",
    "eventData":{
        "contact":{
            "contactId":"575",
            "accountId":"705",
            "accountName":"Antipodes Voyages",
            "department":{ },
            "title":{ },
            "officePhone":"6045669284",
            "fax":"6045669284",
            "firstName":"ANTIPODES Voyages",
            "lastName":{ }, "birthDate":"N\/A",
            "homePhone":"6045669284",
            "mobilePhone":"6045669284",
            "email":{ },
            "addressLine1":"607",
            "addressLine2":{ },
            "city":"Vancouver",
            "state":"BRITISH COLUMBIA",
            "zipCode":"V6B2V2",
            "country":"Canada",
            "username":"ANTVOY"
        }
    }
}
```

**Event Category Trigger**
<br>
• Contact
<br>
**Event Trigger**
<br>
• Create
<br>
• Edit
<br>
• Removal

## Employee Data Payload

> Example Employee Data Payload

```json
{
  "eventNotificationId":"6",
  "eventNotificationName":"update employee",
  "eventNotificationType":"Employee Amendment",
  "eventNotificationDateTime":"2016-04-26 16:12:48",
  "eventData":{
    "employee":{
        "employeeId":"1098", "employeeType":"Admin",
        "accountId":"1",
        "accountName":"",
        "firstName":"Ben",
        "lastName":"Wanterby",
        "title":"A Driver",
        "birthDate":"N\/A",
        "department":"Drivers",
        "homePhone":"6045669284",
        "mobilePhone":"6045669284",
        "officePhone":"6045669284",
        "fax":"6045669284",
        "email":"help@zaui.com",
        "addressLine1":"Suite 606 318 Homer Street",
        "addressLine2":{ },
        "city":"Vancouver",
        "state":"British Columbia",
        "zipCode":"V2B2V2",
        "country":"Canada",
        "username":"qwe"
        }
    }
}
```

**Event Category Trigger**
<br>
• Employee
<br>
**Event Trigger**
<br>
• Create
<br>
• Edit
<br>
• Removal

## Guest Check-In Data Payload

> Example Guest Check-In Data Payload

```json
{
  "eventNotificationDateTime": "2017-11-19 8:54:38",
  "eventNotificationGroupId": "700",
  "eventNotificationTypeId": "700",
  "eventNotificationId": "1",
  "eventNotificationIpAddress": "174.6.183.62",
  "eventNotificationName": "Checkin",
  "eventNotificationType": "Activity Check-in",
  "eventData": {
    "checkinData": {
        "bookingId": "140",
        "checkedIn_activityDate": "2017-11-19",
        "checkedIn_activityId": "2",
        "checkedIn_activityName": "Waterfalls & Canyons",
        "checkedIn_activityTime": "8:00 am", "checkedIn_checkInCurrentStatus": "true", "checkedIn_guestId": "97",
        "checkedIn_message": "Checked-in the guest for Waterfalls & Canyons on 2017-11-19 at 8:11:38",
        "checkedIn_systemUsername": "Bob"
        }
    },
}
```

**Event Category Trigger**
<br>
• Guest Check-In
<br>
**Event Trigger**
<br>
• On toggle of check-in status

## Package Data Payload

> Example Event Package Payload

```json
{
  "eventNotificationGroupId": "800",
  "eventNotificationTypeId": "800",
  "eventNotificationDateTime": "2017-11-19 8:34:31", "eventNotificationId": "2",
  "eventNotificationIpAddress": "174.6.183.62",
  "eventNotificationName": "Package Create Notification",
  "eventNotificationType": "Package Created",
  "eventData": {
    "packageData": {
      "packageId": "9",
      "packageName": "Ultimate Day Tour Package"
    }
  },
}
```

**Event Category Trigger**
<br>
• Packages
<br>
**Event Trigger**
<br>
• Create
<br>
• Edit
<br>
• Removal

## Activity Data Payload

> Example Activity Data Payload

```json
{
  "eventNotificationGroupId": "900",
  "eventNotificationTypeId": "900",
  "eventNotificationDateTime": "2017-11-19 8:34:31",
  "eventNotificationId": "2",
  "eventNotificationIpAddress": "174.6.183.62",
  "eventNotificationName": "Activity Create Notification",
  "eventNotificationType": "Activity Created",
    "eventData": {
      "activityData": {
        "activityId": "1971",
        "activityName": "Brewery Tours PM"
      }
  },
}
```

**Event Category Trigger**
<br>
• Activities
<br>
**Event Trigger**
<br>
• Create
<br>
• Edit
<br>
• Removal

## Product Data Payload

> Example Product Data Payload

``` json
{
  "eventNotificationGroupId": "1000",
  "eventNotificationTypeId": "1000",
  "eventNotificationDateTime": "2017-11-19 8:34:31",
  "eventNotificationId": "2",
  "eventNotificationIpAddress": "174.6.183.62",
  "eventNotificationName": "Product Create Notification",
  "eventNotificationType": "Product Created",
  "eventData": {
    "productData": {
      "productId": "423",
      "productName": "Large Mens Zip Line T-Shirt"
      }
  },
}
```

**Event Category Trigger**
<br>
• Products
<br>
**Event Trigger**
<br>
• Create
<br>
• Edit
<br>
• Removal

# Event Notification Groups and Types

| Event Group | Group ID | Event Type | Type ID |
| ----------- | -------- | ---------- | ------- |
| Bookings | 100 | Create | 100 |
| Bookings | 100 | Update | 101 |
| Bookings | 100 | Remove | 102 |
| Customers | 200 | Create | 200 |
| Customers | 200 | Update | 201 |
| Customers | 200 | Remove | 202 |
| Accounts | 300 | Create | 300 |
| Accounts | 300 | Update | 301 |
| Accounts | 300 | Remove | 302 |
| Contacts | 400 | Create | 400 |
| Contacts | 400 | Update | 401 |
| Contacts | 400 | Remove | 402 |
| Employees | 500 | Create | 500 |
| Employees | 500 | Update | 501 |
| Employees | 500 | Remove | 502 |
| Check-In | 700 | Toggle Status | 700 |
| Packages | 800 | Update | 801 |
| Packages | 800 | Update | 801 |
| Packages | 800 | Remove | 802 |
| Activities | 900 | Create | 900 |
| Activities | 900 | Update | 901 |
| Activities | 900 | Remove | 902 |
| Products | 1000 | Create | 1000 |
| Products | 1000 | Update | 1001 |
| Products | 1000 | Remove | 1002 |


# Legal

The Zaui Web-Hook and Remote Target API (the “API”) is owned and operated by Zaui Software. If you use the API, you will be able to access data from any partner Supplier within the Zaui system. Listed below are the terms and conditions of use (the “Terms”) for this API. By using, accessing and/or viewing information on the API, you agree to be bound by these Terms. If you violate these Terms, Zaui Software has the right to terminate your use of the API and/or take appropriate legal actions against you. We reserve the right to change these Terms at any time without notice.

## Acceptance of Terms

In order to use the API you must agree to these Terms. You represent that you have the full power, capacity and authority to accept these Terms. If you are accepting on behalf of a business entity, you represent that you have the full legal authority to bind the business entity to these Terms. These terms are in addition to the standard Zaui Software Terms of Service.

## Permitted Use

You may access, view and make copies of the data in the API for your personal or commercial use. Due to the special features of API, by accessing and viewing information from API you agree to be bound by these special terms:

1. You will not modify the data from API in any way
2. You will not modify the link structure to API

### Subject to these Terms, Zaui Software gives you a personal, worldwide, non-assignable and non-exclusive license to the API.

## Restrictions

You may not:

1. Display the API in any manner that implies a relationship or affiliation with, sponsorship, or endorsement by Zaui or that can be reasonably interpret to suggest content represents the views or opinions of Zaui.
2. Use the API to disparage Zaui or its products, partners or product suppliers.
3. Use the API on your website if the website promotes illegal activity, contains pornography, gambling, or the sale of tobacco or alcohol to individuals under the age of legal consumption.
4. Delete or alter any trade names, trademarks, service marks, logos, domain names or other distinctive brand features of Zaui that are included in the API in applications or programs that you create.
5. Reverse engineer, decompile or otherwise attempt to extract the source code of the API or any part thereof, unless this is expressly permitted or required by applicable law.
6. Access, tamper with, or use non-public areas of the Services, Zaui computer systems, or the technical delivery systems of Zaui providers; (ii) probe, scan, or test the vulnerability of any system or network or breach or circumvent any security or authentication measures.
7. Access or search or attempt to access or search the Services by any means (automated or otherwise) other than through our currently available, published interfaces that are provided by Zaui, unless you have been specifically allowed to do so in a separate agreement with Zaui.
8. Forge any TCP/IP packet header or any part of the header information in any email or posting, or in any way use the Services to send altered, deceptive or false source-identifying information.
9. Interfere with, or disrupt, (or attempt to do so), the access of any user, host or network, including, without limitation, sending a virus, overloading, flooding, spamming, mail-bombing the Services, or by scripting the creation of Content in such a manner as to interfere with or create an undue burden on the Services.

## Rate Limits and Monitoring

Your use of the Zaui WebHooks and Zaui Content are subject to certain limitations on access, calls, and use as determined by Zaui, at its sole discretion. If Zaui believes that you have attempted to exceed or circumvent these limitations, your ability to use the Zaui WebHooks and ZContent may be temporarily or permanently blocked. Zaui may monitor your use of the Zaui API to improve the Zaui service and to ensure your compliance with these Terms.

## Ownership/Trademarks

You do not acquire or have any ownership, license or other proprietary interest in the API. You understand that the API is protected by copyrights, trademarks, service marks, patents and other proprietary rights and laws.

## Privacy Policy

The use of personal information is governed by our <a href="https://www.zaui.com/privacy" target="_blank"_>Privacy Policy</a> and the <a href="https://www.zaui.com/terms-of-service/" target="_blank"_>Zaui Terms of Service</a>.

## Limitation of Liability

Zaui assumes no responsibility for, and shall not be liable for, any damages or expenses you may incur as a result of any inaccuracy, incompleteness or obsolescence of anything contained in the API. THE SERVICES OF THE API ARE PROVIDED “AS IS”, WITH NO WARRANTIES WHATSOEVER. Without limiting the generality of the forgoing, you agree that neither Zaui nor any of its affiliates, employees or agents will be liable to you or to any other party for any direct or indirect damages, or for any special, exemplary, punitive, incidental, consequential or other damages (including, but not limited to, lost profits or lost time), whether based on contract, tort, strict liability or otherwise, which arise out of or are in any way connected with any access to the API or any viewing or use of any information on the API. You acknowledge that the limitations in this Section are reasonable and appropriate. Zaui DISCLAIMS ALL WARRANTIES REGARDING THE ACCURACY, COMPLETENESS, CURRENCY OR RELIABILITY OF THE DATA IN THE API, INCLUDING, WITHOUT LIMITATION, ANY IMPLIED WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, NON-INFRINGEMENT OR OTHERWISE ARISING BY LAW OR STATUTE. YOU AGREE THAT YOUR USE OF, OR RELIANCE UPON, ALL DATA OBTAINED THROUGH THE API IS AT YOUR OWN DISCRETION AND RISK.

## Unauthorized Use/No Interference

You agree that you will not use or attempt to use any method, device, software or routine to harm others or interfere with functioning of the API or use and/or monitor any information in or related to the API for any unauthorized purpose.

By using the API in applications or programs you create, you agree to be solely liable for any damage resulting from any infringement of copyrights, proprietary rights, or any other harm (including but not limited to harm caused by spyware, malware, worms, Trojan horses and viruses) resulting from such application or program.

## Indemnification

You agree to indemnify and to hold Zaui, its subsidiaries, affiliates, business partners, officers, employers and other agents, harmless from and against any loss, liability, damage or expense (including reasonable attorneys fees) arising out of your use of the API, including, without limitation, any violations by you of these Terms.

## Termination

Without limiting its other remedies, Zaui may immediately discontinue, suspend, terminate or block your and any user’s use of the API at any time in its sole discretion. You may terminate this agreement by ceasing to use the API or any product incorporating it.

Zaui may in its sole discretion choose to upgrade the current version of the API at any time without notice to you, which may make the version of the API that you are using obsolete.

## Accuracy of Information

ALL INFORMATION IN THE API IS PROVIDED TO YOU ON AN “AS-IS” BASIS. ZAUI SOFTWARE DISCLAIMS ALL WARRANTIES REGARDING THE ACCURACY, COMPLETENESS, CURRENCY OR RELIABILITY OF ANY INFORMATION IN THE API, INCLUDING, WITHOUT LIMITATION, ANY IMPLIED WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, NON-INFRINGEMENT OR OTHERWISE ARISING BY LAW OR STATUTE.

## Transmission Failures

Zaui will use commercially reasonable efforts to publish and transmit the API on a continuous and timely basis. Zaui is not, however, responsible for any failure or malfunction in communications; for any failure or refusal of any third party transmission intermediaries to transmit any API; or for the failure to transmit any API resulting from any natural disasters, wars, labor strike or other events beyond the control of Zaui.

## Limitation of Liability

You acknowledge that, Zaui cannot and does not assume any responsibility for, and shall not be liable for, any damages or expenses you may incur as a result of any inaccuracy, incompleteness or obsolescence of any information contained in the API. You agree that Zaui will not be liable to you or to any other party for any direct or indirect damages, or for any special, exemplary, punitive, incidental, consequential or other damages (including, but not limited to, lost profits or lost time), whether based on contract, tort, strict liability or otherwise, which arise out of or are in any way connected with any access to the API or any contractual or other dealings or relationships you may have with third parties based upon any information included in the Zaui.

## Governing law/Jurisdiction

These terms and conditions and your access to and use of information from the API are governed by the laws of the Province of British Columbia. In the event of any dispute regarding the interpretation or compliance with these terms and conditions, you consent to the exclusive jurisdiction of the Provincial and Federal courts located in British Columbia.

## Entire Agreement

These terms and conditions of use for this API constitute the entire agreement between you and Zaui regarding your access to the API and your reproduction and use of any information in the API. Any waiver of any term or condition shall not be effective unless in a written document signed by an authorized representative of Zaui.
