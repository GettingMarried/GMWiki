This wiki documents the data structure to allow the below endpoint to process a RSVP request

High level use case:

```gherkin
Given a wedding with id 88f06170-3454-11e9-b210-d663bd873d93) is set up
And the wedding website has a RSVP block
When a guest visit the website
And the guest submits a RSVP
Then the RSVP data is sent to "/api/weddings/88f06170-3454-11e9-b210-d663bd873d93/submitRsvp"
And the endpoint has created guests, attendances and message according to the RSVP data
```

# Data structure

```jsonc
// POST /api/weddings/88f06170-3454-11e9-b210-d663bd873d93/submitRsvp
{
  "guests": [
    {
      // (FE constraint) - Leave "id" null
      // (BE constraint) - It is automatically populated by doctrine on persist
      "id": null,
      "createdAt": 1547648282,
      // (FE constraint) - Leave "creationId" null
      // (BE constraint) - Populate "creationId" (e.g., 35aed302-c987-4235-96e1-31391bcdda8c)
      //                   It should be same to all guests in the same request
      // (Note) - to allow guests grouped in guest list
      "creationId": null,
      "name": "Jake Critchlow",
      "email": "jc@amp.co",
      "telephone": "01612365504",
      "attendances": [
        {
          // (FE constraint) Populate "event" based on:
          //                  - weddingId
          //                  - eventId
          //                  - The API route from config.json
          //                 Pattern: /api/weddings/%weddingId%/events/%eventId%
          //                 where anything within %% signs is to be String.replace()d.
          "event": "/api/weddings/88f06170-3454-11e9-b210-d663bd873d93/events/f8aa9d9f-7cff-497c-bba0-d836fd1fe733",
          "attending": true,
          "requiredMeals": true,
          "selectedMeals": [
            { "course": "Starter", "choice": "Vegan" },
            { "course": "Main", "choice": "Non Vegetarian" },
          ],
        },
      ],
    },
    { /** guest 2 */ },
    // ...
  ],
  "message": {
    // (FE constraint) - Leave "id" null
    // (BE constraint) - It is automatically populated by doctrine on persist
    "id": null,
    // (Note) "type" is for general purpose. It distinguishes between
    //        RSVP and contact form (contact-form)
    "type": "rsvp",
    // (Note) Unixtime
    "dateReceived": 1547047313,
    // (BE constraint) Make sure this flag is always false
    "read": false,
    // (FE Constraint) Resolve from respondent fields
    "sender": "Jake Critchlow",
    "senderEmail": "jc@amp.co",
    "content": "Hi guys, just a quick question about the nearest accommodation to the wedding venue...",
    "additionalGuests": 1,
  }
}
```