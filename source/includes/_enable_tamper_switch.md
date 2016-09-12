## `/products/<imei>/enable_tamper_switch`

### Description
Each unit is fitted with a "tamper_switch" which will raise alerts if a customer is tampering with a unit.
This switch can be enabled/disabled remotely, particularly useful for periods of time where the switch could be accidentally triggered raising a false alert. This is common in, for example, transportation or installation.

### Endpoint

> A `PUT` request to this endpoint enables the tamper switch on the unit.

```python
    url = "http://smartapi.bboxx.co.uk/v1/products/000000000000/enable_tamper_switch"
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=' + A_VALID_TOKEN}

    r = requests.put(url=url, headers=headers)

    print r.json()
    >>> {
        "status": "success",
        "message': "Product #000000000000000 tamper_switch_enabled",
        "data": None
    }
```

This endpoint is used to enable the tamper switch on a unit. The imei of the unit to be enabled is specified in the url.

    | value
---:|:------
__endpoint__ | `/products/<imei>/enable_tamper_switch`
__method__ | `PUT`
__url_params__ | `product_imei` _(str)_
__payload__ | None
__response__ | 200

Note that if a unit is already enabled the API will return "success" anyway.

### Pending Status and Enable History

A unit's tamper_switch status will only change once it makes an RC-GET connection to the SMARTSolar API and retrieves its new status. Until the RC-GET is complete the unit's actual status is unchanged. To reflect this the unit is placed in a "pending" state. The pending state therefore means that the tamper switch has been enabled (or disabled) but has not yet connected to the system to update its status.

For example:

* A unit has its tamper switch OFF (disabled).
* A technician chooses to enable the tamper_switch, the unit then moves to "pending enabled" and the switch is still off.
* The unit remains in "pending enabled" until a connection is made.
* A connection is made - the unit receives its new status and is moved to enabled, the tamper_switch is now ON

### The <a href="/#tamper-enable-history">`tamper_enable_history`</a> table

The changes above are tracked in the <a href="/#tamper-enable-history">`tamper_enable_history`</a> table. Each time a unit has a change of state this is recorded in the
<a href="/#tamper-enable-history">`tamper_enable_history`</a> table, along with the user who caused the change.

