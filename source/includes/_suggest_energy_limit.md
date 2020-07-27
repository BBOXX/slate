##`/products/<imei>/suggest_energy_limit`

### Description

<<<<<<< Updated upstream
The energy_limit is restricted by the energy_limit_cap, if it is set.
Requests will be accepted and the energy_limit truncated if the requested
limit is higher than the cap.
=======
This endpoint is used to 'suggest' an energy limit.

The energy limit is the number of Watt Hours (WH) of energy that we expect to receive from the battery. Previously api users could ultilise the `v1/product-parameter` endpoint to set the `energy_limit` parameter on BBOXX Home (bPower50) products. To calculate the correct energy limit to set on a product, we would take an energy allowance for each appliance that the customer has and sum these energy allowances to get a total daily energy limit value. If this limit was reached, we would turn off the outputs.

There are now several changes which impact how this parameter can be set.

##Energy Limit Cap

To prevent mis-use there is a second parameter, `energy_limit_cap`,  which caps the value of the energy_limit. This allows us to restrict the energy_limit using default values per NGU.

If a user attempts to set an energy_limit higher than the energy_limit_cap their request will be accepted, but the energy_limit will be truncated to the value of the cap. The energy_limit_cap is determined on a per-battery basis and cannot be altered manually.

#Default Energy Limits

As the unit moves through it's LifeCycle it will enter various Product Life Cycle States, and each time a unit moves between any life-cycle state, SMARTSolar will determine the correct `energy_limit` and `energy_limit_cap` for that battery and state and then apply them to the unit. These default `energy_limits` are stored in the DefaultEnergyLimit table.

#Getting and Setting the energy_limit_cap
The energy_limit_cap is a Parameter, so it can be queried in the usual way from `/products/<imei>/parameters` or from `/product_parameters` with appropriate filters.

`energy_limit_cap` is a 'setting'. This means it does not get sync'ed to the unit and therefore can only have status of active or removed. For more details on getting and setting Parameters see: Parameters

The energy_limit_cap cannot be altered by external users. If a battery is found to have the wrong energy_limit_cap then the default cap for the battery can be altered by request to the support team. This will change the default energy_limit_cap for ALL units with that type of batteries.

NGUs/Entities may also request an override cap by request to the support team. When a unit moves into a new state SMARTSolar will first look for any entity-level overrides, for that battery in that state. If no overrides are found, SMARTSolar will apply the default `energy_limit` and `energy_limit_cap` from the DefaultEnergyLimit table mentioned above.

##Total accessory energy

A unit in the MONITORED state can be given a `total_accessory_energy` value. SMARTSolar will take this value and determine the correct `energy_limit` to set on the unit. This energy_limit will still be capped by the energy_limit_cap for the unit.

Once total_accessory_energy has been set, the energy_limit parameter can no-longer be set directly. The total_accessory_energy value must be removed before any user can set the energy_limit again. The total_accessory_energy can be removed using the `/remove_total_accessory_energy` endpoint.

`total_accessory_energy` will be removed as soon as a unit moves out of the MONITORED state.

##Errors and Restrictions

SMARTSolar will throw errors if:

No valid battery part is attached to the unit.
There is a valid battery but it has no default limit or cap set.
There are multiple entity-level overrides present for that battery/unit. (units can belong to multiple entities)
Since the energy_limit and energy_limit_cap are set on EVERY state transition this means that a unit without a valid battery will be blocked from proceeding through any LifeCycle State.

*NOTE* There is no global default `energy_limit` or `energy_limit_cap`.

If the battery does not have a valid `default_energy_limit` or `energy_limit_cap` set for the required state then the unit will not be able to move into that state.

Currently, the unit must also be in either: `ACTIVATED`, `MONITORED` or `IN_REPAIR_SYSTEM` to suggest an energy limit.

----
##Setting the energy_limit

Requests will be accepted and the energy_limit truncated if the requested limit is higher than the cap.
The endpoint will inform the user of the requested and applied limit, the
energy_limit_cap and explicitly state whether the requested limit has been
truncated.

### Endpoint

To suggest an energy limit on a <a href=/#product>`Product`</a>  with a given imei make a `PUT` request to `/products/<imei>/suggest_energy_limit`.

Energy limits are passed in as strings.

`data = json.dumps({"energy_limit": "<suggested_energy_limit>"})`

    | value
---:|:------
__endpoint__ | `/products/<imei>/suggest_energy_limit`
__method__ | `PUT`
__url_params__ | `product_imei`  <font color="DarkGray">_(str)_</font>
__response__ | 200
__payload__ | date <font color="DarkGray">_(optional)_</font>
__permissions__ | `TECHNICAL`


```python
    data = {"energy_limit": "<energy_limit>"}
    endpoint = "/products/{}/suggest_energy_limit".format(imei)
    r = self.put(endpoint, data=data, user=user, expected_response=expected_response)

    print(r.json())

    >>>{
        "status": "success",
        "message": message,
        "data": {
            "requested": requested_limit,
            "applied": applied_limit,
            "max_energy_limit": max_energy_limit,
            "min_energy_limit": min_energy_limit,
            "bounded": bounded
        } 200
    }


```