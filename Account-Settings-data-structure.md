# Account settings

```js
// Account settings
window.GettingMarried.initialState = {
    // (Note) Password reset endpoint is hard-coded on react app endpoint mapping config
    //        It is "/api/users/me/changePassword"
    // (BE constraint) Unix timestamp(s) in the server local timezone
    nextBillingDate: 1550073197,
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