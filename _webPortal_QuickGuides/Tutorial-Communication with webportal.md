---
title: Communicating with webportal
layout: page2
---

# Communicating with WebPortal

The WebPortal will forward events to your application in order to be informed about the current state of both the App and the Portal.

To deal with these events you will need to implement *event listeners* and call the functions you need in each case.
Below is an example on how to manage them.

```javascript
//Global messages listeners
    window.addEventListener("message", function(event){

	    var data = event.data;
	    var type = event.data.type;

	    switch(type){

	    //When the application is killed or reloaded via an update
	    case "WebPortal.onApplicationUnloaded":
		console.log("The application will be killed, it's time to save your application data");
		alert("The application will be killed, it's time to save your application data");
		break;

		//When the application is put in background    
	    case "WebPortal.onApplicationHide":  
		console.log("Application is hidden");
		alert("Application is hidden");
		break;

		//When the application is put in foreground
	    case "WebPortal.onApplicationShow":
		console.log("Application is shown");
		alert("Application is shown");
		break;

	    //When a notification is pushed to the application
	    case "WebPortal.onCurrentNotificationReceived":
		if (typeof data.value !== 'undefined'){
		    console.log("Notification received",data.value);
		    if (typeof data.value === 'object'){
			alert("Notification received : "+JSON.stringify(data.value));
		    } else {
			alert("Notification received : "+data.value);
		    }
		}
		break;
	    }
});
```

# WebPortal Message

WebPortal is in charge of sending data to and from your Application

### Structure of a WebPortal message
```javascript
	{
		/**
		 * @type {string}
		 */
		"type": "WebPortal.onCurrentNotificationReceived",

		/**
		 * Only present when type=WebPortal.onCurrentNotificationReceived
		 * Contains the payload of the MQTT message
		 */
		"value": {}
	}
```