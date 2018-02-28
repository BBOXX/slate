## <u>Product Software Linker</u>
Specifies which software-version-type is currently on each product.


### <u>The product_software_linker object</u>

Field | Description
------:|:------------
__product_software_linker_id__ <br><font color="DarkGray">_int_</font> <font color="Crimson">__(primary key)__</font> | A unique integer identifier for each product_software_linker.
__<a href="/#product">product_imei</a>__ <br><font color="DarkGray">_varchar(15)_</font> <font color="Crimson">(not-null,foreign-key)</font> | 
__<a href="/#software-version-type">software_version_type_id</a>__ <br><font color="DarkGray">_int_</font> <font color="Crimson">(not-null,foreign-key)</font> | 
__date_added__ <br><font color="DarkGray">_datetime_</font> <font color="Crimson"></font> | 
__date_removed__ <br><font color="DarkGray">_datetime_</font> <font color="Crimson"></font> | 
__update_attempts__ <br><font color="DarkGray">_int_</font> <font color="Crimson"></font> | 
__created_at__  <br><font color="DarkGray">_datetime_</font> | timestamp that the record was created at
__created_by__  <br><font color="DarkGray">_text_</font>| username of the user who created the record
__modified_at__ <br><font color="DarkGray">_datetime_</font>| timestamp that the record was last modified
__modified_by__ <br><font color="DarkGray">_text_</font>| user that last modified the record

<br>

Relationship | Description
-------------:|:------------
<font color="DarkGray">N/A</font> | <font color="DarkGray">_There are no relationships for this table._</font>

<hr>
<br>

> An example POST request. Note that `product_software_linker_id`, `created_at`, `modified_at` and `created_by` are all handled internally by the system and need not be explicitly specified. See Meta Data for more information.

```python
    url = "https://smartapi.bboxx.co.uk/v1/product_software_linker"
    data = json.dumps({
		"product_imei": "000000000000000",
		"software_version_type_id": 1,
		"date_added": "2000-01-01 00:00:00",
		"date_removed": "2000-01-01 00:00:00",
		"update_attempts": 1,
		})
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.post(url=url, data=data, headers=headers)

    r
    >>> <Response 201>

    r.json()

    >>> {
		"product_software_linker_id": 1
		"product_imei": "000000000000000",
		"software_version_type_id": 1,
		"date_added": "2000-01-01 00:00:00",
		"date_removed": "2000-01-01 00:00:00",
		"update_attempts": 1,
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": None
	}
```

    > We can retrieve the `product_software_linker` created by specifying its `product_software_linker_id` in the request url:

```python
    url = 'https://smartapi.bboxx.co.uk/v1/product_software_linker/1'
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.get(url=url, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"product_software_linker_id": 1
		"product_imei": "000000000000000",
		"software_version_type_id": 1,
		"date_added": "2000-01-01 00:00:00",
		"date_removed": "2000-01-01 00:00:00",
		"update_attempts": 1,
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": None
	}
```

> We can retrieve all `product_software_linker` by omitting the `product_software_linker_id`:

```python
    url = 'https://smartapi.bboxx.co.uk/v1/product_software_linker'
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

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

> We can edit the newly created `product_software_linker` with a `PUT` request:

```python
    url = 'https://smartapi.bboxx.co.uk/v1/product_software_linker/1'
    data = json.dumps({
		"product_imei": "999999999999999",
		"software_version_type_id": 2,
		"date_added": "2016-07-01 12:34:45",
		"date_removed": "2016-07-01 12:34:45",
		"update_attempts": 2,
		})
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.put(url=url, data=data, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"product_software_linker_id": 1
		"product_imei": "999999999999999",
		"software_version_type_id": 2,
		"date_added": "2016-07-01 12:34:45",
		"date_removed": "2016-07-01 12:34:45",
		"update_attempts": 2,
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": 2016-07-07 12:34:45
	}
```
> Note that the `modified_at` field has been updated accordingly.

> If a user has `SYSTEM` permissions they can delete the `product_software_linker`

```python
    url = 'https://smartapi.bboxx.co.uk/v1/product_software_linker/1'
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

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
endpoint | `/v1/product_software_linker`
method | `POST`
url_params | <font color="DarkGray">N/A</font>
query params | <font color="DarkGray">N/A</font>
body | JSON-formatted dictionary with the details of the `product_software_linker` that you wish to create
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `201`

### GET
     | value
 ----:|:---
endpoint | `/v1/product_software_linker` or `/v1/product_software_linker/<product_software_linker_id>`
method | `GET`
url_params | `product_software_linker_id` <font color="DarkGray">_(int)_</font>
query params | *> See Query Format and Filtering*
body | <font color="DarkGray">N/A</font>
permissions | <font color="Jade">__`OVERVIEW`__</font>
response | `200`

### PUT
     | value
 ----:|:---
endpoint | `/v1/product_software_linker/<product_software_linker_id>`
method | `PUT`
url_params | `product_software_linker_id` of the product_software_linker you wish to edit
query params | <font color="DarkGray">N/A</font>
body | JSON-formatted dictionary of the columns that you wish to alter
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `200`

### DELETE
     | value
 ----:|:---
endpoint | `/v1/product_software_linker/<product_software_linker_id>`
method | `DELETE`
url_params | `product_software_linker_id` <font color="DarkGray">_(int)_</font>
query params | <font color="DarkGray">N/A</font>
body | <font color="DarkGray">N/A</font>
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `204`

    