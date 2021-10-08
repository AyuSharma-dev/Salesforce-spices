---
layout: post
title: Salesforce Platform Events
date: 2021-10-7
description: What are Salesforce Platform Events and How to use them # Add post description (optional)
icon: PE-Info-Main.jpg # Add image post (optional)
img: PE-Info-Main.jpg
fig-caption: # Add figcaption (optional)
tags: [Salesforce, Platform Events, APIS, Integration]
---

## What we are about to learn
* What are Platform Events
* Create Platform Events
* Publish Platform Events using Apex
* Platform Event Limitations

## What are Salesforce Platform Events

Use platform events to connect business processes in Salesforce and external apps through the exchange of real-time event data. Platform events are secure and scalable messages that contain data. Publishers publish event messages that subscribers receive in real-time. To customize the data published, define platform event fields.

Platform events are just like Custom Objects that can be Published with the information within their fields and can be subscribed by External( MuleSoft ) or Internal( Lightning Web Components, Flows ) Sources to provide Real-time information sync between systems.

## Create and Publish Platform Events

To create Platform event object follow below steps:

* Go to setup and Search Platform Events
* Click on Platform Events.
* Here click new. You can provide Label and API Name of your Platform event here.
* Now click on Save.
* After Your Platform Event object created scroll down to custom fields section and click new here.
* Create a new field:
    * API Name: Message
    * Label: Message
    * Type: Text(255)

 Your Platform Event Object should look like below

![Install CLI page]({{site.baseurl}}/assets/img/PlatformEvent-SS-1.png)

## Publish Platform Events Using Apex:

To Publish a Platform Event we can utilize Apex Anonymous scripts. You can also use the same code to Publish Platform Event from your Apex Trigger and Batch.

Copy paste the below Script into your Developer Console Execute Apex Anonymous window
Here the Triggers related List show if you have created any Apex Triggers for the Platform Events. Platform Events only support After Insert Triggers. The Subscriptions list shows all the sources that have subscribed to this Events. This list will not show any Source that subscribe using CometId.

```java
Database.SaveResult result = EventBus.publish( new Case__e( Message__c='Test Message' ) );
if (result.isSuccess()) {
    System.debug('Successfully published event.');
} else {
    if( result.getErrors().size() > 0 ){
        System.debug('Error::'+result.getErrors());
    }
}
```

Replace the Case__e with your Platform Event API name and provide any values for Message__c field. Now click on Execute. Check for Debug logs if it show shows success message then you Events are published successfully.

To checkout what information is published from your Platform event, we will discuss this in our next blog.

## Platform Event Limitations

While using the Events one should always take considerations over the Govern Limits provided by the Salesforce for creating and publishing Events. Following are some of those limits:

| Description | Unlimited  | Enterprise |  Developer |  Professional Edition |
| :---: | :---: | :---: |
| Maximum number of platform event definitions that can be created in an org | 100 | 50 | 5 | 5 |
| :---: | :---: | :---: |
| Maximum number of concurrent CometD clients (subscribers) across all channels and for all event types | 2000 | 1000 | 20 | 20 |
| :---: | :---: | :---: |
| Maximum number of processes that can subscribe to a platform event | 4000 | 4000 | 4000 | 5 |
| :---: | :---: | :---: |
| Maximum number of active processes that can subscribe to a platform event | 2000 | 2000 | 2000 | 5 |


So as we have seen Platform events can be a great tool for Automated Integration but we should also keep an on all the Limits and also on if the requirement really needs Platform Events.

Thanks for Reading !!