---
title: Car.fuelUnit
layout: headunit-sdk
supported:
  - 2
  - 3
  - 4
type: event
---
Event triggered when the fuel unit is changed.

### Example

```javascript
try {
	
	// Car
	if ((typeof Car !== "undefined") && (typeof Car.addEventListener !== "undefined")) {
		Car.addEventListener("fuelUnit", function(){
			alert("The fuel unit is now:" + Car.GetFuelUnit());
	}
}catch(e) {
	DealWithCarError(e);
}
```