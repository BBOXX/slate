## <u>Product Type</u>
This description is not yet complete it should be filled in!


### <u>The product_type object</u>

Field | Description
------:|:------------
__product_type_id__ <br><font color="DarkGray">_int_</font> <font color="Crimson">__(primary key)__</font> | A unique integer identifier for each product_type.
__modified_by__ <br><font color="DarkGray">_string_</font> <font color="Crimson"></font> |
__name__ <br><font color="DarkGray">_string_</font> <font color="Crimson">(not-null,unique)</font> |
__erp_code__ <br><font color="DarkGray">_varchar(6)_</font> <font color="Crimson"></font> |
__parameter_types__ <br><font color="DarkGray">_unknown-type_</font> <font color="Crimson"></font> |
__created_at__  <br><font color="DarkGray">_datetime_</font> | timestamp that the record was created at
__created_by__  <br><font color="DarkGray">_text_</font>| username of the user who created the record
__modified_at__ <br><font color="DarkGray">_datetime_</font>| timestamp that the record was last modified


<br>

Relationship | Description
-------------:|:------------
__products__ | The associated <a href="/#product">`products`</a>
__alert_type_product_type_linker__ | The associated <a href="/#part-type-product-type-linker">`alert_type_product_type_linker`</a>
__anomaly_type_product_type_linker__ | The associated <a href="/#anomaly-type-product-type-linker">`anomaly_type_product_type_linker`</a>
__part_type_product_type_linker__ | The associated <a href="/#part-type-product-type-linker">`part_type_product_type_linker`</a>
__product_type_software_version_type_linker__ | The associated <a href="/#product-type-software-version-type-linker">`product_type_software_version_type_linker`</a>
__symptom_type_product_type_linker__ | The associated <a href="/#symptom-type-product-type-linker">`symptom_type_product_type_linker`</a>
__latest_software__ | The associated <a href="/#latest-software">`latest_software`</a>


<hr>
<br>

> An example POST request. Note that `product_type_id`, `created_at`, `modified_at` and `created_by` are all handled internally by the system and need not be explicitly specified. See Meta Data for more information.

```python
    url = "http://smartapi.bboxx.co.uk/v1/product_types"
    data = json.dumps({
		"name": "test",                       # unique
		"erp_code": "XX0001",
		"parameter_types": Unknown column type,
		})
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=' + A_VALID_TOKEN}

    r = requests.post(url=url, data=data, headers=headers)

    r
    >>> <Response 201>

    r.json()

    >>> {
		"product_type_id": 1
		"modified_by": "test",
		"name": "test",
		"erp_code": "XX0001",
		"parameter_types": Unknown column type,
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": None
	}
```

> We can retrieve the `product_type` created by specifying its `product_type_id` in the request url:

```python
    url = 'http://smartapi.bboxx.co.uk/v1/product_types/1'
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=' + A_VALID_TOKEN}

    r = requests.get(url=url, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"product_type_id": 1
		"modified_by": "test",
		"name": "test",
		"erp_code": "XX0001",
		"parameter_types": Unknown column type,
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": None
	}
```

> We can retrieve all `product_types` by omitting the `product_type_id`:

```python
    url = 'http://smartapi.bboxx.co.uk/v1/product_types'
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

> We can edit the newly created `product_type` with a `PUT` request:

```python
    url = 'http://smartapi.bboxx.co.uk/v1/product_types'
    data = json.dumps({
		"name": "changed",                            # unique
		"erp_code": YY9999,
		"parameter_types": Unknown column type,
		})
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=' + A_VALID_TOKEN}

    r = requests.put(url=url, data=data, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"product_type_id": 1
		"modified_by": "changed",
		"name": "changed",
		"erp_code": YY9999,
		"parameter_types": Unknown column type,
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": 2016-07-07 12:34:45
	}
```
> Note that the `modified_at` field has been updated accordingly.

> If a user has `SYSTEM` permissions they can delete the `product_type`

```python
    url = 'http://smartapi.bboxx.co.uk/v1/product_types/1'
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=' + A_VALID_TOKEN}

    r = requests.delete(url=url, headers=headers)

    r
    >>> <Response 204>

    r.text
    >>>
```
> Note that the response from a 204 request is empty. This means that `r.json()` cannot be called and will throw a JSONDecodeError. In fact the response is `u''` - an empty unicode string.



### POST
     | value
 ----:|:---
endpoint | `/v1/['table_name_plural']`
method | `POST`
url_params | <font color="DarkGray">N/A</font>
query params | <font color="DarkGray">N/A</font>
body | JSON-formatted dictionary with the details of the `['table_name_singular']` that you wish to create
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `201`

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
endpoint | `/v1/product_types/<product_type_id>`
method | `PUT`
url_params | `product_type_id` of the product_type you wish to edit
query params | <font color="DarkGray">N/A</font>
body | JSON-formatted dictionary of the columns that you wish to alter
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `200`

### DELETE
     | value
 ----:|:---
endpoint | `/v1/product_types/<product_type_id>`
method | `DELETE`
url_params | `product_type_id` <font color="DarkGray">_(int)_</font>
query params | <font color="DarkGray">N/A</font>
body | <font color="DarkGray">N/A</font>
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `204`


