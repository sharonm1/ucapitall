# ucapitall
aapii.ucapitall
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

## Get User Deposits

Get all deposits of user

#### Request

GET http://api.ucapital.com/deposit/getuserdeposits?data=JSON_DATA

where `JSON_DATA` is like

```C#
{  
    int PagingIndex;            // user index to start with in case there are more results
    string UserId;               // user id (it could be user id as number or user id as email)
}
```

##### A valid request example

```json
{
  "PagingIndex": 0,
  "UserId": "216354"
}
```
or
```json
{
  "PagingIndex": 0,
  "UserId": "test@test.com"
}
```

#### Response

Status | Response body
-------|--------------
200    | JSON_RESPONSE

where `JSON_RESPONSE` is like

```C#
{
    string TrackingId;          // tracking id of this request (for troubleshooting...)
    FundTransaction[] Users;    // an array of retrieved transactions
    int PagingIndex;            // should be used in a consequent request
    int HasMoreData;            //     if there is more data
}

DepositFundTransaction
{
    int TransactionId;
    decimal DepositAmount;
	string CompletionTimestamp;
	TransactionType TransactionType;
	string Comment;
}

enum TransactionType
{
    Order, Refund, Bonus
}
```

##### Successful response example

```json
{
	TrackingId: "93.50.93",
	ErrorCode: "RC_OK",
	ErrorMessage: "",
	HasMoreData: 0,
	Transactions: 
			[
				{
				TransactionId: 1088335,
				DepositAmount: 5000,
				CompletionTimestamp: "2015-12-09 08:07:29",
				TransactionType: "Bonus",
				Comment: "test user"
				},
				{
				TransactionId: 1108516,
				DepositAmount: 1,
				CompletionTimestamp: "2015-12-24 14:28:04",
				TransactionType: "Order",
				Comment: "test"
				},
				{
				TransactionId: 1108625,
				DepositAmount: 1,
				CompletionTimestamp: "2015-12-24 15:07:47",
				TransactionType: "Order",
				Comment: "test"
				},
				{
				TransactionId: 1108626,
				DepositAmount: 1,
				CompletionTimestamp: "2015-12-24 15:08:14",
				TransactionType: "Order",
				Comment: "test"
				}
			],
	PagingIndex: 23
}

```

##### Successful response example with consequent request for remaining data

```json
{
  "PagingIndex": 101,
  "HasMoreData": 1
  "Transactions": [
    ...
}
```


#### Access restrictions

- User must be logged in.
- Each request may retrieve up to one hundred items
- White IP list



#### Expectations

None

## Get open positions of a specified user

GET http://api.ubinary.com/trading/affiliate/12345/user/get/position?data=JSON_DATA

where `12345` - is your affiliate id and `JSON_DATA` is like

```C#
{
    string UserId;              // User email or user id
	int PositionId; 
}
```

##### A valid request example

http://api.ubinary.com/trading/affiliate/12345/user/get/position?data={"UserId":"john@ub.com","PositionId":"1234"} 

```json
{
    "UserId": "john@ub.com",
	"PositionId": "1234"
}
```

http://api.ubinary.com/trading/affiliate/12345/user/get/position?data={"UserId":"123456","PositionId":"1234"} 

```json
{
    "UserId": 123456,
	"PositionId": "1234"
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
    Position[] Positions;         // array of open positions
}

enum Direction { Above, Below }

class Position
{
    int PositionId;
    string Asset;
    string ProductName;
    decimal Stake;
    Direction Direction;
    DateTime StartedAt;
    DateTime ExpirationAt;
    decimal OpenRate;
    decimal CloseRate;
    decimal Payout;
    string CloseReason;
}
```

#### Successful response example

```json
{
  "TrackingId": "57.28.63",
  "ErrorCode": "Ok",
  "ErrorMessage": "",
  "Positions": [
    {
      "PositionId": 676449,
      "Asset": "GBPUSD",
      "ProductName": "Sixty seconds",
      "Stake": 40,
      "Direction": "Above",
      "StartedAt": "24-Nov-2014 08:50:04",
      "ExpirationAt": "24-Nov-2014 08:51:04",
      "OpenRate": 1.5061,
      "CloseRate": 0,
      "Payout": 0,
      "CloseReason": null
    }
  ]
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

## Register lead

GET http://api.ubinary.com/trading/affiliate/12345/lead/register?data=JSON_DATA

where `12345` - is your affiliate id and `JSON_DATA` is like

```C#
{
    string FirstName;           // First name
    string LastName;            // Last name
    string PhoneNumber;         // Phone number
    string Email;               // Email
    string LanguageCode;        // optional - user preferred language (see details below)
    ulong Tlid;                 // optional - tracking link id (64 bits)
    string FromIp;              // optional - explicit client IP, if not specified IP is taken from request
    string CountryCode;         // optional - explicit country code, if not specified country is based on IP
    string Ctag;                // optional - a free parameter; it comes back in report API
    string AdData;              // optional - a free parameter (usually information about a campaign)
	string Comment;				// optional - a registration comment
}
```

LanguageCode | Language
-------------|--------------
En           | English
Ar           | Arabic
Ru           | Russian
Fr           | French
De           | Dutch
Es           | Spainish
Cn           | Chinese


##### A valid request example

http://api.ubinary.com/trading/affiliate/12345/lead/register?data=%7B%22FirstName%22:%22TestJohn%22,%22LastName%22:%22TestSmith%22,%22PhoneNumber%22:%22044-1234567%22,%22Email%22:%22test-12317@ub.com%22,%22Tlid%22:%22abcd-efgh-ighk%22,%22CountryCode%22:%22%22,%22FromIp%22:%22%22,%22Ctag%22:%22%22%7D

```json
{
  "FirstName": "TestJohn",
  "LastName": "TestSmith",
  "PhoneNumber": "044-1234567",
  "Email": "test-12317@ub.com",
  "LanguageCode": "en",
  "Tlid": "111222333444555666",
  "CountryCode": "GB",
  "FromIp": "211.148.218.20",
  "Ctag": "lead.JKFDSIE3243-4V432"
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
    int UserId;                   // The id of a newly created lead
}
```

##### Successful response example

```json
{
  "TrackingId": "74.77.97",
  "ErrorCode": "Ok",
  "ErrorMessage": "",
  "UserId": 299493
}
```


##### Unsuccessful response example

```json
{
  "TrackingId": "50.97.61",
  "ErrorCode": "RC_USER_ALREADY_EXISTS",
  "ErrorMessage": "Oops, something went wrong (50.97.61)",
  "UserId": 0
}
```

```json
{
  "TrackingId": "55.26.87",
  "ErrorCode": "Failed",
  "ErrorMessage": "RC_USER_ALREADY_EXISTS; email 'test-123@ub.com' is already exist"
}
```

```json
{
  "TrackingId": "50.01.14",
  "ErrorCode": "Failed",
  "ErrorMessage": "Unknown country code 'UK'"
}
```


#### Expectations
- None

#### Access restrictions
- None (public)

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

## Affiliate API module

#### Availible APIs

**NOTE**: 
You should build your HTTP request in a proper way.
For example, HTTP requests without any HTTP header probably will be blocked.

###### User reports
- [/reports/affiliate/12345/accounts.json](accounts.json.md) - get details of affiliate's users
- [/reports/affiliate/12345/transactions.json](transactions.json.md) - get details of users's fund transactions

###### User registration / login
- [/trading/affiliate/12345/lead/register](lead-register.md) - lead registration
- [/trading/affiliate/12345/user/register](user-register.md) - user registration
- [/trading/user/email/is/available](user-email-is-available.md) - check if email is available for registration
- [/trading/user/login](user-login.md) - user auto-login

###### Per user information
- [/trading/affiliate/12345/user/get/balance](user-get-balance.md) - get user's balance
- [/trading/affiliate/12345/user/get/open/positions](user-get-open-position.md) - get user's open positions
- [/trading/affiliate/12345/user/get/closed/positions](user-get-closed-position.md) - get user's closed positions

###### Trading
- [/trading/affiliate/12345/user/get/trading/options](user-get-trading-options.md) - get trading deals
- [/trading/affiliate/12345/login](login.md) - affiliate's login
- [/trading/affiliate/12345/user/open/position](user-open-position.md) - open position for a user

#### Opening position (bot trading)
- Affiliate has to login in order to open positions - [Login API](login.md)
- Each login starts a session (the session has an expiration timeout)
- During the session affiliate can open positions - [Open position API](user-open-position.md)

#### Deposits
- [/deposit/add] (ChargeCreditCard.md) - Charge Credit Card
- [/creditcard/add] (AddCreditCard.md) - Add Credit Card
- [/deposit/getuserdeposits] (GetUserDeposits.md) - Get User Deposits


## Transactions report

Get fund transactions between specified dates

GET http://api.ubinary.com/reports/affiliate/AFF_ID/transactions.json?from=FROM_DATE&to=TO_DATE&PagingIndex=PAGING_INDEX


where parameters are

Parameter       | Format                  | Description
----------------|-------------------------|-------------
AFF_ID          | integer                 | Your affiliate ID
FROM_DATE       | 'yyyy-MM-dd HH:mm:ss'   | Start from this date
FROM_TO         | 'yyyy-MM-dd HH:mm:ss'   | Until this date
PAGING_INDEX    | integer                 | 1 for first request, PagingIndex from a response if its HasMoreData is true

#### Response

Status | Response body
-------|--------------
200    | JSON_RESPONSE

where `JSON_RESPONSE` is like

```C#
{
    int PagingIndex;            // should be used in a consequent request
    int HasMoreData;            //     if there is more data
    Transaction[] Transactions; // an array of retrieved transactions
}

class Transaction
{
    string TransactionDate;
    string CTag;
    int AccountID;
    int TransactionID;
    string ActionName;
    double Amount;
    string Coin;
}
```

#### Successful request / response example

http://api.ubinary.com/reports/affiliate/12345/transactions.json?from=2014-10-01 00:00:00&to=2014-11-25 00:00:00&PagingIndex=1

```
{
  "HasMoreData": 0,
  "PagingIndex": 5,
  "Transactions": [
    {
      "TransactionDate": "2014-11-06 13:21:48",
      "CTag": null,
      "AccountID": 413003,
      "TransactionID": 810064,
      "ActionName": "deposit",
      "Amount": 250,
      "Coin": "USD"
    },
    ...
  ]
}
```

#### Paging index sample

*CAUTION:* PagingIndex is not the index of a desired page

In the first request PagingIndex should be 1

http://api.ubinary.com/reports/affiliate/12345/transactions.json?from=2014-10-01 00:00:00&to=2014-11-25 00:00:00&PagingIndex=1

```
{
  "HasMoreData": 1,
  "PagingIndex": 101,
  ...
}
```

Response indicates that there is more data - `HasMoreData` is 1

In the next request use PagingIndex from the response above

http://api.ubinary.com/reports/affiliate/12345/transactions.json?from=2014-10-01 00:00:00&to=2014-11-25 00:00:00&PagingIndex=101

```
{
  "HasMoreData": 0,
  "PagingIndex": 154,
  ...
}
```

Response indicates that there is no more data - `HasMoreData` is 0

#### Error response sample

```
{
  "Error": "Affiliate id 12345 is not registered"
}
```

#### Expectations
None

#### Access restrictions
- White IP list


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

## Get closed positions of a specified user

GET http://api.ubinary.com/trading/affiliate/12345/user/get/closed/positions?data=JSON_DATA

where `12345` - is your affiliate id and `JSON_DATA` is like

```C#
{
    string UserId;              // User email or user id
    DateTime From;              // from date
    DateTime To;                // to date
}
```

##### A valid request example

http://api.ubinary.com/trading/affiliate/12345/user/get/closed/positions?data={"UserId":"john@ub.com"} 

```json
{
    "UserId": "john@ub.com",
    "From": "2014-10-01 00:00:00",
    "To": "2014-11-01 00:00:00"
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
    Position[] Positions;         // array of open positions
}

enum Direction { Above, Below }

class Position
{
    int PositionId;
    string ProductName;
    decimal Symbol;
    decimal Stake;
    Direction Direction;
    DateTime StartedAt;
    DateTime ExpirationAt;
    decimal OpenRate;
    decimal CloseRate;
    decimal Payout;
    string CloseReason;
}
```

#### Successful response example

```json
{
  "TrackingId": "57.28.63",
  "ErrorCode": "Ok",
  "ErrorMessage": "",
  "Positions": [
    {
      "PositionId": 676449,
      "Asset": "GBPUSD",
      "ProductName": "Sixty seconds",
      "Stake": 40,
      "Direction": "Above",
      "StartedAt": "24-Nov-2014 08:50:04",
      "ExpirationAt": "24-Nov-2014 08:51:04",
      "OpenRate": 1.5061,
      "CloseRate": 0,
      "Payout": 0,
      "CloseReason": null
    }
  ]
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

## Get open positions of a specified user

GET http://api.ubinary.com/trading/affiliate/12345/user/get/open/positions?data=JSON_DATA

where `12345` - is your affiliate id and `JSON_DATA` is like

```C#
{
    string UserId;              // User email or user id
}
```

##### A valid request example

http://api.ubinary.com/trading/affiliate/12345/user/get/open/positions?data={"UserId":"john@ub.com"} 

```json
{
    "UserId": "john@ub.com",
}
```

http://api.ubinary.com/trading/affiliate/12345/user/get/open/positions?data={"UserId":"123456"} 

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
    Position[] Positions;         // array of open positions
}

enum Direction { Above, Below }

class Position
{
    int PositionId;
    string Asset;
    string ProductName;
    decimal Stake;
    Direction Direction;
    DateTime StartedAt;
    DateTime ExpirationAt;
    decimal OpenRate;
    decimal CloseRate;
    decimal Payout;
    string CloseReason;
}
```

#### Successful response example

```json
{
  "TrackingId": "57.28.63",
  "ErrorCode": "Ok",
  "ErrorMessage": "",
  "Positions": [
    {
      "PositionId": 676449,
      "Asset": "GBPUSD",
      "ProductName": "Sixty seconds",
      "Stake": 40,
      "Direction": "Above",
      "StartedAt": "24-Nov-2014 08:50:04",
      "ExpirationAt": "24-Nov-2014 08:51:04",
      "OpenRate": 1.5061,
      "CloseRate": 0,
      "Payout": 0,
      "CloseReason": null
    }
  ]
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

## Get trading options

GET http://api.ubinary.com/trading/affiliate/12345/user/get/trading/options?data=JSON_DATA

where `12345` - is your affiliate id and `JSON_DATA` is like

```C#
{
    string UserId;              // not supported yet
}
```

##### A valid request example

http://api.ubinary.com/trading/affiliate/12345/user/get/trading/options?data={"UserId":""} 

```json
{
    "UserId": ""
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
    Option[] Options;             // array of asset options
}

class Option
{
    string Symbol;
    Deal[] Deals;
}

class Deal
{
    int DealId;                   // Deal id (to be used in open position request)
    DateTime StartAt;             // deal start date
    DateTime EndAt;               // deal end date
    bool ExpirationIsFixed;       // if true - positions opened on this deal will expire with the deal
                                  //    false - position will expire at now + Duration
    TimeSpan Duration;            // Position duration (if expiration is not fixed)
    decimal PayMatch;             // Percents (stake) payed if positions wins
    decimal PayNoMatch;           // Percents (stake) payed if position losses
    decimal MinStake;             // Minimum stake for this deal
    decimal MaxStake;             // Maximum stake for this deal
}

```

#### Successful response example

```json
{
  "TrackingId": "87.35.06",
  "ErrorCode": "Ok",
  "ErrorMessage": "",
  "Options": [
    {
      "Symbol": "EURUSD",
      "Deals": [
        {
          "DealId": 948504,
          "StartAt": "24-Nov-2014 09:35:00",
          "EndAt": "24-Nov-2014 11:00:00",
          "ExpirationIsFixed": true,
          "Duration": "00:00:00",
          "PayMatch": 75,
          "PayNoMatch": 0,
          "MinStake": 20,
          "MaxStake": 100000
        },
        {
          "DealId": 960885,
          "StartAt": "02-Dec-2014 07:40:00",
          "EndAt": "02-Dec-2014 15:50:00",
          "ExpirationIsFixed": false,
          "Duration": "00:01:00",
          "PayMatch": 75,
          "PayNoMatch": 0,
          "MinStake": 20,
          "MaxStake": 50000
        }
      ]
    }
  ]
}
```


##### Unsuccessful response example

```json
{
  "TrackingId": "37.30.05",
  "ErrorCode": "Failed",
  "ErrorMessage": " Affiliate 111111 has no bot associated with"
}
```


#### Expectations
None

#### Access restrictions
- White IP list

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

## Open position for a specified user

GET http://api.ubinary.com/trading/affiliate/12345/user/open/position?data=JSON_DATA

where `12345` - is your affiliate id and `JSON_DATA` is like

```C#
{
    enum EAboveBelow { Above, Below }

    string SessionKey;          // Returned by a successful login   
    string UserId;              // User email or user id (both are supported)
    string UserPassword;        // User password
    int DealId;                 // A coresponding deal id (from get-trading-options)
    EAboveBelow AboveBelow;     // Position direction should be 'Above' or 'Below'
    decimal Stake;              // Position volume in USD
}
```

##### A valid request example

```json
{
    "SessionKey": "47d8fd5711b84a39a696e5c3b79241f9",
    "UserId": "john@ub.com",
    "UserPassword": "111111",
    "DealId": 948504,
    "AboveBelow": "Above",
    "Stake": 40
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
    int PositionId;               // Id of an successfully opened position
    DateTime ExpirationAt;        // Comment": "Position expiration point
}
```

##### Successful response example

```json
{
  "TrackingId": "74.77.97",
  "ErrorCode": "Ok",
  "ErrorMessage": "",
  "PositionId": 821416,
  "ExpirationAt": "24-Nov-2014 10:08:49"
}
```


##### Unsuccessful response example

```json
{
  "TrackingId": "34.29.31",
  "ErrorCode": "UxError",
  "ErrorMessage": "User 291935 (john@ub.com): login failed; password is wrong",
  "PositionId": 0,
  "ExpirationAt": "01-Jan-0001 00:00:00"
}
```


#### Expectations
- Affiliate is logged in

#### Access restrictions
- White IP list

## Register user

GET http://api.ubinary.com/trading/affiliate/12345/user/register?data=JSON_DATA

where `12345` - is your affiliate id and `JSON_DATA` is like

```C#
{
    string FirstName;           // First name
    string LastName;            // Last name
    string PhoneNumber;         // Phone number
    string Email;               // Email
    string Password;            // Password
    string LanguageCode;        // optional - user preferred language (see details below)
    ulong Tlid;                 // optional - tracking link id (64 bits)
    string FromIp;              // optional - explicit client IP, if not specified IP is taken from request
    string CountryCode;         // optional - explicit country code, if not specified country is based on IP
    string Ctag;                // optional - a free parameter; it comes back in report API
    string AdData;              // optional - a free parameter (usually information about a campaign)
	string Comment;				// optional - a registration comment
}
```

LanguageCode | Language
-------------|--------------
En           | English
Ar           | Arabic
Ru           | Russian
Fr           | French
De           | Dutch
Es           | Spanish
Cn           | Chinese


##### A valid request example

http://api.ubinary.com/trading/affiliate/12345/user/register?data=%7B%22FirstName%22:%22TestJohn%22,%22LastName%22:%22TestSmith%22,%22PhoneNumber%22:%22044-1234567%22,%22Email%22:%22test-12317@ub.com%22,%22Tlid%22:%22abcd-efgh-ighk%22,%22Password%22:%22111111%22,%22CountryCode%22:%22%22,%22FromIp%22:%22%22,%22Ctag%22:%22%22%7D

```json
{
  "FirstName": "TestJohn",
  "LastName": "TestSmith",
  "PhoneNumber": "044-1234567",
  "Email": "test-12317@ub.com",
  "LanguageCode": "en",
  "Tlid": "111222333444555666",
  "Password": "111111",
  "CountryCode": "GB",
  "FromIp": "211.148.218.20",
  "Ctag": "user.JKFDSIE3243-4V432"
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
    int UserId;                   // The id of a newly created user
}
```

##### Successful response example

```json
{
  "TrackingId": "74.77.97",
  "ErrorCode": "Ok",
  "ErrorMessage": "",
  "UserId": 299493
}
```


##### Unsuccessful response example

```json
{
  "TrackingId": "50.97.61",
  "ErrorCode": "RC_USER_ALREADY_EXISTS",
  "ErrorMessage": "Oops, something went wrong (50.97.61)",
  "UserId": 0
}
```

```json
{
  "TrackingId": "55.26.87",
  "ErrorCode": "Failed",
  "ErrorMessage": "RC_USER_ALREADY_EXISTS; email 'test-123@ub.com' is already exist"
}
```

```json
{
  "TrackingId": "50.01.14",
  "ErrorCode": "Failed",
  "ErrorMessage": "Unknown country code 'UK'"
}
```


#### Expectations
- None

#### Access restrictions
- None (public)

## Users (leads) report

Get all **changed** users between specified dates

GET http://api.ubinary.com/reports/affiliate/AFF_ID/accounts.json?from=FROM_DATE&to=TO_DATE&PagingIndex=PAGING_INDEX

where parameters are

Parameter       | Format                  | Description
----------------|-------------------------|-------------
AFF_ID          | integer                 | Your affiliate ID number
FROM_DATE       | 'yyyy-MM-dd HH:mm:ss'   | Start from this date
FROM_TO         | 'yyyy-MM-dd HH:mm:ss'   | Until this date
PAGING_INDEX    | integer                 | 1 for first request, PagingIndex from a response if its HasMoreData is true
AccountID       | integer                 | Account ID of the user


#### Response

Status | Response body
-------|--------------
200    | JSON_RESPONSE

where `JSON_RESPONSE` is like

```C#
{
    int PagingIndex;            // should be used in a consequent request
    int HasMoreData;            //     if there is more data
    Account[] Accounts;         // an array of retrieved users
}

class Account
{
    DateTime TransactionDate;   // Lead creation date
    string cTag;                // the free Ctag parameter sent with registration API
    int AccountID;              // User id
    string Type;                // 'lead' or 'user' (a user is a lead with one successful login)
    string FirstName;
    string LastName;
    string Email;               // User's email
    string CountryCode;         // User's country code (two letters ISO code)
    string SalesStatus;         // User's sales status (NotConverted, New, NoInterest, PaymentSuccessful, NoAnswer, CallInAWhile, CcClearanceFailed)
}
```

#### Successful request / response example

http://api.ubinary.com/reports/affiliate/12345/accounts.json?from=2014-10-01 00:00:00&to=2014-11-25 00:00:00&PagingIndex=1

```
{
  "HasMoreData": 0,
  "PagingIndex": 8,
  "Accounts": [
    {
      "TransactionDate": "2014-11-08 13:35:42",
      "CTag": null,
      "AccountID": 414098,
      "Type": "user",
      "FirstName": "janet",
      "LastName": "polli",
      "Email": "janetp@example.com",
      "CountryCode": "SA",
      "SalesStatus": "PaymentSuccesful"
    },
    ...
  ]
}
```

#### Paging index sample

*CAUTION:* PagingIndex is not the index of a desired page

In the first request PagingIndex should be 1

http://api.ubinary.com/reports/affiliate/12345/accounts.json?from=2014-10-01 00:00:00&to=2014-11-25 00:00:00&PagingIndex=1

```
{
  "HasMoreData": 1,
  "PagingIndex": 101,
  ...
}
```

Response indicates that there is more data - `HasMoreData` is 1

In the next request use PagingIndex from the response above

http://api.ubinary.com/reports/affiliate/12345/accounts.json?from=2014-10-01 00:00:00&to=2014-11-25 00:00:00&PagingIndex=101

```
{
  "HasMoreData": 0,
  "PagingIndex": 154,
  ...
}
```

Response indicates that there is no more data - `HasMoreData` is 0

#### Error response sample

```
{
  "Error": "Affiliate id 12345 is not registered"
}
```

#### Expectations
None

#### Access restrictions
- White IP list
