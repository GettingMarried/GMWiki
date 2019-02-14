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