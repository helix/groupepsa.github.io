---
title: Radio.GetBand()
layout: headunit-sdk
supported:
  - 2
  - 3
  - 4
type: api
---

### `Radio.GetBand()`

| **Description** | Gets the currently used Radio Band.
| **Response** | *String*  The currently used radio band.
| **Parameter**   | *Void*

#### Example

```javascript
//Get the Radio Band
let RadioBand = Radio.GetBand()
```

#### Remark

The possible values for the radio band are the following strings:
- FM
- DaB
- MW

But all values are:
- FM HD
- MW
- LW
- FM
- DaB
- DMB
- SDaRS
- DaB+