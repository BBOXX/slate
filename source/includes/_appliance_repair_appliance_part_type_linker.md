## <u>Appliance Repair Appliance Part Type Linker</u>
Lists the appliance part_types that were used in a given appliance_repair


### <u>The appliance_repair_appliance_part_type_linker object</u>

Field | Description
------:|:------------
__appliance_repair_appliance_part_type_linker_id__ <br><font color="DarkGray">_int_</font> <font color="Crimson">__(primary key)__</font> | A unique integer identifier for each appliance_repair_appliance_part_type_linker.
__<a href="/#appliance-repair">appliance_repair_id</a>__ <br><font color="DarkGray">_int_</font> <font color="Crimson">(not-null,foreign-key)</font> | 
__<a href="/#old-appliance-part-type">old_appliance_part_type_id</a>__ <br><font color="DarkGray">_int_</font> <font color="Crimson">(not-null,foreign-key)</font> | 
__<a href="/#new-appliance-part-type">new_appliance_part_type_id</a>__ <br><font color="DarkGray">_int_</font> <font color="Crimson">(foreign-key)</font> | 
__repaired_parts_count__ <br><font color="DarkGray">_int_</font> <font color="Crimson"></font> | count of repaired parts
__requested_date__ <br><font color="DarkGray">_datetime_</font> <font color="Crimson"></font> | 
__replaced_date__ <br><font color="DarkGray">_datetime_</font> <font color="Crimson"></font> | 
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

> An example POST request. Note that `appliance_repair_appliance_part_type_linker_id`, `created_at`, `modified_at` and `created_by` are all handled internally by the system and need not be explicitly specified. See Meta Data for more information.

```python
    url = "https://smartapi.bboxx.co.uk/v1/appliance_repair_appliance_part_type_linker"
    data = json.dumps({
		"appliance_repair_id": 1,
		"old_appliance_part_type_id": 1,
		"new_appliance_part_type_id": 1,
		"requested_date": "2000-01-01 00:00:00",
		"replaced_date": "2000-01-01 00:00:00",
		})
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.post(url=url, data=data, headers=headers)

    r
    >>> <Response 201>

    r.json()

    >>> {
		"appliance_repair_appliance_part_type_linker_id": 1
		"appliance_repair_id": 1,
		"old_appliance_part_type_id": 1,
		"new_appliance_part_type_id": 1,
		"repaired_parts_count": 1,
		"requested_date": "2000-01-01 00:00:00",
		"replaced_date": "2000-01-01 00:00:00",
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": None
	}
```

> We can retrieve the `appliance_repair_appliance_part_type_linker` created by specifying its `appliance_repair_appliance_part_type_linker_id` in the request url:

```python
    url = 'https://smartapi.bboxx.co.uk/v1/appliance_repair_appliance_part_type_linker/1'
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.get(url=url, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"appliance_repair_appliance_part_type_linker_id": 1
		"appliance_repair_id": 1,
		"old_appliance_part_type_id": 1,
		"new_appliance_part_type_id": 1,
		"repaired_parts_count": 1,
		"requested_date": "2000-01-01 00:00:00",
		"replaced_date": "2000-01-01 00:00:00",
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": None
	}
```

> We can retrieve all `appliance_repair_appliance_part_type_linker` by omitting the `appliance_repair_appliance_part_type_linker_id`:

```python
    url = 'https://smartapi.bboxx.co.uk/v1/appliance_repair_appliance_part_type_linker'
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

> We can edit the newly created `appliance_repair_appliance_part_type_linker` with a `PUT` request:

```python
    url = 'https://smartapi.bboxx.co.uk/v1/appliance_repair_appliance_part_type_linker/1'
    data = json.dumps({
		"appliance_repair_id": 2,
		"old_appliance_part_type_id": 2,
		"new_appliance_part_type_id": 2,
		"requested_date": "2016-07-01 12:34:45",
		"replaced_date": "2016-07-01 12:34:45",
		})
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.put(url=url, data=data, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"appliance_repair_appliance_part_type_linker_id": 1
		"appliance_repair_id": 2,
		"old_appliance_part_type_id": 2,
		"new_appliance_part_type_id": 2,
		"repaired_parts_count": 1,
		"requested_date": "2016-07-01 12:34:45",
		"replaced_date": "2016-07-01 12:34:45",
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": 2016-07-07 12:34:45
	}
```
> Note that the `modified_at` field has been updated accordingly.

> If a user has `SYSTEM` permissions they can delete the `appliance_repair_appliance_part_type_linker`

```python
    url = 'https://smartapi.bboxx.co.uk/v1/appliance_repair_appliance_part_type_linker/1'
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
endpoint | `/v1/appliance_repair_appliance_part_type_linker`
method | `POST`
url_params | <font color="DarkGray">N/A</font>
query params | <font color="DarkGray">N/A</font>
body | JSON-formatted dictionary with the details of the `appliance_repair_appliance_part_type_linker` that you wish to create
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `201`

### GET
     | value
 ----:|:---
endpoint | `/v1/appliance_repair_appliance_part_type_linker` or `/v1/appliance_repair_appliance_part_type_linker/<appliance_repair_appliance_part_type_linker_id>`
method | `GET`
url_params | `appliance_repair_appliance_part_type_linker_id` <font color="DarkGray">_(int)_</font>
query params | *> See Query Format and Filtering*
body | <font color="DarkGray">N/A</font>
permissions | <font color="Jade">__`OVERVIEW`__</font>
response | `200`

### PUT
     | value
 ----:|:---
endpoint | `/v1/appliance_repair_appliance_part_type_linker/<appliance_repair_appliance_part_type_linker_id>`
method | `PUT`
url_params | `appliance_repair_appliance_part_type_linker_id` of the appliance_repair_appliance_part_type_linker you wish to edit
query params | <font color="DarkGray">N/A</font>
body | JSON-formatted dictionary of the columns that you wish to alter
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `200`

### DELETE
     | value
 ----:|:---
endpoint | `/v1/appliance_repair_appliance_part_type_linker/<appliance_repair_appliance_part_type_linker_id>`
method | `DELETE`
url_params | `appliance_repair_appliance_part_type_linker_id` <font color="DarkGray">_(int)_</font>
query params | <font color="DarkGray">N/A</font>
body | <font color="DarkGray">N/A</font>
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `204`

    