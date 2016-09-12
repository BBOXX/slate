## <u>Alert Type Product Type Linker</u>
This description is not yet complete it should be filled in!


### <u>The alert_type_product_type_linker object</u>

Field | Description
------:|:------------
__alert_type_product_type_linker_id__ <br><font color="DarkGray">_int_</font> <font color="Crimson">__(primary key)__</font> | A unique integer identifier for each alert_type_product_type_linker.
__modified_by__ <br><font color="DarkGray">_string_</font> <font color="Crimson"></font> |
__<a href="/#alert-type">alert_type_id</a>__ <br><font color="DarkGray">_int_</font> <font color="Crimson">(not-null,foreign-key)</font> |
__<a href="/#product-type">product_type_id</a>__ <br><font color="DarkGray">_int_</font> <font color="Crimson">(not-null,foreign-key)</font> |
__created_at__  <br><font color="DarkGray">_datetime_</font> | timestamp that the record was created at
__created_by__  <br><font color="DarkGray">_text_</font>| username of the user who created the record
__modified_at__ <br><font color="DarkGray">_datetime_</font>| timestamp that the record was last modified


<br>

Relationship | Description
-------------:|:------------
<font color="DarkGray">N/A</font> | <font color="DarkGray">_There are no relationships for this table._</font>

<hr>
<br>

> An example POST request. Note that `alert_type_product_type_linker_id`, `created_at`, `modified_at` and `created_by` are all handled internally by the system and need not be explicitly specified. See Meta Data for more information.

```python
    url = "http://smartapi.bboxx.co.uk/v1/alert_type_product_type_linker"
    data = json.dumps({
		"alert_type_id": 1,                   # look up alert type IDs using GET: alert type
		"product_type_id": 1,                 # look up product type IDs using GET: product type
		})
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=' + A_VALID_TOKEN}

    r = requests.post(url=url, data=data, headers=headers)

    r
    >>> <Response 201>

    r.json()

    >>> {
		"alert_type_product_type_linker_id": 1
		"modified_by": "test",
		"alert_type_id": 1,
		"product_type_id": 1,
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": None
	}
```

> We can retrieve the `alert_type_product_type_linker` created by specifying its `alert_type_product_type_linker_id` in the request url:

```python
    url = 'http://smartapi.bboxx.co.uk/v1/alert_type_product_type_linker/1'
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=' + A_VALID_TOKEN}

    r = requests.get(url=url, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"alert_type_product_type_linker_id": 1
		"modified_by": "test",
		"alert_type_id": 1,
		"product_type_id": 1,
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": None
	}
```

> We can retrieve all `alert_type_product_type_linker` by omitting the `alert_type_product_type_linker_id`:

```python
    url = 'http://smartapi.bboxx.co.uk/v1/alert_type_product_type_linker'
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

> We can edit the newly created `alert_type_product_type_linker` with a `PUT` request:

```python
    url = 'http://smartapi.bboxx.co.uk/v1/alert_type_product_type_linker/1'
    data = json.dumps({
		"alert_type_id": 2,                   # look up alert type IDs using GET: alert type
		"product_type_id": 2,                 # look up product type IDs using GET: product type
		})
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=' + A_VALID_TOKEN}

    r = requests.put(url=url, data=data, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"alert_type_product_type_linker_id": 1
		"modified_by": "changed",
		"alert_type_id": 2,
		"product_type_id": 2,
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": 2016-07-07 12:34:45
	}
```
> Note that the `modified_at` field has been updated accordingly.

> If a user has `SYSTEM` permissions they can delete the `alert_type_product_type_linker`

```python
    url = 'http://smartapi.bboxx.co.uk/v1/alert_type_product_type_linker/1'
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
endpoint | `/v1/alert_type_product_type_linker/<alert_type_product_type_linker_id>`
method | `PUT`
url_params | `alert_type_product_type_linker_id` of the alert_type_product_type_linker you wish to edit
query params | <font color="DarkGray">N/A</font>
body | JSON-formatted dictionary of the columns that you wish to alter
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `200`

### DELETE
     | value
 ----:|:---
endpoint | `/v1/alert_type_product_type_linker/<alert_type_product_type_linker_id>`
method | `DELETE`
url_params | `alert_type_product_type_linker_id` <font color="DarkGray">_(int)_</font>
query params | <font color="DarkGray">N/A</font>
body | <font color="DarkGray">N/A</font>
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `204`


