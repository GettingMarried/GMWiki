This wiki temporarily keeps the data structure design for inbox. When the ticket is finish, we should move it to the bundle's readme and remove this wiki.

```json
// /guestManagement/inbox/?page=2&filter=rsvp

{
    "unreadMessages": 2,
    "totalMessages": 103,
    "filter": [
        {
            // (BE Constraint) Populate it according to the supplied parameters
            "title": "RSVP",
            "selected": true,
            "location": {
                "filter": "rsvp",
                "page": 2,
            },
        },
        {
            // (Note) Location's page number will reset when we select a new filter
            "title": "Contact Form",
            "selected": false,
            "location": {
                "filter": "contact-form",
                "page": 1,
            },
        },
        {
            "title": "Showing All",
            "selected": false,
            "location": {
                "filter": null,
                "page": 1,
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
            "receiver": "Emily & Archie",
            "content": "Hi guys, just a quick question about the nearest accommodation to the wedding venue...",
        },
        // (Note) Rsvp
        {
            // (Note) Exactly the same as contact form, except for the type and type specific data (e.g., additionalGuests)
            "type": "rsvp",
            // (Note) Type specific data
            // (Note) For FE to populate the text "Their RSVP details have been added to your guest list along with their additional [$additionalGuests] guest(s)."
            "additionalGuests": 1,
        },
    ],
    "pagination": {
        "prevPage": {
            "title": "Previous Page",
            // (Note) Location can be null if pagination is not possible (e.g. prevPage.location on page 1)
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