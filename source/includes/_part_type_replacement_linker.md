## <u>Part Type Replacement Linker</u>
Specifies which parts can replace which other parts.This table can be used to generate list of possible parts for each product_type.


### <u>The part_type_replacement_linker object</u>

Field | Description
------:|:------------
__part_type_replacement_linker_id__ <br><font color="DarkGray">_int_</font> <font color="Crimson">__(primary key)__</font> | A unique integer identifier for each part_type_replacement_linker.
__<a href="/#product-type">product_type_id</a>__ <br><font color="DarkGray">_int_</font> <font color="Crimson">(foreign-key)</font> | 
__<a href="/#existing-part-type">existing_part_type_id</a>__ <br><font color="DarkGray">_int_</font> <font color="Crimson">(not-null,foreign-key)</font> | 
__<a href="/#replacement-part-type">replacement_part_type_id</a>__ <br><font color="DarkGray">_int_</font> <font color="Crimson">(not-null,foreign-key)</font> | 
__default_part_type__ <br><font color="DarkGray">_boolean_</font> <font color="Crimson">(not-null)</font> | 
__critical_part_type__ <br><font color="DarkGray">_boolean_</font> <font color="Crimson">(not-null)</font> | 
__non_transferable__ <br><font color="DarkGray">_boolean_</font> <font color="Crimson">(not-null)</font> | 
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

> An example POST request. Note that `part_type_replacement_linker_id`, `created_at`, `modified_at` and `created_by` are all handled internally by the system and need not be explicitly specified. See Meta Data for more information.

```python
    url = "https://smartapi.bboxx.co.uk/v1/part_type_replacement_linker"
    data = json.dumps({
		"product_type_id": 1,
		"existing_part_type_id": 1,
		"replacement_part_type_id": 1,
		"default_part_type": True,
		"critical_part_type": True,
		"non_transferable": True,
		})
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.post(url=url, data=data, headers=headers)

    r
    >>> <Response 201>

    r.json()

    >>> {
		"part_type_replacement_linker_id": 1
		"product_type_id": 1,
		"existing_part_type_id": 1,
		"replacement_part_type_id": 1,
		"default_part_type": True,
		"critical_part_type": True,
		"non_transferable": True,
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": None
	}
```

> We can retrieve the `part_type_replacement_linker` created by specifying its `part_type_replacement_linker_id` in the request url:

```python
    url = 'https://smartapi.bboxx.co.uk/v1/part_type_replacement_linker/1'
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.get(url=url, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"part_type_replacement_linker_id": 1
		"product_type_id": 1,
		"existing_part_type_id": 1,
		"replacement_part_type_id": 1,
		"default_part_type": True,
		"critical_part_type": True,
		"non_transferable": True,
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": None
	}
```

> We can retrieve all `part_type_replacement_linker` by omitting the `part_type_replacement_linker_id`:

```python
    url = 'https://smartapi.bboxx.co.uk/v1/part_type_replacement_linker'
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

> We can edit the newly created `part_type_replacement_linker` with a `PUT` request:

```python
    url = 'https://smartapi.bboxx.co.uk/v1/part_type_replacement_linker/1'
    data = json.dumps({
		"product_type_id": 2,
		"existing_part_type_id": 2,
		"replacement_part_type_id": 2,
		"default_part_type": False,
		"critical_part_type": False,
		"non_transferable": False,
		})
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.put(url=url, data=data, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"part_type_replacement_linker_id": 1
		"product_type_id": 2,
		"existing_part_type_id": 2,
		"replacement_part_type_id": 2,
		"default_part_type": False,
		"critical_part_type": False,
		"non_transferable": False,
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": 2016-07-07 12:34:45
	}
```
> Note that the `modified_at` field has been updated accordingly.

> If a user has `SYSTEM` permissions they can delete the `part_type_replacement_linker`

```python
    url = 'https://smartapi.bboxx.co.uk/v1/part_type_replacement_linker/1'
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
endpoint | `/v1/part_type_replacement_linker`
method | `POST`
url_params | <font color="DarkGray">N/A</font>
query params | <font color="DarkGray">N/A</font>
body | JSON-formatted dictionary with the details of the `part_type_replacement_linker` that you wish to create
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `201`

### GET
     | value
 ----:|:---
endpoint | `/v1/part_type_replacement_linker` or `/v1/part_type_replacement_linker/<part_type_replacement_linker_id>`
method | `GET`
url_params | `part_type_replacement_linker_id` <font color="DarkGray">_(int)_</font>
query params | *> See Query Format and Filtering*
body | <font color="DarkGray">N/A</font>
permissions | <font color="Jade">__`OVERVIEW`__</font>
response | `200`

### PUT
     | value
 ----:|:---
endpoint | `/v1/part_type_replacement_linker/<part_type_replacement_linker_id>`
method | `PUT`
url_params | `part_type_replacement_linker_id` of the part_type_replacement_linker you wish to edit
query params | <font color="DarkGray">N/A</font>
body | JSON-formatted dictionary of the columns that you wish to alter
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `200`

### DELETE
     | value
 ----:|:---
endpoint | `/v1/part_type_replacement_linker/<part_type_replacement_linker_id>`
method | `DELETE`
url_params | `part_type_replacement_linker_id` <font color="DarkGray">_(int)_</font>
query params | <font color="DarkGray">N/A</font>
body | <font color="DarkGray">N/A</font>
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `204`

    