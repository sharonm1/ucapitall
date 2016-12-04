## Get user balance

GET http://api.ubinary.com/trading/affiliate/12345/user/get/balance?data=JSON_DATA

where `12345` - is your affiliate id and `JSON_DATA` is like

```C#
{
    string UserId;              // User email or user id
}
```

##### A valid request example

http://api.ubinary.com/trading/affiliate/12345/user/get/balance?data={"UserId":"john@ub.com"} 

```json
{
    "UserId": "john@ub.com",
}
```

http://api.ubinary.com/trading/affiliate/12345/user/get/balance?data={"UserId":"123456"} 

```json
{
    "UserId": 123456,
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
    decimal Balance;              // user's balance
    decimal FreeBalance;          // user's free balance (balance minus open positions)
    decimal Stakes;               // sum of user's open positions
    object Custom;                // custom (per affiliate) fields
}
```

#### Successful response example

```json
{
  "TrackingId": "99.89.96",
  "ErrorCode": "Ok",
  "ErrorMessage": "",
  "Balance": 5148.24,
  "Stakes": 0,
  "FreeBalance": 5148.24,
  "Custom": null
}
```


##### Unsuccessful response example

```json
{
  "TrackingId": "37.30.05",
  "ErrorCode": "Failed",
  "ErrorMessage": "User 'john@ub.com' is not registered"
}
```


#### Expectations
None

#### Access restrictions
- White IP list
