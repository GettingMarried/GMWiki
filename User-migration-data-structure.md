## User migration data structure

Version: 3.0.0

Please maintain a version number (above) on update to keep a reference for communication.

Reference: https://ampersand.atlassian.net/browse/GETMARRIED-519

**Endpoint: /api/userMigration**

The old GM is expected to send a user migration request to force / upon user migration. The data structure is defined in below format. The new GM should then create an user and migrate the data, mainly for wedding website, defined in: https://github.com/AmpersandHQ/gettingmarried/pull/181/

### Migrate multiple objects at once

For NDJSON specification, please see: https://github.com/ndjson/ndjson-spec#3-functional-specification

```jsonc
// Content-Type: application/x-ndjson
//
{ /** user migration object 1 */ }
{ /** user migration object 2 */ }
// more objects (delimited by new line char "\n" or "\n\r") ...
```

### Migrate single object

```jsonc
// Content-Type: application/json
//
// (IMPORTANT) Migration object (below) is on "wedding" account level.
// That is, multiple users who below to the same wedding account, must be migrated at once.
// Splitting up migration of the same wedding account for different users will result in
// creating multiple wedding account.
//
// Http Endpoint: (Tentative - to be confirmed) https://gettingmarried.co.uk/api/userMigration
//
// Http Method: POST
//
// On success, a 200 http response code will be returned
// On error, a 4xx http response code will be returned (the exact error codes are to be confirmed)
{
    "users": [
        // (Note) Mulitiple users are allowed and they are not necessary participants (e.g., wedding planner)
        {
            // (Note) Identity provider id - unique identifier in Auth0
            "id": "auth0|g67sd876sd6dfg8sg6",
            // (Note) Marketing email
            "email": "ben.aimes@htomail.com",
            // (Note) Marketing and synchronising to mailchimp based on opt-in state
            "marketingOptIn": {
                "email": true
            }
        }
    ],
    // (Note) Participants' givenName, familyName, and preferredName are meatadata used for personalising content
    // They will be persisted in the new GM for further usage. "profile" and "image" however populate against
    // "about us" block only.
    "participant1": {
        "givenName": "Benjamin",
        "familyName": "Aimes",
        // (Note) Name shows in the "about us" block
        "preferredName": "Ben",
        // (Note) Description to put into "about us" block
        "profile": "Ben loves nothing more than cosy nights in the sofa ...",
        // (Note) Image to be persisted in the new GM and used in the "about us" block
        "image": "https://ui-avatars.com/api/?name=Benjamin+Aimes&rounded=true&size=300&color=ffffff&background=3d5afe"
    },
    "participant2": {
        "givenName": "Jennifer",
        "familyName": "Grubb",
        "preferredName": "Jen",
        "profile": "Jen loves travelling ...",
        "image": "https://ui-avatars.com/api/?name=Jennifer+Grubb&rounded=true&size=300&color=000000&background=ce93d8"
    },
    // (Note) Datetime uses in the "countdown clock" block
    // (Note) Unix timestamp in precision down to seconds (For example: 0 = UTC 1970-01-01 00:00:00; 55815 = UTC 1970-01-01 15:30:15)
    "weddingDatetime": 1570752000,
    "websiteSetting": {
        // (Note) Metadata to specify if the wedding website can be indexed by search engine
        "indexable": false,
        // (Note) Metadata to specify custom domain setup
        "subDomain": "bennyandjenny",
        "primaryDomain": "ourdayinhistory.co.uk"
    },
    // (Note) If yes, "countdown clock" is set to published (i.e., visible to guest)
    "showCountdown": true,
    // (Note) (Out of scope) Texts *potentially* become "custom-text-block" in the new wedding website;
    // as the list of free package features are not decided and it is unsure if it includes below three blocks,
    // migration of them is currently out of scope.
    // "texts": [
    //     {
    //         // site_intro_text
    //         "title": "Introduction",
    //         "content": "We\u0026#39;re getting married! ..."
    //     },
    //     {
    //         // how_we_met_text
    //         "title": "How we met",
    //         "content": "As most of you know ..."
    //     },
    //     {
    //         // proposal_text
    //         "title": "Proposal text",
    //         "content": "It was a lovely ..."
    //     }
    // ],
    "events": [
        // (Note) Data used for creating a "ceremony" block
        {
            "type": "ceremony",
            // (Note) Unix timestamp in precision down to seconds (For example: 0 = UTC 1970-01-01 00:00:00; 55815 = UTC 1970-01-01 15:30:15)
            "datetime": 1570806000,
            "location": {
                "name": "Rivington Hall Barn",
                "addressLines": [
                    "33 Rivington Drive",
                    "Bolton"
                ],
                "postCode": "BL1 2AB",
                // ISO 3166-1 alpha-2
                "country": "GB",
                "coords": {
                    "lat": 53.578474,
                    "lng": -2.429915
                }
            },
            "description": "We have chosen the most beautiful location in Bolton - Rivington Hall Barn, situated perfectly to watch the sunset. We have the privilege of saying our vows on the spa roof terrace overlooking the sea with all of you beautiful people up there with us. Rivington Hall Barn is the perfect blend of style and substance, we chose it knowing it was perfect for us.",
        },
        // (Note) Data used for creating a "reception" block
        {
            "type": "reception",
            // (Note) Unix timestamp in precision down to seconds (For example: 0 = UTC 1970-01-01 00:00:00; 55815 = UTC 1970-01-01 15:30:15)
            "datetime": 1570806000,
            "location": {
                "name": "Rivington Hall Barn",
                "addressLines": [
                    "33 Rivington Drive",
                    "Bolton"
                ],
                "postCode": "BL1 2AB",
                //ISO 3166-1 alpha-2
                "country": "GB",
                "coords": {
                    "lat": 53.578474,
                    "lng": -2.429915
                }
            },
            "description": "We have chosen the most beautiful location in Bolton - Rivington Hall Barn, situated perfectly to watch the sunset. We have the privilege of saying our vows on the spa roof terrace overlooking the sea with all of you beautiful people up there with us. Rivington Hall Barn is the perfect blend of style and substance, we chose it knowing it was perfect for us."
        },
    ]
}
```