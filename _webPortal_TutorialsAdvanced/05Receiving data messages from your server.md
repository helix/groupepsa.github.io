---
title: Receiving Data Messages from server
layout: page2
---

# Receiving data messages from your server

When receiving data from your server, if :

- The NAC module is active
- Your application is launched (not in background)

Then we are in the **Foreground** case.

If at least one of those 2 conditions is not fulfilled then we are in the **Background** case.

#### What you need

- [Being connected to the MQTT Broker]({{ site.baseurl }}/webportal_TutorialAdvanced/#connecting-to-the-mqtt-broker)

- Your [MQTT Publishing Topic]({{ site.baseurl }}/webportal_TutorialAdvanced/#selecting-your-mqtt-publishing-topic) looking as follows :
	psa/OVIPPartners-Dev/from/uid/{UID}/opa/{VIN}/

- Your properly set up server

#### Foreground

When both WebPortal and your application are running, your messages are transmitted directly by WebPortal using the HTML5 API `window.postMessage()`

To retrieve your messages you have to implement the `"message"` event handler and filter on the type `WebPortal.onCurrentNotificationReceived`


**Implementation example :**
```javascript
	window.addEventListener('message', function(messageEvent) {
	    let webportalMessage = messageEvent.data;
	
	    if (webportalMessage.type === 'WebPortal.onCurrentNotificationReceived') {
	        let mqttMessagePayload = webportalMessage.value;
	        let appServerMessage = mqttMessagePayload.content;
	
	        // Use your own application message handler
	        myHandleServerMessage(appServerMessage);
	    }
	});
```

#### Background

When WebPortal is in background or your application isn't running, WebPortal keeps in cache memory the last 10 data messages sent to your application.

To retrieve those pending messages you have to use the `WebPortal.getPendingNotifications()` method that is directly injected in your application's `window` object and so can be called directly.

In order to retrieve the messages over time, you can call this method :

- at fixed interval, using `setTimeout` or `setInterval`
- when detecting the following WebPortal events being triggered :
	+ `WebPortal.onApplicationShow`  
	+ `WebPortal.onApplicationHide`


**Implementation example :**

```javascript
/**
 * Get the buffered messages for application 'appId'
 * and clean/reset the WebPortal's buffer
 * 
 * @param {string} Application id
 * @return {array} List of buffered MQTT messages or empty array if none
 */
WebPortal.getPendingNotifications = function(appId) {};

const MY_APP_ID = 'some_id';

(function processWebportalPendingNotifications() {
	let pendingNotifications = WebPortal.getPendingNotifications(MY_APP_ID);
	for (let i = 0; i < pendingNotifications.length; ++i) {
		let mqttMessage = pendingNotifications[i];

		/*
		mqttMessage = {
			"content": {
				// application data here
			}
		}
		*/

		//Use your own function to process the message
		processMqttMessage(mqttMessage);
	}

	setTimeout(processWebportalPendingNotifications, 5000);
})();
```