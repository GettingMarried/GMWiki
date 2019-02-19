```jsonc
// POST /api/weddings/88f06170-3454-11e9-b210-d663bd873d93/submitRsvp
{
    "guests": [
        {
            // FE constraint - this can be used for removing or updating guests
            // BE constraint - BE to populate
            "id": "c5850948-8169-4e7f-b347-6eadf261a7d8",
            "createdAt": 1547648282,
            // BE constraint - Populated by BE on creation
            // BE constraint - The same creationId should be provided to all guests
            //                 sent in one request
            "creationId": "35aed302-c987-4235-96e1-31391bcdda8c",
            "name": "Jake Critchlow",
            "email": "jc@amp.co",
            "telephone": "01612365504",
            "attendances": [
                {
                // FE constraint - Need to generate this ID based off:
                //               - The wedding ID
                //               - The event ID
                //               - The API route from config.json
                //               This will be something like /api/weddings/%weddingId%/events/%eventId% 
                //               where anything within %% signs is to be String.replace()d.
                "event": "/api/weddings/88f06170-3454-11e9-b210-d663bd873d93/events/f8aa9d9f-7cff-497c-bba0-d836fd1fe733",
                "attending": true,
                "requiredMeals": true,
                "selectedMeals": [
                        {
                            "course": "Starter",

                            "choice": "Vegan",
                        },
                        {
                            "course": "Main",
                            "choice": "Non Vegetarian",
                        },
                    ],
                }, 
            ],
        }
    ],
    // (BE Constraint) This uses the same class as the individual Message for the 
    //                 Inbox view to make sure the data is consistent
    "message": {
        // (BE constraint) Back-end will populate this. 
        //                 Have fun, lads ;) 
        "id": null,
        // (Note) General purpose - distinguish between
        //        RSVP and contact form (contact-form)
        "type": "rsvp",
        // (Note) Unixtime
        "dateReceived": 1547047313,
        // (BE Constraint) Is this really needed for messages/RSVPs that are 
        //                 sent from RSVP? To be considered if it is needed. 
        // (FE Constraint) Leave as null - BE will fix this when they receive the
        //                 data and populate as required
        "read": null,
        "sender": "Jake Critchlow",
        // (FE Constraint) Resolve from respondent fields
        "senderEmail": "jc@amp.co",
        // (FE Constraint) Leave unpopulated so this can be
        //                 provided by BE
        // (BE Constraint) To be populated when the form data
        //                 is received
        "receiver": "Emily & Archie",
        "content": "Hi guys, just a quick question about the nearest accommodation to the wedding venue...",
        "additionalGuests": 1,
    }
}
```