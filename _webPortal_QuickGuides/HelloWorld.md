---
title: Selecting MQTT publishing topic
layout: page2
---

# Information available

The API will allow you to get the following information :

- `Car` : Get information about the vehicle : VIN code, Fuel type, unit and level, Current speed and unit, Mileage and distance unit, Autonomy, level of battery and fuel, the driving state, the time, 
- `Connectivity` : Detect the connectivity status
- `Device` : Request a popup, get hardware and software version of the system, 
- `HMI` : Information on the user, UIN, language, country, 
- `Media` : Information on the media : album name, artist name, current track, state of the media, type of media
- `Navigation` : Get the current position info, destination info, maneuver info, journey info, waypoint info, start new journey, 
- `Phone` : Launch phone call,
- `Privacy` : Manage privacy mode of user
- `Radio` : Information on the radio : frequency, preset...
- `System` : Settings action reserved to administrative use
- `Webportal` : All the events associated to user interaction or due to server

# Hello World

This tutorial will guide you through the creation of your Application.  
You can start by downloading the base of your application <a href="{{ site.baseurl }}/helloworld.zip" download="">Here</a>.


## HTML

The HTML part of your project is conventional, you create your objects and static content.

```html
<!-- STYLES -->
<link rel="stylesheet" type="text/css" href="css/main.css">
<!-- SCRIPTS -->
<script type="text/javascript" src="../test/shared/libs/jquery/1.10.0/jquery.js"></script>
<script type="text/javascript" src="js/main.js"></script>

<div id="mainContainer">
    Hello World!
</div>
```

## CSS

You can customize your CSS stylesheet, here is simply an example changing the color of the text displayed.

```css
//Your normal css file
#mainContainer {
    color: blue;
}
```

## JS

Here you have the required JS for your application to function properly. You can add the functions you need to handle other events.

```javascript
//On document ready
$(document).ready(function() {
    
    // Inform the parent window (applications portal) that the application is
    // loaded and ready
    window.parent.postMessage({
        'type' : 'WebPortal.onApplicationLoaded'
    }, '*');
});
```

##  Structure to submit Application
![Application Structure]({{ site.baseurl }}/the_structure.png)

Once developped you have to submit your application to PSA for us to check its behavior before actually deploying it.
The structure of the file to submit is mostly free with some requirements:

- The files must be sent in a TAR archive compressed via GZIP
- The *.md5* file is required in order to perform an integrity check
- An *index.html* file must be present at the root of the project and is the starting point of the application
- The logo for the application: *icon-100x100.png* (15kB max) and *icon-136x136.png* (21kB max) must be present at the root of the project for the different screen sizes.
- JavaScript functions must be executed when the DOM is ready
- It is required to add a version file in the root directory of the app, named info.json and containing the following information :
```json
{
  "artifactId": "appid",
  "name": "appname (optional)",
  "description": "appdescription (optional)",
  "version": "X.Y.Z",
  "buildDate": "YYYY-MM-DD HH:mm"
}
```

**In addition** to the package submitted, the following information must be provided separately :
+ **App name (translated if needed)** The partner must provide at least one name for its app, that can be translated into several languages if needed. The master name will be displayed if no translation was given for the language chosen by the user.
+ **Country scope** The partner must provide the list of countries where the app can be activated for customers, within the list of countries where the WebPortal is available.
+ **Brand scope** The partner must provide the list of brands for which the app can be activated for customers. Today, Peugeot, Citroën, DS, Opel and Vauxhall are available.
+ **Device scope** The partner must provide the list of devices and configurations where the app can be activated for customers. Today NACw2.1, NACw3.1 and NACw4 are available.
+ **App identifier** To be given by PSA, this App Id is mandatory as it enables us to identify the app in MQTT exchanges and in the process of display in the vehicles.
+ **MQTT partner account**
