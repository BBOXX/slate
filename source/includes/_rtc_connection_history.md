## <u>Rtc Connection History</u>
Contains a history of RTC messages sent to each unit.


### <u>The rtc_connection_history object</u>

Field | Description
------:|:------------
__rtc_connection_history_id__ <br><font color="DarkGray">_int_</font> <font color="Crimson">__(primary key)__</font> | A unique integer identifier for each rtc_connection_history.
__<a href="/#product">product_imei</a>__ <br><font color="DarkGray">_varchar(15)_</font> <font color="Crimson">(not-null,foreign-key)</font> | 
__connection_status__ <br><font color="DarkGray">_string_</font> <font color="Crimson">(not-null)</font> | <br><font color="DodgerBlue">options: ["offline", "online"]</font>
__connection_status_time__ <br><font color="DarkGray">_datetime_</font> <font color="Crimson">(not-null)</font> | 
__connection_status_reason__ <br><font color="DarkGray">_string_</font> <font color="Crimson">(not-null)</font> | <br><font color="DodgerBlue">options: ["low-battery-voltage", "sleep-mode", "unknown", "user-request", "inactivity", "message-received"]</font>
__connection_status_info__ <br><font color="DarkGray">_string_</font> <font color="Crimson"></font> | 
__latest_message_time__ <br><font color="DarkGray">_datetime_</font> <font color="Crimson"></font> | 
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

> `POST` requests are not allowed at this endpoint

> We can retrieve the `rtc_connection_history` created by specifying its `rtc_connection_history_id` in the request url:

```python
    url = 'https://smartapi.bboxx.co.uk/v1/rtc_connection_history/1'
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.get(url=url, headers=headers)

    r
    >>> <Response 200>

    r.json()
    >>> {
		"rtc_connection_history_id": 1
		"product_imei": "000000000000000",
		"connection_status": "test",
		"connection_status_time": "2000-01-01 00:00:00",
		"connection_status_reason": "test",
		"connection_status_info": "test",
		"latest_message_time": "2000-01-01 00:00:00",
		"created_at": "2000-01-01 00:00:00"
		"created_by": "test.user@bboxx.co.uk"
		"modified_at": None
	}
```

> We can retrieve all `rtc_connection_history` by omitting the `rtc_connection_history_id`:

```python
    url = 'https://smartapi.bboxx.co.uk/v1/rtc_connection_history'
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

> If a user has `SYSTEM` permissions they can delete the `rtc_connection_history`

```python
    url = 'https://smartapi.bboxx.co.uk/v1/rtc_connection_history/1'
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=A_VALID_TOKEN'}

    r = requests.delete(url=url, headers=headers)

    r
    >>> <Response 204>

    r.text
    >>>
```
> Note that the response from a 204 request is empty. This means that `r.json()` cannot be called and will throw a JSONDecodeError. In fact the response is `u''` - an empty unicode string.



### POST
`POST` requests are not allowed at this endpoint

### GET
     | value
 ----:|:---
endpoint | `/v1/rtc_connection_history` or `/v1/rtc_connection_history/<rtc_connection_history_id>`
method | `GET`
url_params | `rtc_connection_history_id` <font color="DarkGray">_(int)_</font>
query params | *> See Query Format and Filtering*
body | <font color="DarkGray">N/A</font>
permissions | <font color="Jade">__`OVERVIEW`__</font>
response | `200`

### PUT
`PUT` requests are not allowed at this endpoint

### DELETE
     | value
 ----:|:---
endpoint | `/v1/rtc_connection_history/<rtc_connection_history_id>`
method | `DELETE`
url_params | `rtc_connection_history_id` <font color="DarkGray">_(int)_</font>
query params | <font color="DarkGray">N/A</font>
body | <font color="DarkGray">N/A</font>
permissions | <font color="Crimson">__`SYSTEM`__</font>
response | `204`

    