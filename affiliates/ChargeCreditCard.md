## Charge Credit Card

Chage credit card of the logged in user
#### Request

GET http://api.ucapital.com/deposit/add?data=JSON_DATA


where `JSON_DATA` is like

```C#
{
    string creditCard;
	string cvv2;
	decimal amount; 
    string location ;
}
```

##### A valid request example

```json
 {
  "creditCard": "5984",
  "cvv2": "055",
  "amount": "100",
  "location": "GB"
}

```


#### Response

Status | Response body
-------|--------------
200    | JSON_RESPONSE

where `JSON_RESPONSE` is like

```C#
{
   string TrackingId;
   string ErrorCode;
   string ErrorMessage;
}

##### Response example

```json
{
	TrackingId: "83.81.35",
	ErrorCode: "Ok",
	ErrorMessage: ""
}
```


#### Access restrictions

- User must be logged in
- White IP list


#### Expectations

None
