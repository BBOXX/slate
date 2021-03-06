## <u>Test Jig Test Result</u>
Test results from the BBOXX test jig


### <u>The test_jig_test_result object</u>

Field | Description
------:|:------------
__test_jig_test_result_id__ <br><font color="DarkGray">_int_</font> <font color="Crimson">__(primary key)__</font> | A unique integer identifier for each test_jig_test_result.
__jig_id__ <br><font color="DarkGray">_unknown-type_</font> <font color="Crimson"></font> | 
__machine_id__ <br><font color="DarkGray">_unknown-type_</font> <font color="Crimson"></font> | 
__<a href="/#product">product_imei</a>__ <br><font color="DarkGray">_varchar(15)_</font> <font color="Crimson">(not-null,foreign-key)</font> | 
__jig_software_version__ <br><font color="DarkGray">_unknown-type_</font> <font color="Crimson"></font> | 
__user__ <br><font color="DarkGray">_string_</font> <font color="Crimson">(not-null)</font> | 
__passed__ <br><font color="DarkGray">_boolean_</font> <font color="Crimson">(not-null)</font> | 
__results__ <br><font color="DarkGray">_unknown-type_</font> <font color="Crimson"></font> | 
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

> An example POST request. Note that `test_jig_test_result_id`, `created_at`, `modified_at` and `created_by` are all handled internally by the system and need not be explicitly specified. See Meta Data for more information.

```python
    url = "https://smartapi.bboxx.co.uk/v1/test_jig_test_results"
    data = json.dumps({
		"jig_id": Unknown column type,
		"machine_id": Unknown column type,
		"product_imei": "000000000000000",
		"jig_software_version": Unknown column type,
		"user": "test",
		"passed": True,
		"results": Unknown column type,
		})
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.post(url=url, data=data, headers=headers)

    r
    >>> <Response 201>

    r.json()

    >>> {
		"test_jig_test_result_id": 1
		"jig_id": Unknown column type,
		"machine_id": Unknown column type,
		"product_imei": "000000000000000",
		"jig_software_version": Unknown column type,
		"user": "test",
		"passed": True,
		"results": Unknown column type,
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": None
	}
```

> We can retrieve the `test_jig_test_result` created by specifying its `test_jig_test_result_id` in the request url:

```python
    url = 'https://smartapi.bboxx.co.uk/v1/test_jig_test_results/1'
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.get(url=url, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"test_jig_test_result_id": 1
		"jig_id": Unknown column type,
		"machine_id": Unknown column type,
		"product_imei": "000000000000000",
		"jig_software_version": Unknown column type,
		"user": "test",
		"passed": True,
		"results": Unknown column type,
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": None
	}
```

> We can retrieve all `test_jig_test_results` by omitting the `test_jig_test_result_id`:

```python
    url = 'https://smartapi.bboxx.co.uk/v1/test_jig_test_results'
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

> We can edit the newly created `test_jig_test_result` with a `PUT` request:

```python
    url = 'https://smartapi.bboxx.co.uk/v1/test_jig_test_results/1'
    data = json.dumps({
		"jig_id": Unknown column type,
		"machine_id": Unknown column type,
		"product_imei": "999999999999999",
		"jig_software_version": Unknown column type,
		"user": "changed",
		"passed": False,
		"results": Unknown column type,
		})
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.put(url=url, data=data, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"test_jig_test_result_id": 1
		"jig_id": Unknown column type,
		"machine_id": Unknown column type,
		"product_imei": "999999999999999",
		"jig_software_version": Unknown column type,
		"user": "changed",
		"passed": False,
		"results": Unknown column type,
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": 2016-07-07 12:34:45
	}
```
> Note that the `modified_at` field has been updated accordingly.

> If a user has `SYSTEM` permissions they can delete the `test_jig_test_result`

```python
    url = 'https://smartapi.bboxx.co.uk/v1/test_jig_test_results/1'
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
endpoint | `/v1/test_jig_test_results`
method | `POST`
url_params | <font color="DarkGray">N/A</font>
query params | <font color="DarkGray">N/A</font>
body | JSON-formatted dictionary with the details of the `test_jig_test_result` that you wish to create
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `201`

### GET
     | value
 ----:|:---
endpoint | `/v1/test_jig_test_results` or `/v1/test_jig_test_results/<test_jig_test_result_id>`
method | `GET`
url_params | `test_jig_test_result_id` <font color="DarkGray">_(int)_</font>
query params | *> See Query Format and Filtering*
body | <font color="DarkGray">N/A</font>
permissions | <font color="Jade">__`OVERVIEW`__</font>
response | `200`

### PUT
     | value
 ----:|:---
endpoint | `/v1/test_jig_test_results/<test_jig_test_result_id>`
method | `PUT`
url_params | `test_jig_test_result_id` of the test_jig_test_result you wish to edit
query params | <font color="DarkGray">N/A</font>
body | JSON-formatted dictionary of the columns that you wish to alter
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `200`

### DELETE
     | value
 ----:|:---
endpoint | `/v1/test_jig_test_results/<test_jig_test_result_id>`
method | `DELETE`
url_params | `test_jig_test_result_id` <font color="DarkGray">_(int)_</font>
query params | <font color="DarkGray">N/A</font>
body | <font color="DarkGray">N/A</font>
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `204`

    