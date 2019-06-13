# AnalyticsDocumentation

This documentation gives clear idea of how the application is keeping track of all the events.

It mainly has 

* AnalyticsModule
* AnalyticsTracker
* AnalyticsHashmap
* (XYZ)Analytics

## Working of the entire ecosystem

This module takes in all the basic component from the **App Component** and then eventually provides the 
instance of **AnalyticsTracker** which will further be used by **(XYZ)Analytics** to call the methods available in 
AnalyticsTracker itself. The methods in AnalyticsTracker that will be used by  **(XYZ)Analytics** will further use 
**AnalyticsHashmap**, which will provide a HashMap with basic OS-level attributes already added to it as a key-value pair. Inside AnalyticsTracker, methods will further add more attribute to the available HashMap to make it ready to lauch as an event using **AnalyticsClient**. 

Now, let's discuss about the individual player of the ecosystem. 

### AnalyticsModule

AnalyticsModule is like any other module which is used to provide instance to be used by Dagger ***@inject** annotation*.
It uses **CognitoPoolID**, **Region**, **CognitoCachingCredentialsProvider** and **PinpointManager** to eventually provide the instance of **AnalyticsTracker** at runtime. 

[!image](https://i.imgur.com/pWIJKcM.png)

