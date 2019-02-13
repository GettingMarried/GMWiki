# Account settings

```js
// Account settings
window.GettingMarried.initialState = {
    // FE constraint - these live in different sections, they'll all need to be hard-coded. 
    "changePasswordLink": "https://gettingmarried.co.uk/account/changePassword",
    // BE constraint - Unix timestamp(s) - @to discuss, how does time work
    // BE constraint - payment list comes from Stripe, separate API call
    nextBillingDate: 1550073197,
}
```

# Billing History

```jsonc
// GET: /api/wedding/me/invoices
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