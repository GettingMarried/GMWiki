# Initial state

Backend to provide the data structure as initial state in window object and front-end to consume it

```js
// "initialState" deals with the main application we have on the specific page
window.GettingMarried.initialState = /** website settings object defined below */;
```

# Data structure
```jsonc
{
    // (FE constraint) When toggle to true, send a PUT request to "/api/wedding/me/putWebsiteLive"
    // (FE constraint) When toggle to false, send a PUT request to "/api/wedding/me/putWebsiteOffline"
    // (Note) It is separated in two endpoints to avoid doing PATCH request against wedding
    //        which is less meaningful to this use case
    // (BE constraint) Resolve from wedding "websiteLive" attribute
    // (Note) "true" if website is live (i.e., visible to guest)
    isLive: true,
}
```