## <u>Product Entity Linker</u>
This description is not yet complete it should be filled in!


### <u>The product_entity_linker object</u>

Field | Description
------:|:------------
__product_entity_linker_id__ <br><font color="DarkGray">_int_</font> <font color="Crimson">__(primary key)__</font> | A unique integer identifier for each product_entity_linker.
__<a href="/#product">product_imei</a>__ <br><font color="DarkGray">_varchar(15)_</font> <font color="Crimson">(not-null,foreign-key)</font> | 
__<a href="/#entity">entity_id</a>__ <br><font color="DarkGray">_int_</font> <font color="Crimson">(not-null,foreign-key)</font> | 
__date_added__ <br><font color="DarkGray">_datetime_</font> <font color="Crimson"></font> | 
__date_removed__ <br><font color="DarkGray">_datetime_</font> <font color="Crimson"></font> | 
__created_at__  <br><font color="DarkGray">_datetime_</font> | timestamp that the record was created at
__created_by__  <br><font color="DarkGray">_text_</font>| username of the user who created the record
__modified_at__ <br><font color="DarkGray">_datetime_</font>| timestamp that the record was last modified


<br>

Relationship | Description
-------------:|:------------
<font color="DarkGray">N/A</font> | <font color="DarkGray">_There are no relatioships for this table._</font>

<hr>
<br>

> An example POST request. Note that product_entity_linker_id, created_at, modified_at and created_by are all handled internally by the system and need not be explicitly specified. See Meta Data for more information.

```python
    url = "http://smartapi.bboxx.co.uk/v1/product_entity_linker"
    data = json.dumps({
		"product_imei": "000000000000000",
		"entity_id": 1,
		"date_added": "2000-01-01 00:00:00",
		"date_removed": "2000-01-01 00:00:00",
		})
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=' + <valid_token>}

    r = requests.post(url=url, data=data, headers=headers)

    r
    >>> <Response 201>

    r.json()

    >>> {
		"product_entity_linker_id": 1
		"product_imei": "000000000000000",
		"entity_id": 1,
		"date_added": "2000-01-01 00:00:00",
		"date_removed": "2000-01-01 00:00:00",
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": None
	}
```

> We can retrieve the `product_entity_linker` created by specifying its `product_entity_linker_id` in the request url:

```python
    url = 'http://smartapi.bboxx.co.uk/v1/product_entity_linker/1'
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=' + <valid_token>}

    r = requests.get(url=url, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"product_entity_linker_id": 1
		"product_imei": "000000000000000",
		"entity_id": 1,
		"date_added": "2000-01-01 00:00:00",
		"date_removed": "2000-01-01 00:00:00",
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": None
	}
```

> and we can retrieve all product_entity_linker by omitted the product_entity_linker_id:

```python
    url = 'http://smartapi.bboxx.co.uk/v1/product_entity_linker'
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=' + <valid_token>}

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

> We can edit the newly created product_entity_linker with a `PUT` request:

```python
    url = 'http://smartapi.bboxx.co.uk/v1/product_entity_linker'
    data = json.dumps({
		"product_imei": "999999999999999",
		"entity_id": 2,
		"date_added": "2016-07-01 12:34:45",
		"date_removed": "2016-07-01 12:34:45",
		})
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=' + <valid_token>}

    r = requests.post(url=url, data=data, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"product_entity_linker_id": 1
		"product_imei": "999999999999999",
		"entity_id": 2,
		"date_added": "2016-07-01 12:34:45",
		"date_removed": "2016-07-01 12:34:45",
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": 2016-07-07 12:34:45
	}
```
> Note that the `modified_at` field has been updated accordingly.

> If a user has `SYSTEM` permissions they can delete the product_entity_linker

```python
    url = 'http://smartapi.bboxx.co.uk/v1/product_entity_linker/1'
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=' + <valid_token>}

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
endpoint | `/v1/product_entity_linker`
method | `POST`
url_params | <font color="DarkGray">N/A</font>
query params | <font color="DarkGray">N/A</font>
body | JSON-formatted dictionary with the details of the `product_entity_linker` that you wish to create
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `201`

### GET
     | value
 ----:|:---
endpoint | `/v1/product_entity_linker` or `/v1/product_entity_linker/<product_entity_linker_id>`
method | `GET`
url_params | `product_entity_linker_id` <font color="DarkGray">_(int)_</font>
query params | *> See Query Format and Filtering*
body | <font color="DarkGray">N/A</font>
permissions | <font color="Jade">__`OVERVIEW`__</font>
response | `200`

### PUT
     | value
 ----:|:---
endpoint | `/v1/product_entity_linker/<product_entity_linker_id>`
method | `PUT`
url_params | `product_entity_linker_id` of the product_entity_linker you wish to edit
query params | <font color="DarkGray">N/A</font>
body | JSON-formatted dictionary of the columns that you wish to alter
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `200`

### DELETE
     | value
 ----:|:---
endpoint | `/v1/product_entity_linker/<product_entity_linker_id>`
method | `DELETE`
url_params | `product_entity_linker_id` <font color="DarkGray">_(int)_</font>
query params | <font color="DarkGray">N/A</font>
body | <font color="DarkGray">N/A</font>
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `204`
    