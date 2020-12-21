## <u>Part Type</u>
Lists the available part types


### <u>The part_type object</u>

Field | Description
------:|:------------
__part_type_id__ <br><font color="DarkGray">_int_</font> <font color="Crimson">__(primary key)__</font> | A unique integer identifier for each part_type.
__name__ <br><font color="DarkGray">_string_</font> <font color="Crimson">(not-null,unique)</font> | 
__description__ <br><font color="DarkGray">_string_</font> <font color="Crimson"></font> | 
__erp_code__ <br><font color="DarkGray">_unknown-type_</font> <font color="Crimson"></font> | 
__<a href="/#part-type-category">part_type_category_id</a>__ <br><font color="DarkGray">_int_</font> <font color="Crimson">(not-null,foreign-key)</font> | 
__serial_number_category__ <br><font color="DarkGray">_string_</font> <font color="Crimson">(not-null)</font> | <br><font color="DodgerBlue">options: ["unknown", "known", "hidden"]</font>
__parameter_types__ <br><font color="DarkGray">_array_</font> <font color="Crimson"></font> | 
__part_type_metadata_validator__ <br><font color="DarkGray">_string_</font> <font color="Crimson"></font> | 
__is_sent_by_unit__ <br><font color="DarkGray">_boolean_</font> <font color="Crimson"></font> | 
__created_at__  <br><font color="DarkGray">_datetime_</font> | timestamp that the record was created at
__created_by__  <br><font color="DarkGray">_text_</font>| username of the user who created the record
__modified_at__ <br><font color="DarkGray">_datetime_</font>| timestamp that the record was last modified
__modified_by__ <br><font color="DarkGray">_text_</font>| user that last modified the record

<br>

Relationship | Description
-------------:|:------------
__parts__ | The associated parts
__old_part_type_linkers__ | The associated old_part_type_linkers
__new_part_type_linkers__ | The associated new_part_type_linkers
__replacements__ | The associated replacements
__existings__ | The associated existings
__default_energy_limits__ | The associated default_energy_limits


<hr>
<br>

> `POST` requests are not allowed at this endpoint

> We can retrieve the `part_type` created by specifying its `part_type_id` in the request url:

```python
    url = 'https://smartapi.bboxx.co.uk/v1/part_types/1'
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.get(url=url, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"part_type_id": 1
		"name": "test",
		"description": "test",
		"erp_code": Unknown column type,
		"part_type_category_id": 1,
		"serial_number_category": "test",
		"parameter_types": [1,2,3],
		"part_type_metadata_validator": "test",
		"is_sent_by_unit": True,
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": None
	}
```

> We can retrieve all `part_types` by omitting the `part_type_id`:

```python
    url = 'https://smartapi.bboxx.co.uk/v1/part_types'
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

> `PUT` requests are not allowed at this endpoint

> `DELETE` requests are not allowed at this endpoint



### POST
`POST` requests are not allowed at this endpoint

### GET
     | value
 ----:|:---
endpoint | `/v1/part_types` or `/v1/part_types/<part_type_id>`
method | `GET`
url_params | `part_type_id` <font color="DarkGray">_(int)_</font>
query params | *> See Query Format and Filtering*
body | <font color="DarkGray">N/A</font>
permissions | <font color="Jade">__`OVERVIEW`__</font>
response | `200`

### PUT
`PUT` requests are not allowed at this endpoint

### DELETE
`DELETE` requests are not allowed at this endpoint



    