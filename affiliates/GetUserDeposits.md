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
