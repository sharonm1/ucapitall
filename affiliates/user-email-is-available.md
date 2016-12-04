## Check if email is available for registration

GET http://api.ubinary.com/trading/user/email/is/available?data=JSON_DATA

where `JSON_DATA` is like

```C#
{
    string Email;               // an email to test
}
```

##### A valid request example

http://api.ubinary.com/trading/user/email/is/available?data=%7B%22Email%22:%22john@ub.com%22%7D

```json
{
  "Email": "john@ub.com"
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
    bool EmailIsAvailable;        // true - user with this email can be registered
                                  // false - this email exists (registration will fail)
}
```

##### Successful response example

```json
{
  "TrackingId": "74.77.97",
  "ErrorCode": "Ok",
  "ErrorMessage": "",
  "EmailIsAvailable": true
}
```


##### Unsuccessful response example

```json
{
  "TrackingId": "50.97.61",
  "ErrorCode": "Failed",
  "ErrorMessage": "Oops, something went wrong (50.97.61)"
}
```


#### Expectations
- None

#### Access restrictions
- None (public)
