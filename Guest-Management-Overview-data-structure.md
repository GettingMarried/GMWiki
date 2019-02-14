# Initial state

Backend to provide the data structure as initial state in window object and front-end to consume it

```js
// "initialState" deals with the main application we have on the specific page
window.GettingMarried.initialState = /** account setting object defined below */;
```

# Data structure
```jsonc
// Guest management
{
    "coupleName": "Emily & Archie",
	// Unix timestamp
    "weddingDate": 1234567890,
    "inbox": {
        "unreadMessages": 2,
        "link": "https://gettingmarried.co.uk/guestManagement/inbox"
    },
    "guestList": {
        "guestsAttending": 11,
        "link": "https://gettingmarried.co.uk/guestManagement/guestList"
    },
}
```