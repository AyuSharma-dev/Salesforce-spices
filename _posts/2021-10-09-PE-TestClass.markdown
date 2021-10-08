---
layout: post
title: Test class for Platform Events
date: 2021-10-8
description: Learn how to cover and test the Platform Events logic in Test classes. # Add post description (optional)
icon: pe-testClass.jpg # Add image post (optional)
img: pe-testClass.jpg
fig-caption: # Add figcaption (optional)
tags: [Salesforce, Platform Events, APIS, Test Class]
---

## What we are about to learn
In This blog we will Learn how to Create a Test class for the Platform Event logic with valid unit testing.


## Overview
Platform Events are cool, fast, easy and optimized way to build an Integration between two sources with a real time sync. Platform events are easy to setup and publish as we discussed in our previous [blog]({{site.baseurl}}/Setup-SF-PE-intro/). 

Test class are compulsory in Salesforce with atleast 75% of code coverage but along with Code coverage an ideal class should have proper unit testing with System asserts for the performed logic in the main class. 

Creating Test classes for Platform Events can be pain because Test classes cannot subscribe to the Platform Events till now so you never know if events are published successfully. In the below part we will see how to test out that if your Platform events are published successfully or stopped due to some error. 


### Main Class

```java
public without sharing class PublishEventsClass {
    
    @TestVisible private static Integer successPublishCount; //This variable will keep the Successful Events number

    public static void publishAccountDetails( List<Account> newAccounts ){
        List<event__e> eventsToPublish = new List<event__e>();
        for( Account acct : newAccounts ){
            eventsToPublish.add( new event__e( Name = acct.Name, website__c = acct.Website ) ); //Creating Events to Publish
        }

        if(!eventsToPublish.isEmpty()){
            List<Database.SaveResult> results = EventBus.publish(eventsToPublish); 
            successPublishCount = 0;
            for (Database.SaveResult sr : results) {
                if (sr.isSuccess()) {
                    System.debug('Successfully published event.');
                    successPublishCount += 1; //Increment for each successful event
                } else {
                    if( sr.getErrors().size() > 0 ){
                        System.debug('Error::'+sr.getErrors().size());
                    }
                }
            }
        }
    }
}
```

### Test Class For The Above Class

```java
@isTest
private without sharing class PublishEventsClassTest{
    
    @isTest
    public static void testMethodEx() {
        List<Account> accounts = new List<Account>();
        for( Integer i=0; i<10; i++ ){
            accounts.add( new Account( Name = 'test '+i ) ); //Creating Sample Account records.
        }

        Test.startTest();
        PublishEventsClass.publishAccountDetails( accounts ); //Calling the Publish method with Accounts
        Test.stopTest();

        //Below Assert will check if there are less Successfully published events then the number of Accounts Passed.
        System.assertEquals( accounts.size(), PublishEventsClass.successPublishCount, 'Platform Events not Published Successfully.' );
    }
}
```

<br/>
Above Unit testing method will make the test class fail if there are some issues in Publishing the events. So instead of just getting the code coverage we should always try to test the executed logics in the main class.

Thanks for Reading !!

<br/>
### Related Blogs
[Introduction to Salesforce Platform Events]({{site.baseurl}}/Setup-SF-PE-intro/)<br/>
[Platform Events Test in Real Time]({{site.baseurl}}/PE-Tester/)<br/>

