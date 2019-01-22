```jsonc
{
    // BE constraint - check the website editor information
    //                 to see if the RSVP block is visible to guests
    "isRsvpActive": true,
    "guestsAttending": 11,
    "guestsNotAttending": 1,
    // FE constraint - If this array is empty,
    //                 the user doesn't have an event created;
    //                 prompt them to create an event
    "attendingSummaries": [
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
        // BE constraint - "All guests" is hard-coded
        {
            "title": "All guests",
            "selected": true,
            "location": {
                "filter": null,
                "page": 2,
            },
        },
        // BE constraint - These (ceremony, reception, etc) will be populated dynamically
        //                 from the list of events;
        {
            "title": "Ceremony",
            "selected": false,
            // BE constraint - the "location" offers FE metadata to generate a filter link
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
        // BE constraint - "Not attending" is hard-coded
        {
            "title": "Not attending",
            "selected": false,
            "location": {
                "filter": "not_attending",
                "page": 2,
            },
        },
    ],
    // FE constraint - If this list is empty AND the user has created an event,
    // render a message prompting them to add users
    "rsvps": [
        {
            // (Note) Unix timestamp
            "dateReceived": 1547648282,
            "guests": [
                {
                    // FE constraint - this can be used for removing or updating guests
                    "id": 'c5850948-8169-4e7f-b347-6eadf261a7d8',
                    "name": 'Jake Critchlow',
                    "email": 'jc@amp.co',
                    "telephone": '01612365504',
                    "attendances": [
                        // (Note) An "attendance" indicates the guest's attendance metadata.
                        //        For example (in below), on "Ceremony" event,
                        //        the guest is attending and required meals.
                        {
                            // BE constraint - Event is populated and retrieved from database.
                            //                 No modification is needed
                            "event": {
                                // i.e., Ceremony
                                "id": "f8aa9d9f-7cff-497c-bba0-d836fd1fe733",
                                "title": 'Ceremony',
                                "meals": [
                                    // (Note) Meal is an Value Object and for now they are hard-coded
                                    //        as "Starter", "Main", and "Dessert". (out of scope -
                                    //        allowed to extend in the future)
                                    {
                                        // i.e., Starter
                                        "title": "Starter",
                                        // (Note) (Out of Scope) choices are configurable by Couple
                                        "choices": [
                                            "Non Vegetarian",
                                            "Vegetarian",
                                            "Vegan",
                                        ]
                                    },
                                    {
                                        "title": "Main",
                                        // ...
                                    },
                                    {
                                        "title": "Dessert",
                                        // ...
                                    },
                                ],
                            },
                            "attending": true,
                            "requiredMeals": true,
                            // (Note) A "selectedMeal" indicates the guest's meal preferences
                            //        for the Event level.
                            //        For example (in below), in the "Ceremony" event:
                            //        - for "Starter" meal, the guest prefers a "Vegan" course; and
                            //        - for "Main" meal, the guest prefers a "Non Vegetarian" course.
                            "selectedMeals": [
                                // (Note) A "selectedCourse" indicates the guest's course preference
                                //        on the Meal level.
                                {
                                    "course": "Starter",
                                    // BE constraint - if no "course" is selected, default to the first one.
                                    "choice": "Vegan",
                                },
                                {
                                    "course": "Main",
                                    "choice": "Non Vegetarian",
                                },
                            ],
                        },
                    ],
                },
                //...
            ]
        },
        // ...
    ],
    "guestsDownload": "https://gettingmarried.co.uk/20190101-your-list.xls"
}
```