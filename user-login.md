## User login

GET http://api.ubinary.com/trading/user/login?data=JSON_DATA

where `JSON_DATA` is like

```C#
{
    string UserEmail;               // user's email
    string UserPassword;            // user's password
    string RedirectTo;              // optional - redirect user to this URL
                                    //      URL should be an abolute URL
                                    //      URL should be within the same domain
}
```


##### A valid request example

http://api.ubinary.com/trading/user/login?data={"UserEmail":"john@company.com","UserPassword":"111111"}


```json
{
  "UserEmail": "john@company.com",
  "UserPassword": "111111"
}
```

```json
{
  "UserEmail": "john@company.com",
  "UserPassword": "111111",
  "RedirectTo": "http://www.ubinary.com/trade-binary/"
}
```


#### Response

Status | Response body
-------|--------------
200    | JSON_RESPONSE

where `JSON_RESPONSE` is like

```C#
{
    string TrackingId;          // tracking id of this request for a later troubleshooting
    string ErrorCode;           // short error code; 'Ok' - for successful request
    string ErrorMessage;        // error description (if there is an error)
}
```

##### Successful response example

```json
{
    "TrackingId": "12.34.56",
    "ErrorCode": "Ok",
    "Error": ""
}
```


##### Unsuccessful response example

```json
{
  "TrackingId": "80.21.87",
  "ErrorCode": "RC_PASSWORD_IS_WRONG",
  "ErrorMessage": "Oops, something went wrong (80.21.87)"
}
```

```json
{
  "TrackingId": "80.04.65",
  "ErrorCode": "Failed",
  "ErrorMessage": "'UserEmail': an email is only supported; userEmail='284695'"
}
```

#### Expectations
None


#### Access restrictions
None (public)
