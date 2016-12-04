## Affiliate login

GET http://api.ubinary.com/trading/affiliate/12345/login?data=JSON_DATA

where `12345` - is your affiliate id and `JSON_DATA` is like

```C#
{
    string LoginKey;            // Login key
}
```

##### A valid request example

http://api.ubinary.com/trading/affiliate/12345/login?data={"LoginKey":"111111"}

```json
{
  "LoginKey": "111111"
}
```


#### Response

Status | Response body
-------|--------------
200    | JSON_RESPONSE

where `JSON_RESPONSE` is like

```C#
{
    string TrackingId;            // Tracking id for troubleshooting
    string ErrorCode;             // "Ok" if request succeeds, short error code if request fails
    string ErrorMessage;          // error description if request fails
    string SessionKey;            // Session key to use in API calls
}
```

##### Successful response example

```json
{
  "TrackingId": "85.82.63",
  "ErrorCode": "Ok",
  "ErrorMessage": "",
  "SessionKey": "c97ca67746cd46478cffb7ddb194f3a8"
}
```


##### Unsuccessful response example

```json
{
  "TrackingId": "34.02.14",
  "ErrorCode": "Failed",
  "ErrorMessage": "Affiliate 12345 has no bot associated with"
}
```

```json
{
  "TrackingId": "35.58.50",
  "ErrorCode": "Failed",
  "ErrorMessage": "Affiliate '101': LoginKey is not matched"
}
```

#### Expectations
None

#### Access restrictions
- White IP list
