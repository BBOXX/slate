## <u>Part Type Category</u>
The category of parts that each part_type belongs to


### <u>The part_type_category object</u>

Field | Description
------:|:------------
__part_type_category_id__ <br><font color="DarkGray">_int_</font> <font color="Crimson">__(primary key)__</font> | A unique integer identifier for each part_type_category.
__name__ <br><font color="DarkGray">_string_</font> <font color="Crimson">(not-null,unique)</font> | 
__created_at__  <br><font color="DarkGray">_datetime_</font> | timestamp that the record was created at
__created_by__  <br><font color="DarkGray">_text_</font>| username of the user who created the record
__modified_at__ <br><font color="DarkGray">_datetime_</font>| timestamp that the record was last modified
__modified_by__ <br><font color="DarkGray">_text_</font>| user that last modified the record

<br>

Relationship | Description
-------------:|:------------
__part_types__ | The associated part_types


<hr>
<br>

> `POST` requests are not allowed at this endpoint

> We can retrieve the `part_type_category` created by specifying its `part_type_category_id` in the request url:

```python
    url = 'https://smartapi.bboxx.co.uk/v1/part_type_categories/1'
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.get(url=url, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"part_type_category_id": 1
		"name": "test",
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": None
	}
```

> We can retrieve all `part_type_categories` by omitting the `part_type_category_id`:

```python
    url = 'https://smartapi.bboxx.co.uk/v1/part_type_categories'
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
endpoint | `/v1/part_type_categories` or `/v1/part_type_categories/<part_type_category_id>`
method | `GET`
url_params | `part_type_category_id` <font color="DarkGray">_(int)_</font>
query params | *> See Query Format and Filtering*
body | <font color="DarkGray">N/A</font>
permissions | <font color="Jade">__`OVERVIEW`__</font>
response | `200`

### PUT
`PUT` requests are not allowed at this endpoint

### DELETE
`DELETE` requests are not allowed at this endpoint



    