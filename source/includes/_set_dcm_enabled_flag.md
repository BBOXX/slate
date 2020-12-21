## `/products/<imei>/set_dcm_enabled_flag`

> A `PUT` request to this endpoint sets the value of a unit's DCM Enabled Flag.

```python
    url = "https://smartapi.bboxx.co.uk/v1/products/000000000000/set_dcm_enabled_flag"
    data = json.dumps({"enabled": true})
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=' + A_VALID_TOKEN}

    r = requests.put(url=url, headers=headers)

    print r.json()
    >>> {
            "status": "success",
            "message": "Product 000000000000000. DCM Enabled Flag set to True"
            "data": {}
    }
```

This endpoint sets the DCM Enabled flag of a unit. The imei of the unit is specified in the url.

    | value 
---:|:------
__endpoint__ | `/products/<imei>/set_dcm_enabled_flag`
__method__ | `PUT`
__url_params__ | `product_imei` _(str)_
__payload__ | `{"enabled": <status>}`
__response__ | 200

### Status
The body of the `PUT` should be a valid boolean value: true or false.
