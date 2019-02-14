```jsonc
{
    // (FE constraint) When toggle to true, send a POST request to "/api/wedding/me/putWebsiteLive"
    // (FE constraint) When toggle to false, send a POST request to "/api/wedding/me/putWebsiteOffline"
    // (BE constraint) Resolve from wedding "websiteLive" attribute
    // (Note) "true" if website is live (i.e., visible to guest)
    isLive: true,
}
```