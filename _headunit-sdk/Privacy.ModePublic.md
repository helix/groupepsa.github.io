---
title: Privacy.ModePublic
layout: headunit-sdk
supported:
  - 3
  - 4
type: event
---
Event triggered when the Public privacy mode is selected.

### Example

```javascript
try {
	// Privacy
	if ((typeof Privacy !== "undefined") && (typeof Privacy.addEventListener !== "undefined")) {
		Privacy.addEventListener("ModePublic", function(){
			alert("Public privacy mode is now active");
		});
	}
} catch(e) {
	DealWithPrivacyError(e);
}
```