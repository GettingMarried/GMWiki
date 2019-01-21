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
                        //        For example, on "Ceremony" event, the guest is attending and required meals.
                        {
                            "event": {
                                // i.e., Ceremony
                                "id": "f8aa9d9f-7cff-497c-bba0-d836fd1fe733",
                                "title": 'Ceremony',
                                // BE constraint - To simplify, remove the unnecessary attributes (e.g., "meals") in the "event" object
                            },
                            "attending": true,
                            "requiredMeals": true,
                        }
                    ],
                    "selectedMeals": [
                        // (Note) A "selectedMeal" indicates the guest's meal preferences on the Event level.
                        //        For example (in below), on the "Ceremony" event:
                        //        - for "Starter" meal, the guest prefers a "Vegan" course; and
                        //        - for "Main" meal, the guest prefers a "Non Vegetarian" course.
                        {
                            "event": {
                                // i.e., Ceremony
                                "id": "f8aa9d9f-7cff-497c-bba0-d836fd1fe733",
                                "title": 'Ceremony',
                                // BE constraint - To simplify, remove the unnecessary attributes (e.g., "meals") in the "event" object
                            },
                            "selectedCourses": [
                                // (Note) A "selectedCourse" indicates the guest's course preference on the Meal level.
                                {
                                    "meal": {
                                        // i.e., Starter
                                        "id": "db835b62-2064-43e0-8cbf-ab061bbcc8c1",
                                        "title": "Starter",
                                        "courses": [
                                            {
                                                "id": "c79f4586-4b8d-44ea-a643-6c48dfc01b3b",
                                                "title": "Non Vegetarian",
                                            },
                                            {
                                                "id": "1fec0eb1-930a-4321-879c-b2cfef5140f2",
                                                "title": "Vegetarian",
                                            },
                                            {
                                                "id": "bfaa4a3c-9b51-41e9-8b38-036bb5a29735",
                                                "title": "Vegan",
                                            },
                                        ]
                                    },
                                    // BE constraint - if no "course" is selected, default to the first one.
                                    "course": {
                                        // i.e., Vegan
                                        "id": "bfaa4a3c-9b51-41e9-8b38-036bb5a29735"
                                        // BE constraint - To simplify, remove the unnecessary attributes (e.g., "title") in the "course" object
                                    }
                                },
                                {
                                    "meal": {
                                        // i.e., Main
                                        "id": "863157e0-b098-439d-94f5-8502143ae7a7",
                                        "title": "Main",
                                        "courses": [
                                            {
                                                "id": "d507d771-348b-46be-a2d5-201d20872775",
                                                "title": "Non Vegetarian",
                                            },
                                            // ...
                                        ]
                                    },
                                    "course": {
                                        // i.e., Non Vegetarian
                                        "id": "d507d771-348b-46be-a2d5-201d20872775"
                                    }
                                },
                            ],
                        },
                        // ...
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