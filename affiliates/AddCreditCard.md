## Add Credit Card

add **credit card** for the logged in user


#### Request

GET http://api.ucapital.com/creditcard/add?data=JSON_DATA

where `JSON_DATA` is like

```C#

{
   string cardNumber;
   int cardTypeID;
   string cardholderName;
   string billcountry; 
   string billcity;
   string billaddres; 
   string billzipcode;
   string expYear;
   string expMonth;
   bool isDefault;  
}

```

   enum CreditCardTypes
{
    Visa = 1,
    MasterCard = 2,
    AmericanExpress = 3,
    Discover = 4,
    BankCard = 5,
    DinersClub = 6,
    JCB = 7,
    Maestro = 8,
    VisaElectron = 9,
    Isracard = 10,
    PayoneerCard = 11,
    LiveKash = 12
};

##### A valid request example

```json
{
  "billaddress": "Test",
  "billcity": "London",
  "billcountry": "UK",
  "billzipcode": "123456",
  "cardholderName": "Test",
  "cardNumber": "4111111111111111",
  "expMonth": "08",
  "expYear": "2017",
  "cardTypeID": "1"
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

```

##### Successful response example

```json
{
	TrackingId: "47.67.74",
	ErrorCode: "Ok",
	ErrorMessage: ""
}
```

#### Access restrictions

- user must be logged in
- Each request may retrieve up to one hundred items
- White IP list


#### Expectations

None
