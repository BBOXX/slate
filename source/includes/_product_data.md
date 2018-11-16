# Product Data

Along with the technical data described in the <a href="#schema">Schema</a> , BBOXX collects telemetry data such as Current, Voltage and Temperature (amongst a range of others) from each unit. This time-series data is held in a separate time-series database.

BBOXX uses <a href="https://docs.influxdata.com/influxdb/v1.0/">InfluxDB</a> as it's time-series database.

## Schema

InfluxDB uses <a href="https://docs.influxdata.com/influxdb/v1.0/concepts/key_concepts/#measurement">`measurements`</a>, <a href="https://docs.influxdata.com/influxdb/v1.0/concepts/key_concepts/#field-set">`fields`</a> and <a href="https://docs.influxdata.com/influxdb/v1.0/concepts/key_concepts/#tag-set">`tags`</a> to uniquely identify data.

All `measurements` are stored inside `retention policies`. 
A `measurement` is a logical grouping of streams of incoming data.
A `field` describes a single stream like `current`, `voltage` or `temperature`.
The `tags` identify the unit that the data is generated from.

All data recorded from a unit is held in the relevant `field`. 
Some `measurements`, and some fields with are currently only used by certain products. 
Also, only certain units are currently using certain `fields` as well (e.g device usage disaggregation)

There are several `rentention policies` and `measurements` inside the Bboxx instance of InfluxDB. Below is an overview of some of the fields inside the core measurements.

The `telemetry` measurement from the `telemetry_rp` retention policy contains the following fields:

field | data-type
 ----:|:--- | ---
`ac_current` | float
`ac_voltage` | float
`active_power` | float
`apparent_power` | float
`charge_current` | float
`current` | float
`current_in` | float
`current_out` | float
`dc_load_current` | float
`energy` | float
`pack_current` | float
`panel_voltage` | float
`product_imei` | integer
`pulse_count` | integer?
`state_of_charge_percent` | integer
`state_of_charge_wh` | float
`temperature` | float
`usb_current` | float
`voltage` | float
`voltage_cell_1` | float
`voltage_cell_2` | float 
`voltage_cell_3` | float
`voltage_cell_4` | float    

The `analysis` measurement from the `analysis_rp` contains the following fields:

field | data-type
 ----:|:--- | ---
`discharge_ah` | float
`discharge_end` | integer
`discharge_imax` | float
`discharge_vmax` | float
`discharge_vmin` | float
`discharge_wh` | float
`energy_in` | float
`energy_out` | float
`gap_end` | float
`lvd` | float
`state_of_charge` | float

All products use the `telemetry` measurement to record data, so we'll be using that in our examples.

Inside `telemetry` datapoint is tagged with the <a href="#product">product_imei</a>. However some measurements
have different tags. 

## Example 1
> InfluxDB schema for a single unit storing I, V, T

```python
name: telemetry            fld     fld       fld         tag
-----------------------------------------------------------------
time                     current voltage temperature product_imei

2016-09-02T08:30:42.645Z    1       2         3      013777946874001
2016-09-02T08:40:53.327Z    1       2         3      013777946874001
2016-09-02T08:41:56.348Z    1       2         3      013777946874001
2016-09-02T08:42:35.505Z    1       2         3      013777946874001
```
For example - a unit has product_imei: 013777946874001
This unit has 3 things being recorded:

* current (I)
* voltage (V)
* temperature (T)

The data would therefore be recorded in Influx as follows (see right):

## Example 2
> New schema for the 'telemetry' measurement with a second unit adding data.

```python
name: telemetry            fld     fld       fld     fld   fld       tag
-------------------------------------------------------------------------------
time                     current voltage temperature c_in c_out  product_imei

2016-09-02T08:30:42.645Z    1       2         3                 013777946874001
2016-09-02T08:40:53.327Z    1       2         3                 013777946874001
2016-09-02T08:41:56.348Z    1       2         3                 013777946874001
2016-09-02T08:42:35.505Z    1       2         3                 013777946874001
2016-08-30T10:05:36.873Z    4       5         6       7     8   013950004127933
2016-08-30T10:06:00.734Z    4       5         6       7     8   013950004127933
2016-08-30T16:43:11.984Z    4       5         6       7     8   013950004127933
2016-08-30T16:43:22.646Z    4       5         6       7     8   013950004127933
```

A second unit has product_imei: 866771029491460
This unit has 5 things being recorded:

* current (I)
* current_in (I_in)
* current_out (I_out)
* voltage (V)
* temperature (T)

The influx data would therefore be now look like this (see right):

Note that two new `fields` have been added `current_in`, and `current_out` (abbreviated for readability), which are null for unit 4001 but filled for unit 7933. The telemetry measurement can support arbitrary new fields from a unit.

As it currently stands, the 'telemetry' measurement currently has 24 fields in use, although not all units are
using these measurements. The fields are:
`time`,  `ac_current`, `ac_voltage`, `active_power`, `apparent_power`, `charge_current`, `current`, `current_in`,      `current_out`, `dc_load_current energy`, `pack_current`, `panel_voltage`, `product_imei`, `pulse_count`, `state_of_charge_percent`, `state_of_charge_wh`, `temperature`, `usb_current voltage`, `voltage_cell_1`, `voltage_cell_2`, `voltage_cell_3`, `voltage_cell_4`

Users can query data relating to each product, specifying fields and tags as desired. See <a href="#reading-data-for-a-product">Reading Data for a Product</a> for more information.

## Writing Data to Influx

> Data should be supplied in the following JSON data structure:


```python
data = {
    "measurement": <measurement_name>,
    "tags": { "tag_name": <value> },
    "fields": {
        "field_name": [ [time, value], [time, value], [time, value] ]
        "field_name": [ [time, value], [time, value], [time, value] ]
        "field_name": [ [time, value], [time, value], [time, value] ]
    },
}
```

> Below is a specific example for storing current, voltage and temperature:

```python
data = {
    "measurement": "telemetry",
    "tags": { "some_tag": "tag_value" },
    "fields": {
        "current": [
            ['2016-09-01', 1.0],
            ['2016-09-02', 2.0],
            ['2016-09-03', 3.0]
        ],
        "voltage": [
            ['2016-09-01', 10],
            ['2016-09-02', 20],
            ['2016-09-03', 30]
        ],
        "temperature": [
            ['2016-09-01', 0.1],
            ['2016-09-02', 0.2],
            ['2016-09-03', 0.3]
        ]
    }
}
```

Data is written to influx as a list of timestamp/value pairs. The `measurement`, `field` and `tags` are defined in a data structure as shown on the right.

### Measurements

A `measurement` is a logical container for different series. Examples of sensible measurement names could be:

* telemetry -_(for Current, Voltage, Temperature, Power)_
* logging - _(for storing logs if required)_
* analysis - _(for storing time-series that are not measured directly)_

### Fields

Each `measurement` may have many `fields`. Each `field` represents a single stream of incoming data. Example of sensible fields could be:

* current
* voltage
* temperature
* product_logs

### Tags

Values inside a `field` are differentiated by the `tags` on each point. Sensible `tags` could be:

* product_imei
* product_type_id
* entity_id

Tags may only contain Uppercase, Lowercase, '_' and '-' characters.

The combination of `Measurement/Field/Tag` therefore defines a time-series for a single unit.

For example if we wish to see Current and Voltage data for the unit 013777894567 we would look inside:

* `Measurement`: "telemetry"
* `Fields`: "current, voltage"
* `Tags`: {"product_imei": "013777894567"}

## Writing Data for a Product

> Data can be written to a specific product like this - note that the <a href="#product">`product_imei`</a> is automatically written into the tags and does not need to be specified by the user:

```python
    url = "https://smartapi.bboxx.co.uk/v1/products/<imei>/data"
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=' + A_VALID_TOKEN}

    data = json.dumps({
        "measurement": "telemetry",
        "tags": {"some_tag": "tag_value"},
        "fields": {
            "current": [
                [1472688000000, 1.0],
                [1472774400000, 2.0],
                [1472860800000, 3.0]
            ],
            "voltage": [
                ['2016-09-01T00:00:00Z', 10.0],
                ['2016-09-02 00:00:00', 20.0],
                ['2016-09-03', 30.0]
            ],
            "temperature": [
                ['Thu, September 1st 2016', 0.1],
                ['Fri, September 2nd 2016', 0.2],
                ['Sat, September 3rd 2016', 0.3]
            ]
        }
    })


    r = requests.post(url=url, data=data, headers=headers)

    print r.text
    >>> {
      "staus": "success"
      "message": "9 data-point(s) successfully written to influx",
      "data": null,
    }
```
Data for a single product data is written using the `/v1/products/<imei>/data` endpoint.

This endpoint will write data into the database tagged with the product_imei supplied in the endpoint.
Users can also specify other tags to be applied to every point in the supplied data by including them in the `tags` sections of the `POST` request.

Data is supplied as a dictionary with the `measurement`, `tags` and `fields` specified in the format as shown on the right.

The actual data is supplied as a list of `[<timestamp>, <value>]` pairs.

The `<timestamp>` can be any of the following:

* _**milliseconds**_ since epoch eg: `1475685693839`
* isoformatted date-time object eg: `'yyyy-mm-ddTHH:MM:SS.nnnnnnnnnZ'`
* sensibly formatted datetime string eg: `'yyyy-mm-dd HH:MM:SS.nnnnnnnnn'`
* most sensibly formatted string eg: `'Tue, October 4th 2016'`


<aside class="notice">If using integer-since-epoch the user <b>MUST</b> supply in <b>MILLISECONDS</b> since epoch start. Supplying seconds, microseconds or nanoseconds can result in unpredictable behaviour.</aside>


### POST
     | value
 ----:|:---
endpoint | `/v1/products/<imei>/data`
method | `POST`
url_params | `product_imei` <font color="DarkGray">_(varchar(15))_</font>
query params |  None
body | dictionary with  data-structure and a list of valid datapoints.
permissions | <font color="Jade">__`TECHNICAL`__</font>
response | `200`

<aside class="notice">Note! The <a href="#product">product_imei</a> tag doesn't need to be specified - it will be added automatically.</aside>


## Writing General Data

> More general data can be written like this:

```python
    url = "https://smartapi.bboxx.co.uk/v1/influx/data"
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=' + A_VALID_TOKEN}

    data = json.dumps({
        "measurement": "analysis",
        "fields": {
            "curve-data": [
                ["2016-01-01T00:01:20", 1],
                ["2016-01-01T00:01:21", 2],
                ["2016-01-01T00:01:22", 3],
                ["2016-01-01T00:01:23", 4],
            ],
        },
        "tags": {
            "analysis-type": "state-of-health",
            "product_imei": "000000000000000"
        }
    })


    r = requests.post(url=url, data=data, headers=headers)

    print r.text
    >>> {
      "staus": "success"
      "message": "4 data-point(s) successfully written to influx",
      "data": null,
    }
```

If a user wishes to store data that doesn't relate to a specific product they can send a `POST` the more general `/v1/influx/data` endpoint with data in the same format as before.

<aside class="notice">Note that this endpoint cannot auto-assign a <a href="#product">product_imei</a> tag so all fields and tags must be explicitly stated in the request.</aside>


### POST
     | value
 ----:|:---
endpoint | `/v1/influx/data`
method | `POST`
url_params | None
query params |  None
body | Correctly formatted set of datapoints (see right)
permissions | <font color="Jade">__`TECHNICAL`__</font>
response | `200`

## Reading data for a Product
> Here's an example dataset for a product with imei = 000000000000000

```
time                 current  product_imei    voltage  temperature
------------------------------------------------------------------
2016-01-01 00:00:00   1.234  000000000000000   14.243   21.345
2016-01-01 04:00:00   2.234  000000000000000   14.723
2016-01-01 08:00:00   3.234  000000000000000   14.826   21.345
2016-01-01 12:00:00   1.234  000000000000000   13.284
2016-01-01 16:00:00   2.345  000000000000000   12.345   21.345
2016-01-01 20:00:00   2.678  000000000000000   12.678
2016-01-02 00:00:00   2.910  000000000000000   12.910   21.910
2016-01-02 04:00:00   2.345  000000000000000   12.345
2016-01-02 08:00:00   2.678  000000000000000   12.678   21.678
2016-01-02 12:00:00   2.910  000000000000000   12.910
2016-01-02 16:00:00   2.345  000000000000000   12.345   21.345
2016-01-02 20:00:00   2.678  000000000000000   12.678
2016-01-03 00:00:00   2.910  000000000000000   12.910   21.910

```

> A `GET` request with no parameters will return the default query for the product.

```python
    url = "https://smartapi.bboxx.co.uk/v1/products/000000000000000/data"
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=' + A_VALID_TOKEN}

    r = requests.get(url=url, headers=headers)
    print r.json()
    >>> {
    u'status': u'success',
    u'message': u'data retrieved successfully',
    u'data': {
        u'measurement': u'telemetry'},
        u'tags': {u'product_imei': u'000000000000000'},
        u'current': [
            [1.234, u'2016-01-01T00:00:00Z'], [2.234, u'2016-01-01T04:00:00Z'], [3.234, u'2016-01-01T08:00:00Z'], [1.234, u'2016-01-01T12:00:00Z'], [2.345, u'2016-01-01T16:00:00Z'], [2.678, u'2016-01-01T20:00:00Z'], [2.91, u'2016-01-02T00:00:00Z'], [2.345, u'2016-01-02T04:00:00Z'], [2.678, u'2016-01-02T08:00:00Z'], [2.91, u'2016-01-02T12:00:00Z'], [2.345, u'2016-01-02T16:00:00Z'], [2.678, u'2016-01-02T20:00:00Z'], [2.91, u'2016-01-03T00:00:00Z']
        ],
        u'current_in': [
            [0, u'2016-01-01T00:00:00Z'], [0, u'2016-01-01T04:00:00Z'], [0, u'2016-01-01T08:00:00Z'], [0, u'2016-01-01T12:00:00Z'], [0, u'2016-01-01T16:00:00Z'], [0, u'2016-01-01T20:00:00Z'], [0, u'2016-01-02T00:00:00Z'], [0, u'2016-01-02T04:00:00Z'], [0, u'2016-01-02T08:00:00Z'], [0, u'2016-01-02T12:00:00Z'], [0, u'2016-01-02T16:00:00Z'], [0, u'2016-01-02T20:00:00Z'], [0, u'2016-01-03T00:00:00Z']
        ],
        u'current_out': [
            [1.234, u'2016-01-01T00:00:00Z'], [2.234, u'2016-01-01T04:00:00Z'], [3.234, u'2016-01-01T08:00:00Z'], [1.234, u'2016-01-01T12:00:00Z'], [2.345, u'2016-01-01T16:00:00Z'], [2.678, u'2016-01-01T20:00:00Z'], [2.91, u'2016-01-02T00:00:00Z'], [2.345, u'2016-01-02T04:00:00Z'], [2.678, u'2016-01-02T08:00:00Z'], [2.91, u'2016-01-02T12:00:00Z'], [2.345, u'2016-01-02T16:00:00Z'], [2.678, u'2016-01-02T20:00:00Z'], [2.91, u'2016-01-03T00:00:00Z']
        ],
        u'voltage': [
            [14.243, u'2016-01-01T00:00:00Z'], [14.723, u'2016-01-01T04:00:00Z'], [14.826, u'2016-01-01T08:00:00Z'], [13.284, u'2016-01-01T12:00:00Z'], [12.345, u'2016-01-01T16:00:00Z'], [12.678, u'2016-01-01T20:00:00Z'], [12.91, u'2016-01-02T00:00:00Z'], [12.345, u'2016-01-02T04:00:00Z'], [12.678, u'2016-01-02T08:00:00Z'], [12.91, u'2016-01-02T12:00:00Z'], [12.345, u'2016-01-02T16:00:00Z'], [12.678, u'2016-01-02T20:00:00Z'], [12.91, u'2016-01-03T00:00:00Z']
        ],
        u'temperature': [
            [21.345, u'2016-01-01T00:00:00Z'], [None, u'2016-01-01T04:00:00Z'], [21.345, u'2016-01-01T08:00:00Z'], [None, u'2016-01-01T12:00:00Z'], [21.345, u'2016-01-01T16:00:00Z'], [None, u'2016-01-01T20:00:00Z'], [21.91, u'2016-01-02T00:00:00Z'], [None, u'2016-01-02T04:00:00Z'], [21.678, u'2016-01-02T08:00:00Z'], [None, u'2016-01-02T12:00:00Z'], [21.345, u'2016-01-02T16:00:00Z'], [None, u'2016-01-02T20:00:00Z'], [21.91, u'2016-01-03T00:00:00Z']
        ],
}
```

> Any number of parameters can be explicitly specified, the other parameters will be filled with the default options.

```python
    url = "https://smartapi.bboxx.co.uk/v1/products/000000000000000/data"
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=' + A_VALID_TOKEN}

    params = {
        "start": "2016-01-02 23:00:00"
    }

    r = requests.get(url=url, params=params, headers=headers)
    r.json()
    >>> {
        u'status': u'success',
        u'message': u'data retrieved successfully',
        u'data': {
            u'tags': {u'product_imei': u'000000000000000'},
            u'measurement': u'telemetry'}
            u'current': [[2.91, u'2016-01-03T00:00:00Z']],
            u'current_in': [[2.91, u'2016-01-03T00:00:00Z']],
            u'current_out': [[2.91, u'2016-01-03T00:00:00Z']],
            u'voltage': [[12.91, u'2016-01-03T00:00:00Z']],
            u'temperature': [[21.91, u'2016-01-03T00:00:00Z']],
        }
```

> Complex queries can be built using the `where` clause parameters

```python
    url = "https://smartapi.bboxx.co.uk/v1/products/000000000000000/data"
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=' + A_VALID_TOKEN}

    params = {
        "start": '2016-01-01',
        "end": '2016-01-02',
        "limit": 100,
        "where": "voltage > 14.0"
        "fields": ["current", "temperature"]
    }

    r = requests.get(url=url, params=params, headers=headers)
    r.json()
    >>> {
        u'status': u'success',
        u'message': u'data retrieved successfully',
        u'data': {
            u'measurement': u'telemetry'}
            u'tags': {u'product_imei': u'000000000000000'},
            u'current': [[2.234, u'2016-01-01T04:00:00Z'], [3.234, u'2016-01-01T08:00:00Z']],
            u'temperature': [[None, u'2016-01-01T04:00:00Z'], [21.345, u'2016-01-01T08:00:00Z']],
    }
```

> Note that the query above has return datapoints in "current" and "temperature", where the corresponding voltage values were > 14.0V.

Users can `GET` data for a particular product using the same rm_data endpoint `/v1/products/<imei>/data`

As expected a `GET` request to this endpoint returns data relating to that product.

### Data Structure
Provided no errors occured with the request the response will be structured as follows:

<code>
{  
&emsp;&emsp;"status": "success",  
&emsp;&emsp;"message": "data returned successfully",  
&emsp;&emsp;"data": `<influx data structure>`  
}
</code>

Where `<influx data structure>` is as follows:

<code>
{  
&emsp;&emsp;"measurement": `<measurement name>`,  
&emsp;&emsp;"tags": {  
&emsp;&emsp;&emsp;&emsp;`<tagName1>`: `<tagValue1>`,  
&emsp;&emsp;&emsp;&emsp;`<tagName2>`: `<tagValue2>`, 
&emsp;&emsp;&emsp;&emsp;`<tagName3>`: `<tagValue3>`,  
&emsp;&emsp;&emsp;&emsp;etc..  
&emsp;&emsp;},  
&emsp;&emsp;`<fieldName1>`: [[`<value>`, `<timestamp>`],[`<value>`, `<timestamp>`],[`<value>`, `<timestamp>`]],  
&emsp;&emsp;`<fieldName2>`: [[`<value>`, `<timestamp>`],[`<value>`, `<timestamp>`],[`<value>`, `<timestamp>`]],  
&emsp;&emsp;`<fieldName3>`: [[`<value>`, `<timestamp>`],[`<value>`, `<timestamp>`],[`<value>`, `<timestamp>`]],  
}  
</code>

**NOTE** if the get request is asking for device disaggregation data, then `<influx data structure>` will look more like this:

{  
&emsp;&emsp;"measurement": `<measurement name>`,  
&emsp;&emsp;"tags": {  
&emsp;&emsp;&emsp;&emsp;`<tagName1>`: `<tagValue1>`,  
&emsp;&emsp;&emsp;&emsp;`<tagName2>`: `<tagValue2>`, 
&emsp;&emsp;&emsp;&emsp;`<tagName3>`: `<tagValue3>`,  
&emsp;&emsp;&emsp;&emsp;etc..  
&emsp;&emsp;},  
&emsp;&emsp;`<fieldName1>`: [[`<value>`, `<timestamp>`],[`<value>`, `<timestamp>`],[`<value>`, `<timestamp>`]],  
&emsp;&emsp;`<fieldName2>`: [[`<value>`, `<timestamp>`],[`<value>`, `<timestamp>`],[`<value>`, `<timestamp>`]],  
&emsp;&emsp;`<fieldName3>`: [[`<value>`, `<timestamp>`],[`<value>`, `<timestamp>`],[`<value>`, `<timestamp>`]],  
}  
</code>



### Parameters

Users can filter the data they received by providing filters in the `parameters` of the `GET` request. Each parameter is optional and if not provided will be filled by the default option.

Defaults will be defined separately for each <a href="#product_type">product_type</a> so different product types will return different data structures.

name | description | default
 ----:|:--- | ---
`start` | start-time | 7 days ago
`end` | end-time | now()
`fields` | fields to query | ["*"]
`measurement` | measurement to query | "telemetry"
`limit` | number of data-points to return | No limit
`where` | an optional <a href="https://docs.influxdata.com/influxdb/v1.0//query_language/data_exploration/#the-where-clause">`WHERE`-clause</a> | None
`tags` | JSON dictionary of tags to query | "{}" _(an empty JSON dictionary)
`ds_interval` | A downsampling interval to apply to the query | None
`ds_function` | The downsampling function to apply with `ds_interval` | `mean()`


### Full Query Examples

If a user queries `/v1/products/<imei>/data` and includes the following parameters:

* `{start: "2016-01-01"}`

Then they can expect to receive all available data from `telemetry` before 2016-01-01 and `now()`. Since `now()` is the default endtime.

A second query with parameters:

<code>  
{  
&emsp;&emsp;start: "2016-01-01",  
&emsp;&emsp;end: "2016-02-01",  
&emsp;&emsp;limit: 100,  
&emsp;&emsp;where: "'voltage' > 14.0",  
&emsp;&emsp;fields: ["current", "temperature"]  
}
</code>


Would return the first 100 datapoints in January where voltage > 14.0V for the unit. Note that since `fields` is specified as only `current` and `temperature` here the data returned are the values of `current` and `temperature` where the corresponding voltage was > 14.0,


### Tags
Users can filter by specific tags by supplying a JSON formatted dictionary in the parameters like this:

<code>
{  
&emsp;&emsp;start: "2016-01-01",  
&emsp;&emsp;end: "2016-02-01",  
&emsp;&emsp;tags: "{tagKey: tagValue, tagKey: tagValue}"  
}  
</code>

### Downsampling

Users can downsample data by using the `ds_interval` and `ds_function` parameters. These parameters are used to implement the `GROUP BY` functionality listed <a href="https://docs.influxdata.com/influxdb/v1.0//query_language/data_exploration/#group-by-tag-values">HERE</a> in the influxDB documentation.

Users can specifiy a time-range using `ds_interval` and a function using `ds_function` and the API will return data which been downsampled into '`ds_interval`'' chunks by applying the '`ds_interval`' function to datapoints with-in each chunk.  
When choosing a function users only need to name the function - do NOT include brackets (). 

### Available Downsampling Functions

<a href="https://docs.influxdata.com/influxdb/v1.0/query_language/functions/#integral">You can find a full list of available functions here</a>

The default downsampling function is `mean`

### Available Time Intervals
Time intervals are specifed as a string in the format: `"[number][unit]"`.  
Five minutes would be specified as `"5m"`  
The following units are available:  
<code>
{  
&emsp;&emsp; `u` _(microseconds)_  
&emsp;&emsp; `ms` _(milliseconds)_  
&emsp;&emsp; `s` _(seconds)_  
&emsp;&emsp; `m` _(minutes)_  
&emsp;&emsp; `h` _(hours)_  
&emsp;&emsp; `d` _(days)_  
&emsp;&emsp; `w` _(weeks)_  
}  
</code>

**Time Interval Examples**

Specifying 1 minute intervals  
`{ds_interval: "1m"}`  

Specifying 10 d intervals  
`{ds_interval: "10d"}`

Specifying half-second intervals in microseconds  
`{ds_interval: "500000u"}`

### Downsample Examples

To compute the 5 minute average of a series:

<code>
{  
&emsp;&emsp;"ds_interval": "5m"  
&emsp;&emsp;"ds_fucntion": "mean"  
}  
</code>

To compute the daily sum of a series:

<code>
{  
&emsp;&emsp;"ds_interval": "1d"  
&emsp;&emsp;"ds_fucntion": "sum"  
}  
</code>

To compute the hourly maximum of a series:

<code>
{  
&emsp;&emsp;"ds_interval": "1h"  
&emsp;&emsp;"ds_fucntion": "max"  
}  
</code>


## Reading General Data

A `GET` request to `/v1/influx/data` allows the user to read more general data from influx that doesn't relate to a specific product_imei. The parameter syntax and defaults are the same.


<aside class="notice">Note! A <a href="#product">product_imei</a> must be explicity stated if required when using this endpoint.</aside>

`Tags` are specified in the `GET` request as a JSON dictionary of key/value pairs. For example:

<code>
{  
&emsp;&emsp;start: "2016-01-01",  
&emsp;&emsp;end: "2016-02-01",  
&emsp;&emsp;tags: json.dumps({"product_imei": 111010101010101010})  
}
</code>

## Custom Queries

`#######################################################################################################`

** THIS IS SET TO BE REMOVED IN THE NEAR FUTURE! **

Please use `/v1/products/<imei>/data` or `/v1/influx/data` endpoint to query Influx data, and modifiy any existing calls to `/v1/influx/custom_query`.

`#######################################################################################################`

```python
    url = "https://smartapi.bboxx.co.uk/v1/influx/custom_query"
    headers = {'Content-Type': 'application/json', 'Authorization': 'Token token=' + A_VALID_TOKEN}

    params = {
        "q": "SELECT max(current) / mean(voltage) FROM telemetry WHERE "product_imei" = '000000000000000' and time > '2016-01-01'"
    }

    r = requests.get(url=url, params=params, headers=headers)
    r.json()
    >>> {
        u'status': u'success',
        u'message': u'data retrieved successfully',
        u'data': {}
```

For more complex queries and to leverage the full power of the <a href="https://docs.influxdata.com/influxdb/v1.0/query_language/data_exploration/">influxQL</a> the `/influx/custom_query` endpoint is available. 

Here users can submit a plain-text influxQL query which will be directly executed and the results returned. The other query parameters will not be accepted here.  

Queries should be submitted in the `q` parameter like this:  

<code>
{  
&emsp;&emsp;"q": `<valid-influxQL-query-str>`  
}  
</code>

Error checking and reporting on this endpoint is minimal so it's important to check that your query is valid before sending. 

The data is returned in a raw format so the format of the response will depend heavily on the query that is run. 

It's important to avoid queries that could cause enormous returns such as `"SELECT * FROM telemetry"`.   
In addition please note that `limit 1` will return 1 result _**per series**_.   
Therefore `SELECT * FROM telemetry limit 1` will return many thousands of results.   

Finally note that in plain-text influxQL queries quotes are important for naming `measurements`, `tags`, `fields` and timestamps. If unsure please check the influx documentation for details of what values should be quoted and what should, and which types of quotes (single/double) to use. 
