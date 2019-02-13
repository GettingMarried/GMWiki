```js
// site-wide configuration
// to be used on all pages for logged-in users as it is required for the menu
// @to discuss - how will we get this information?
window.GettingMarried.initialState.dashboard = {
    "coupleName": "Emily & Archie",
    "logoutUrl": "https://gettingmarried.co.uk/logout",
    // BE constraint - If site is not live, this URL is not needed.  
    "siteUrl": "http://emily-and-archie.are.gettingmarried.co.uk",
    // FE constraint - if `siteLive` is false, don't show the 'View Site' button
    "siteLive": false,
    "navigation": [
        {
            "title": "Website Editor",
            "url": "https://gettingmarried.co.uk/wedding/couple",
        },
        {
            "title": "Website Settings",
            "url": "https://gettingmarried.co.uk/websiteSettings",
        },
        {
            "title": "Guest Management",
            "url": "https://gettingmarried.co.uk/guestManagement",
        },
        {
            "title": "My Subscription",
            "url": "https://gettingmarried.co.uk/mySubscription",
        },
        {
            "title": "Account Settings",
            "url": "https://gettingmarried.co.uk/accountSettings",
        },
    ],
};
```