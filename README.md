# AnalyticsDocumentation

This documentation gives clear idea of how the nLearn application is keeping track of all the events.

It mainly has followings:

* AnalyticsModule
* AnalyticsTracker
* AnalyticsHashmap
* (XYZ)Analytics

## Working of the entire ecosystem

This module takes in all the basic component from the **App Component** and then eventually provides the 
instance of **AnalyticsTracker** which will further be used by **(XYZ)Analytics** to call the methods available in 
AnalyticsTracker itself. The methods in AnalyticsTracker that will be used by  **(XYZ)Analytics** will further use 
**AnalyticsHashmap**, which will provide a HashMap with basic OS-level attributes already added to it as a key-value pair. Inside AnalyticsTracker, methods will further add more attribute to the available HashMap to make it ready to lauch as an event using **AnalyticsClient**. 

For Analytics events, we're using [Amazon Web Service SDK](https://aws-amplify.github.io/docs/android/analytics)

Now, let's discuss about the individual player of the ecosystem. 

### AnalyticsModule

AnalyticsModule is like any other module which is used to provide instance to be used by Dagger ***@inject** annotation*.
It uses **CognitoPoolID**, **Region**, **CognitoCachingCredentialsProvider** and **PinpointManager** to eventually provide the instance of **AnalyticsTracker** at runtime. 

![image](https://i.imgur.com/pWIJKcM.png)



### (XYZ)Analytics

(XYZ)Analytics is just a common name of any custom-analytics class for any Activity/Fragment or any other View, **XYZ** will be replaced by the specific name of the View. Ex:- PracticeAnalytics etc. 

(XYZ)Analytics uses [Singleton design pattern](https://en.wikipedia.org/wiki/Singleton_pattern) to create only one instance throughout. 

![image](https://i.imgur.com/w1QGH1O.png)


### AnalyticsHashMap

AnalyticsHashMap class does nothing but creates a HashMap and adds certain OS-level attributes like *PLATFORM*, *APP_VERSION*, 
*NETWORK_TYPE*, *OS_VERSION*, *DEVICE_ID*(which is a unique session ID from **Settings.Secure**) and *TIMESTAMP*.



### AnalyticsTracker

AnalyticsTracker takes in all the attributes from AnalyticsHashMap and (XYZ)Analytics and then adds some more preference-level
attribute(like STUDENT_ID, ADMISSION_NO, UUID, EVENT_GROUP) to the resultant HashMap to submit the event instance that was created as shown using PinpointManager.

![image](https://i.imgur.com/y2IsV3W.png)
