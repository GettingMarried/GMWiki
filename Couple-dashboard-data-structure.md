# Initial state

Backend to provide the data structure as initial state in window object and front-end to consume it

```js
// (Note) "dashboardState" object is a site-wide configuration
// It is used on all pages for logged-in users as it is required for the menu.
// 
// (Note) the object should be "null" if the user is not logged in
window.GettingMarried.dashboardState = { /** couple dashboard data structure */ };

// // "initialState" deals with the main application we have on the specific page
// window.GettingMarried.initialState = { /** main application data structure, e.g, website editor */ };

```

**Note:** ideally, we could eventually do away with the `window` object and just inject what we need from the server (https://github.com/AmpersandHQ/gettingmarried/issues/202)

# Data structure

```jsonc
// (Note) "null" or "undefined" if the user is not logged in
{
    // (Note) participant1_preferred_name and participant2_preferred_name joint together by an "&"
    // (BE Constraint) On registration, the preferred names are resolved from first names and persisted
    "coupleName": "Emily & Archie",
    // (BE Constraint) Resolved logout url from route
    "logoutUrl": "https://gettingmarried.co.uk/logout",
    // (BE constraint) Create a service to resolve this url. For now, resolve as "/wedding/guest/{wedding-uuid}"
    // (Note) null, if site is not live
    "siteUrl": "http://emily-and-archie.are.gettingmarried.co.uk",
    // (FE constraint) if `siteLive` is false, don't show the 'View Site' button
    // (BE constraint) Resolve from "websiteLive" wedding attribute
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
}
```