## <u>Part Parameter</u>
Base table that product_parameters and part_parameters can inherit from


### <u>The part_parameter object</u>

Field | Description
------:|:------------
__part_parameter_id__ <br><font color="DarkGray">_int_</font> <font color="Crimson">__(primary key)__</font> | A unique integer identifier for each part_parameter.
__value__ <br><font color="DarkGray">_string_</font> <font color="Crimson">(not-null)</font> | 
__date_added__ <br><font color="DarkGray">_datetime_</font> <font color="Crimson"></font> | 
__date_removed__ <br><font color="DarkGray">_datetime_</font> <font color="Crimson"></font> | 
__<a href="/#part">part_id</a>__ <br><font color="DarkGray">_int_</font> <font color="Crimson">(not-null,foreign-key)</font> | 
__status__ <br><font color="DarkGray">_string_</font> <font color="Crimson"></font> | <br><font color="DodgerBlue">options: ["active", "removed", "expired", "pending"]</font>
__<a href="/#parameter-type">parameter_type_id</a>__ <br><font color="DarkGray">_int_</font> <font color="Crimson">(not-null,foreign-key)</font> | 
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

> An example POST request. Note that `part_parameter_id`, `created_at`, `modified_at` and `created_by` are all handled internally by the system and need not be explicitly specified. See Meta Data for more information.

```python
    url = "http://smartapi.bboxx.co.uk/v1/part_parameters"
    data = json.dumps({
		"value": "test",
		"date_added": "2000-01-01 00:00:00",
		"date_removed": "2000-01-01 00:00:00",
		"part_id": 1,
		"status": "test",
		"parameter_type_id": 1,
		})
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.post(url=url, data=data, headers=headers)

    r
    >>> <Response 201>

    r.json()

    >>> {
		"part_parameter_id": 1
		"value": "test",
		"date_added": "2000-01-01 00:00:00",
		"date_removed": "2000-01-01 00:00:00",
		"part_id": 1,
		"status": "test",
		"parameter_type_id": 1,
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": None
	}
```

    > We can retrieve the `part_parameter` created by specifying its `part_parameter_id` in the request url:

```python
    url = 'http://smartapi.bboxx.co.uk/v1/part_parameters/1'
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.get(url=url, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"part_parameter_id": 1
		"value": "test",
		"date_added": "2000-01-01 00:00:00",
		"date_removed": "2000-01-01 00:00:00",
		"part_id": 1,
		"status": "test",
		"parameter_type_id": 1,
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": None
	}
```

> We can retrieve all `part_parameters` by omitting the `part_parameter_id`:

```python
    url = 'http://smartapi.bboxx.co.uk/v1/part_parameters'
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

> We can edit the newly created `part_parameter` with a `PUT` request:

```python
    url = 'http://smartapi.bboxx.co.uk/v1/part_parameters/1'
    data = json.dumps({
		"value": "changed",
		"date_added": "2016-07-01 12:34:45",
		"date_removed": "2016-07-01 12:34:45",
		"part_id": 2,
		"status": "changed",
		"parameter_type_id": 2,
		})
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.put(url=url, data=data, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"part_parameter_id": 1
		"value": "changed",
		"date_added": "2016-07-01 12:34:45",
		"date_removed": "2016-07-01 12:34:45",
		"part_id": 2,
		"status": "changed",
		"parameter_type_id": 2,
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": 2016-07-07 12:34:45
	}
```
> Note that the `modified_at` field has been updated accordingly.

> If a user has `SYSTEM` permissions they can delete the `part_parameter`

```python
    url = 'http://smartapi.bboxx.co.uk/v1/part_parameters/1'
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
endpoint | `/v1/part_parameters`
method | `POST`
url_params | <font color="DarkGray">N/A</font>
query params | <font color="DarkGray">N/A</font>
body | JSON-formatted dictionary with the details of the `part_parameter` that you wish to create
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `201`

### GET
     | value
 ----:|:---
endpoint | `/v1/part_parameters` or `/v1/part_parameters/<part_parameter_id>`
method | `GET`
url_params | `part_parameter_id` <font color="DarkGray">_(int)_</font>
query params | *> See Query Format and Filtering*
body | <font color="DarkGray">N/A</font>
permissions | <font color="Jade">__`OVERVIEW`__</font>
response | `200`

### PUT
     | value
 ----:|:---
endpoint | `/v1/part_parameters/<part_parameter_id>`
method | `PUT`
url_params | `part_parameter_id` of the part_parameter you wish to edit
query params | <font color="DarkGray">N/A</font>
body | JSON-formatted dictionary of the columns that you wish to alter
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `200`

### DELETE
     | value
 ----:|:---
endpoint | `/v1/part_parameters/<part_parameter_id>`
method | `DELETE`
url_params | `part_parameter_id` <font color="DarkGray">_(int)_</font>
query params | <font color="DarkGray">N/A</font>
body | <font color="DarkGray">N/A</font>
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `204`

    