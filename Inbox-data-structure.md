This wiki temporarily keeps the data structure design for inbox. When the ticket is finish, we should move it to the bundle's readme and remove this wiki.

```json
// /guestManagement/inbox/?page=2&filter=rsvp

{
    "unreadMessage": 2,
    "totalMessage": 103,
    "filter": [
        {
            "title": "RSVP",
            "selected": false,
            "location": {
                "filter": "rsvp",
                "page": 2,
            },
        },
        {
            "title": "Contact Form",
            "selected": false,
            "location": {
                "filter": "contact-form",
                "page": 2,
            },
        },
        {
            "title": "Showing All",
            "selected": true,
            "location": {
                "filter": null,
                "page": 2,
            },
        },
    ],
    "messages": [
        // (Note) Contact form
        {
            "id": "00000000-0000-1000-8000-000000000000",
            "type": "contact-form",
            // (Note) Unixtime
            "dateReceived": 1547047313,
            "read": true,
            "sender": "Joe Bloggs",
            "senderEmail": "jb@amp.co",
            "content": "Hi Emily & Archie,<br /><br />You received a message...",
        },
        // (Note) Rsvp
        {
            //... Exactly the same as contact form, except for the type really for now
            "type": "rsvp",
        },
    ],
    "pagination": {
        "prevPage": {
            "title": "Previous Page",
            "location": {
                "filter": "rsvp",
                "page": 1,
            },
        },
        "nextPage": {
            "title": "Next Page",
            "location": {
                "filter": "rsvp",
                "page": 3,
            },
        },
    },
}

// /api/inbox/?page=2&filter=rsvp
// should return extactly the same JSON as normal http request

```