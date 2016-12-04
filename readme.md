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

