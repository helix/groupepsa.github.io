---
title: Car.GetDrivingState()
layout: headunit-sdk
supported:
  - 2
  - 3
  - 4
type: api
---

### `Car.GetDrivingState()`

| **Description** | Determines whether the user is driving their car or not.
| **Response** | *Boolean*  `True` if the speed is higher than 5km/h (default value), else `False`.
| **Parameter**   | *Void*

#### Example

```javascript
if (Car.GetDrivingState() == false) {
	Startapplication()
} else {
	DisplayDrivingWarning()
}
```
	
#### Remark

>**Note :** The 5km/h limit to delimit the driving states can be changed by diagnostic.