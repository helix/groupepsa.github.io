---
title: Car.distanceUnit
layout: headunit-sdk
supported:
  - 2
  - 3
  - 4
type: event
---

Event triggered when the distance unit is changed.

### Example

```javascript
try {
	
	// Car
	if ((typeof Car !== "undefined") && (typeof Car.addEventListener !== "undefined")) {
		Car.addEventListener("distanceUnit", function(){
			alert("The distance unit is now :" + Car.GetDistanceUnit() );
		});
	}
}catch(e) {
	DealWithCarError(e);
}
```