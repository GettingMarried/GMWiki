```jsonc
{
    // BE constraint - check the website editor information to see if the RSVP block is visible to guests
    "isRsvpActive": true,
    "guestsAttending": 11,
    "guestsNotAttending": 1,
    // FE constraint - If this array is empty, the user doesn't have an event created;
    // prompt them to create an event
    "attendingSummary": [
        {
            "label": "Ceremony",
            "total": 8,
        },
        {
            "label": "Reception",
            "total": 11,
        },
    ],
    "filter": [
        { 
            // These will populate from the BE from the list of events; the only two constants will be the
            // 'Attending' and 'Not Attending' at the bottom but even they will be sent over from the BE.
            "title": "Ceremony",
            "selected": false,
            "location": {
                "filter": "ceremony",
                "page": 2,
            },
        },
        {
            "title": "Reception",
            "selected": false,
            "location": {
                "filter": "reception",
                "page": 2,
            },
        },
        {
            "title": "Stag do",
            "selected": false,
            "location": {
                "filter": "stag_do",
                "page": 2,
            },
        },
        {
            "title": "Not attending",
            "selected": false,
            "location": {
                "filter": "not_attending",
                "page": 2,
            },
        },
        {
            "title": "All guests",
            "selected": true,
            "location": {
                "filter": null,
                "page": 2,
            },
        },
    ],
    // FE constraint - If this list is empty AND the user has created an event, 
    // render a message prompting them to add users
    "guests": [
        // multiple instances of Guest would come in here
        // TBD - still on discussion
    ],
    "guestsDownload": "https://gettingmarried.co.uk/20190101-your-list.xls"
}
```