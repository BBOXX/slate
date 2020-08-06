## IRT Event Specifications

Each event specification contains two mandatory fields:

"ident" - unique identifier for the event

"label" - short description of the event, to be displayed to the user

### Example

{<br/>
   "ident": "battery.charged",<br/>
   "label": "Battery Charged",<br/>
}

The value entered by the user would be submitted to the send_event endpoint like this:

{<br/>
    "event": "battery.charged"<br/>
}


### ERROR_EVENT Events

current_state responses with attribute "user-input=False" may also define an event with id "ERROR_EVENT". This should be submitted to the send_event endpoint when an error occurs in the IRT client application during communication with the product under repair, or another device such as a printer. The data is submitted as a dictionary with two keys:

* "event" : "ERROR_EVENT"
* "payload" : a dictionary containing 3 keys:
    * "ident" : the ident of the input specification associated with the error
    * "message" : a message describing the error
    * "severity" : either "temporary" if the error may be resolved in future (e.g. by replacing a faulty printer) or "permanent" if the problem will never be resolved


