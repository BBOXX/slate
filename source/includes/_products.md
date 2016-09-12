## <u>Product</u>
This description is not yet complete it should be filled in!


### <u>The product object</u>

Field | Description
------:|:------------
__product_imei__ <br><font color="DarkGray">_varchar(15)_</font> <font color="Crimson">__(primary key)__</font> |
__modified_by__ <br><font color="DarkGray">_string_</font> <font color="Crimson"></font> |
__analysis_timestamp__ <br><font color="DarkGray">_datetime_</font> <font color="Crimson"></font> |
__capacity_limit__ <br><font color="DarkGray">_string_</font> <font color="Crimson">(not-null)</font> |
__current_enable_flag__ <br><font color="DarkGray">_boolean_</font> <font color="Crimson">(not-null)</font> |
__desired_enable_flag__ <br><font color="DarkGray">_boolean_</font> <font color="Crimson">(not-null)</font> |
__current_tamper_flag__ <br><font color="DarkGray">_boolean_</font> <font color="Crimson">(not-null)</font> |
__desired_tamper_flag__ <br><font color="DarkGray">_boolean_</font> <font color="Crimson">(not-null)</font> |
__device_key__ <br><font color="DarkGray">_unknown-type_</font> <font color="Crimson">(unique)</font> |
__<a href="/#hub">hub_id</a>__ <br><font color="DarkGray">_int_</font> <font color="Crimson">(foreign-key)</font> |
__imsi__ <br><font color="DarkGray">_varchar(15)_</font> <font color="Crimson">(not-null,unique)</font> |
__<a href="/#connection">latest_connection_id</a>__ <br><font color="DarkGray">_int_</font> <font color="Crimson">(foreign-key)</font> |
__<a href="/#connection">latest_connection_location_id</a>__ <br><font color="DarkGray">_int_</font> <font color="Crimson">(foreign-key)</font> |
__<a href="/#state">latest_state_id</a>__ <br><font color="DarkGray">_int_</font> <font color="Crimson">(foreign-key)</font> |
__<a href="/#product-type">product_type_id</a>__ <br><font color="DarkGray">_int_</font> <font color="Crimson">(not-null,foreign-key)</font> |
__serial_number__ <br><font color="DarkGray">_string_</font> <font color="Crimson">(not-null,unique)</font> |
__<a href="/#shop">shop_id</a>__ <br><font color="DarkGray">_int_</font> <font color="Crimson">(foreign-key)</font> |
__<a href="/#products-lt-imei-gt-lock_software">software_lock</a>__ <br><font color="DarkGray">_int_</font> <font color="Crimson">(foreign-key)</font> |
__created_at__  <br><font color="DarkGray">_datetime_</font> | timestamp that the record was created at
__created_by__  <br><font color="DarkGray">_text_</font>| username of the user who created the record
__modified_at__ <br><font color="DarkGray">_datetime_</font>| timestamp that the record was last modified


<br>

Relationship | Description
-------------:|:------------
__alerts__ | The associated <a href="/#alert">`alerts`</a>
__anomalies__ | The associated <a href="/#anomaly">`anomalies`</a>
__connections__ | The associated <a href="/#connection">`connections`</a>
__customer_product_history__ | The associated <a href="/#customer-product-history">`customer_product_history`</a>
__notes__ | The associated notes
__part_product_linker__ | The associated <a href="/#part-product-linker">`part_product_linker`</a>
__product_entity_linker__ | The associated <a href="/#product-entity-linker">`product_entity_linker`</a>
__product_software_linker__ | The associated <a href="/#product-software-linker">`product_software_linker`</a>
__enable_history_rel__ | The associated <a href="/#enable-history-rel">`enable_history_rel`</a>
__repairs__ | The associated <a href="/#repair">`repairs`</a>
__sms_history__ | The associated <a href="/#sms-history">`sms_history`</a>
__states__ | The associated <a href="/#state">`states`</a>
__tamper_enable_history__ | The associated <a href="/#tamper-enable-history">`tamper_enable_history`</a>


<hr>
<br>

> `POST` requests are not allowed at this endpoint

> We can retrieve the `product` created by specifying its `product_imei` in the request url:

```python
    url = 'http://smartapi.bboxx.co.uk/v1/products/1'
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=' + A_VALID_TOKEN}

    r = requests.get(url=url, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"product_imei": 1
		"analysis_timestamp": "2000-01-01 00:00:00",
		"capacity_limit": "test",
		"current_enable_flag": True,
		"desired_enable_flag": True,
		"current_tamper_flag": True,
		"desired_tamper_flag": True,
		"device_key": Unknown column type,
		"hub_id": 1,
		"imsi": "000000000000000",
		"latest_connection_id": 1,
		"latest_connection_location_id": 1,
		"latest_state_id": 1,
		"product_type_id": 1,
		"serial_number": "test",
		"shop_id": 1,
		"software_lock": 1,
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": None
	}
```

> We can retrieve all `products` by omitting the `product_imei`:

```python
    url = 'http://smartapi.bboxx.co.uk/v1/products'
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=' + A_VALID_TOKEN}

    r = requests.get(url=url, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
        u'total_pages': 1,
        u'objects': [
            {<record>},
            {<record>},
            {<record>},
            {<record>},
            {<record>},
        ],
        u'num_results': 10,
        u'page': 1
    }
```

> We can edit the newly created `product` with a `PUT` request:

```python
    url = 'http://smartapi.bboxx.co.uk/v1/products/1'
    data = json.dumps({
		"analysis_timestamp": "2016-07-01 12:34:45",
		"capacity_limit": "changed",
		"current_enable_flag": False,
		"desired_enable_flag": False,
		"current_tamper_flag": False,
		"desired_tamper_flag": False,
		"device_key": Unknown column type,
		"hub_id": 2,
		"imsi": "999999999999999",                # unique
		"latest_connection_id": 2,
		"latest_connection_location_id": 2,
		"latest_state_id": 2,
		"product_type_id": 2,
		"serial_number": "changed",               # unique
		"shop_id": 2,
		"software_lock": 2,
		})
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=' + A_VALID_TOKEN}

    r = requests.put(url=url, data=data, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"product_imei": 1
		"modified_by": "changed",
		"analysis_timestamp": "2016-07-01 12:34:45",
		"capacity_limit": "changed",
		"current_enable_flag": False,
		"desired_enable_flag": False,
		"current_tamper_flag": False,
		"desired_tamper_flag": False,
		"device_key": Unknown column type,
		"hub_id": 2,
		"imsi": "999999999999999",
		"latest_connection_id": 2,
		"latest_connection_location_id": 2,
		"latest_state_id": 2,
		"product_type_id": 2,
		"serial_number": "changed",
		"shop_id": 2,
		"software_lock": 2,
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": 2016-07-07 12:34:45
	}
```
> Note that the `modified_at` field has been updated accordingly.

> If a user has `SYSTEM` permissions they can delete the `product`

```python
    url = 'http://smartapi.bboxx.co.uk/v1/products/1'
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=' + A_VALID_TOKEN}

    r = requests.delete(url=url, headers=headers)

    r
    >>> <Response 204>

    r.text
    >>>
```
> Note that the response from a 204 request is empty. This means that `r.json()` cannot be called and will throw a JSONDecodeError. In fact the response is `u''` - an empty unicode string.



### POST
`POST` requests are not allowed at this endpoint

### GET
     | value
 ----:|:---
endpoint | `/v1/['table_name_plural']` or `/v1/['table_name_plural']/<['pk_name']>`
method | `GET`
url_params | `['pk_name']` <font color="DarkGray">_(['pk_type'])_</font>
query params | *> See Query Format and Filtering*
body | <font color="DarkGray">N/A</font>
permissions | <font color="Jade">__`OVERVIEW`__</font>
response | `200`

### PUT
     | value
 ----:|:---
endpoint | `/v1/products/<product_imei>`
method | `PUT`
url_params | `product_imei` of the product you wish to edit
query params | <font color="DarkGray">N/A</font>
body | JSON-formatted dictionary of the columns that you wish to alter
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `200`

### DELETE
     | value
 ----:|:---
endpoint | `/v1/products/<product_imei>`
method | `DELETE`
url_params | `product_imei` <font color="DarkGray">_(varchar(15))_</font>
query params | <font color="DarkGray">N/A</font>
body | <font color="DarkGray">N/A</font>
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `204`


