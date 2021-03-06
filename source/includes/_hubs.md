## <u>Hub</u>
Contains details of all every BBOXX hub-centre (obselete)


### <u>The hub object</u>

Field | Description
------:|:------------
__hub_id__ <br><font color="DarkGray">_int_</font> <font color="Crimson">__(primary key)__</font> | A unique integer identifier for each hub.
__name__ <br><font color="DarkGray">_string_</font> <font color="Crimson">(not-null,unique)</font> | 
__guid__ <br><font color="DarkGray">_string_</font> <font color="Crimson">(unique)</font> | 
__<a href="/#entity">entity_id</a>__ <br><font color="DarkGray">_int_</font> <font color="Crimson">(not-null,foreign-key)</font> | 
__latitude__ <br><font color="DarkGray">_varchar(12)_</font> <font color="Crimson"></font> | 
__longitude__ <br><font color="DarkGray">_varchar(12)_</font> <font color="Crimson"></font> | 
__created_at__  <br><font color="DarkGray">_datetime_</font> | timestamp that the record was created at
__created_by__  <br><font color="DarkGray">_text_</font>| username of the user who created the record
__modified_at__ <br><font color="DarkGray">_datetime_</font>| timestamp that the record was last modified
__modified_by__ <br><font color="DarkGray">_text_</font>| user that last modified the record

<br>

Relationship | Description
-------------:|:------------
__products__ | The associated products
__shops__ | The associated shops


<hr>
<br>

> An example POST request. Note that `hub_id`, `created_at`, `modified_at` and `created_by` are all handled internally by the system and need not be explicitly specified. See Meta Data for more information.

```python
    url = "https://smartapi.bboxx.co.uk/v1/hubs"
    data = json.dumps({
		"name": "test",
		"guid": "test",
		"entity_id": 1,
		"latitude": "-1.111111111",
		"longitude": "-1.111111111",
		})
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.post(url=url, data=data, headers=headers)

    r
    >>> <Response 201>

    r.json()

    >>> {
		"hub_id": 1
		"name": "test",
		"guid": "test",
		"entity_id": 1,
		"latitude": "-1.111111111",
		"longitude": "-1.111111111",
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": None
	}
```

> We can retrieve the `hub` created by specifying its `hub_id` in the request url:

```python
    url = 'https://smartapi.bboxx.co.uk/v1/hubs/1'
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.get(url=url, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"hub_id": 1
		"name": "test",
		"guid": "test",
		"entity_id": 1,
		"latitude": "-1.111111111",
		"longitude": "-1.111111111",
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": None
	}
```

> We can retrieve all `hubs` by omitting the `hub_id`:

```python
    url = 'https://smartapi.bboxx.co.uk/v1/hubs'
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

> We can edit the newly created `hub` with a `PUT` request:

```python
    url = 'https://smartapi.bboxx.co.uk/v1/hubs/1'
    data = json.dumps({
		"name": "changed",
		"guid": "changed",
		"entity_id": 2,
		"latitude": "-9.999999999",
		"longitude": "-9.999999999",
		})
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.put(url=url, data=data, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"hub_id": 1
		"name": "changed",
		"guid": "changed",
		"entity_id": 2,
		"latitude": "-9.999999999",
		"longitude": "-9.999999999",
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": 2016-07-07 12:34:45
	}
```
> Note that the `modified_at` field has been updated accordingly.

> If a user has `SYSTEM` permissions they can delete the `hub`

```python
    url = 'https://smartapi.bboxx.co.uk/v1/hubs/1'
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
endpoint | `/v1/hubs`
method | `POST`
url_params | <font color="DarkGray">N/A</font>
query params | <font color="DarkGray">N/A</font>
body | JSON-formatted dictionary with the details of the `hub` that you wish to create
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `201`

### GET
     | value
 ----:|:---
endpoint | `/v1/hubs` or `/v1/hubs/<hub_id>`
method | `GET`
url_params | `hub_id` <font color="DarkGray">_(int)_</font>
query params | *> See Query Format and Filtering*
body | <font color="DarkGray">N/A</font>
permissions | <font color="Jade">__`OVERVIEW`__</font>
response | `200`

### PUT
     | value
 ----:|:---
endpoint | `/v1/hubs/<hub_id>`
method | `PUT`
url_params | `hub_id` of the hub you wish to edit
query params | <font color="DarkGray">N/A</font>
body | JSON-formatted dictionary of the columns that you wish to alter
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `200`

### DELETE
     | value
 ----:|:---
endpoint | `/v1/hubs/<hub_id>`
method | `DELETE`
url_params | `hub_id` <font color="DarkGray">_(int)_</font>
query params | <font color="DarkGray">N/A</font>
body | <font color="DarkGray">N/A</font>
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `204`

    