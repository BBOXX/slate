## <u>Part</u>
Contains details of all of the parts in each BBOXX product.


### <u>The part object</u>

Field | Description
------:|:------------
__part_id__ <br><font color="DarkGray">_int_</font> <font color="Crimson">__(primary key)__</font> | A unique integer identifier for each part.
__serial_number__ <br><font color="DarkGray">_string_</font> <font color="Crimson">(unique)</font> | 
__<a href="/#part-type">part_type_id</a>__ <br><font color="DarkGray">_int_</font> <font color="Crimson">(not-null,foreign-key)</font> | 
__properties__ <br><font color="DarkGray">_unknown-type_</font> <font color="Crimson"></font> | 
__manufacturer__ <br><font color="DarkGray">_string_</font> <font color="Crimson"></font> | 
__created_at__  <br><font color="DarkGray">_datetime_</font> | timestamp that the record was created at
__created_by__  <br><font color="DarkGray">_text_</font>| username of the user who created the record
__modified_at__ <br><font color="DarkGray">_datetime_</font>| timestamp that the record was last modified
__modified_by__ <br><font color="DarkGray">_text_</font>| user that last modified the record

<br>

Relationship | Description
-------------:|:------------
__part_product_linker__ | The associated part_product_linker


<hr>
<br>

> An example POST request. Note that `part_id`, `created_at`, `modified_at` and `created_by` are all handled internally by the system and need not be explicitly specified. See Meta Data for more information.

```python
    url = "https://smartapi.bboxx.co.uk/v1/parts"
    data = json.dumps({
		"serial_number": "test",
		"part_type_id": 1,
		"properties": Unknown column type,
		"manufacturer": "test",
		})
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.post(url=url, data=data, headers=headers)

    r
    >>> <Response 201>

    r.json()

    >>> {
		"part_id": 1
		"serial_number": "test",
		"part_type_id": 1,
		"properties": Unknown column type,
		"manufacturer": "test",
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": None
	}
```

> We can retrieve the `part` created by specifying its `part_id` in the request url:

```python
    url = 'https://smartapi.bboxx.co.uk/v1/parts/1'
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.get(url=url, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"part_id": 1
		"serial_number": "test",
		"part_type_id": 1,
		"properties": Unknown column type,
		"manufacturer": "test",
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": None
	}
```

> We can retrieve all `parts` by omitting the `part_id`:

```python
    url = 'https://smartapi.bboxx.co.uk/v1/parts'
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

> We can edit the newly created `part` with a `PUT` request:

```python
    url = 'https://smartapi.bboxx.co.uk/v1/parts/1'
    data = json.dumps({
		"serial_number": "changed",
		"part_type_id": 2,
		"properties": Unknown column type,
		"manufacturer": "changed",
		})
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.put(url=url, data=data, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"part_id": 1
		"serial_number": "changed",
		"part_type_id": 2,
		"properties": Unknown column type,
		"manufacturer": "changed",
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": 2016-07-07 12:34:45
	}
```
> Note that the `modified_at` field has been updated accordingly.

> If a user has `SYSTEM` permissions they can delete the `part`

```python
    url = 'https://smartapi.bboxx.co.uk/v1/parts/1'
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
endpoint | `/v1/parts`
method | `POST`
url_params | <font color="DarkGray">N/A</font>
query params | <font color="DarkGray">N/A</font>
body | JSON-formatted dictionary with the details of the `part` that you wish to create
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `201`

### GET
     | value
 ----:|:---
endpoint | `/v1/parts` or `/v1/parts/<part_id>`
method | `GET`
url_params | `part_id` <font color="DarkGray">_(int)_</font>
query params | *> See Query Format and Filtering*
body | <font color="DarkGray">N/A</font>
permissions | <font color="Jade">__`OVERVIEW`__</font>
response | `200`

### PUT
     | value
 ----:|:---
endpoint | `/v1/parts/<part_id>`
method | `PUT`
url_params | `part_id` of the part you wish to edit
query params | <font color="DarkGray">N/A</font>
body | JSON-formatted dictionary of the columns that you wish to alter
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `200`

### DELETE
     | value
 ----:|:---
endpoint | `/v1/parts/<part_id>`
method | `DELETE`
url_params | `part_id` <font color="DarkGray">_(int)_</font>
query params | <font color="DarkGray">N/A</font>
body | <font color="DarkGray">N/A</font>
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `204`

    