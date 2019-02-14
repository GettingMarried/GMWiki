# Initial state

Backend to provide the data structure as initial state in window object and front-end to consume it

```js
// "initialState" deals with the main application we have on the specific page
window.GettingMarried.initialState = /** guest management overview object defined below */;
```

# Data structure
```jsonc
// Guest management
{
    // (Note) participant1_preferred_name and participant2_preferred_name joint together by an "&"
    // (BE Constraint) On registration, the preferred names are resolved from first names and persisted
    // (See Couple Dashboard data structure)
    "coupleName": "Emily & Archie",
    // (Note) Unix timestamp in the server timezone
    // (BE constraint) Resolve from weddingDate attribute
    "weddingDate": 1234567890,
    "inbox": {
        // 
        "unreadMessages": 2,
        "link": "https://gettingmarried.co.uk/guestManagement/inbox"
    },
    "guestList": {
        "guestsAttending": 11,
        "link": "https://gettingmarried.co.uk/guestManagement/guestList"
    },
}
```