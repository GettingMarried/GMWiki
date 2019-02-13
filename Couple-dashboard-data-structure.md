```js
// site-wide configuration
// to be used on all pages for logged-in users as it is required for the menu
window.GettingMarried.dashboardState = {
    "coupleName": "Emily & Archie",
    "logoutUrl": "/auth0/logout",
    // BE constraint - If site is not live, this URL is not needed.  
    "siteUrl": "http://emily-and-archie.are.gettingmarried.co.uk",
    // FE constraint - if the `currentPage` is null, don't show the close button - 
    // if the user has opened the dashboard from a page, make sure it appears
    // as if it were a modal
    // Hopefully we don't need this...
    "currentPage": null,
    // BE constraint - If `unreadMessages` from the Inbox is greater than 0. 
    // Don't need to worry about this state being updated until page refresh.
    "newMessages": true,
    // BE constraint - If `unreadMessages` from the Inbox is greater than 0, 
    // AND `unreadMessages` from `RSVP` are greater than 0. 
    // Don't need to worry about this state being updated until page refresh.
    "newRsvps": false,
    // FE constraint - if `siteLive` is false, don't show the 'View Site' button
    "siteLive": false,
};
```