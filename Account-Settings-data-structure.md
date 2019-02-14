# Initial state

Backend to provide the data structure as initial state in window object and front-end to consume it

```js
// "initialState" deals with the main application we have on the specific page
window.GettingMarried.initialState = /** account setting object defined below */;
```

# Account settings

```jsonc
// Account settings
{
    // (Note) Password reset endpoint is hard-coded on react app endpoint mapping config
    //        It is "/api/users/me/resetPassword"
    // (BE constraint) Unix timestamp(s) in the server local timezone
    nextBillingDate: 1550073197,
    // (FE constraint) Show a message confirming that all current Packages Subscribed to are Free
    // (BE constraint) "true" if there is any billable package subscribed in the account
    //                 As package's prices are no longer editable after once it has ever be subscribable,
    //                 it is safe to resolve by looking at the subscribed package current prices
    isBillable: true,
    // (Note) It is possible that at the same time isBillable=false and hasBillingHistory=true
    //        where the user might have paid for billable package before and later on downgraded to free package
    // (FE constraint) Show "billing history" link if it is true
    // (BE constraint) "false" if stripe has never issued invoices
    hasBillingHistory: true,
    // (Note) Payment history comes from Stripe through separate GM API call
    // (Note) Account cancel endpoint is hard-coded on react app endpoint mapping config
}
```

# Billing History

```jsonc
// GET: /api/weddings/me/invoices
[
    {
        "date": 1532700031,
        "reference": 'in_1CsWUdAN9tOdQHyBEeUptyr7',
        "currency": "gbp",
        "amount": 9.99,
        "paid": true,
    },
]
```