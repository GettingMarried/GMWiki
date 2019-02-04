## User migration data structure

**Endpoint: /api/userMigration**

The old GM is expected to send a user migration request to force / upon user migration. The data structure is defined in below format. The new GM should then create an user and migrate the data, mainly for wedding website, defined in: https://github.com/AmpersandHQ/gettingmarried/pull/176/

### Migrate multiple objects at once

```jsonc
// Content-Type: application/ld+json
[
    { /** user migration object 1 */ },
    { /** user migration object 2 */ },
    // ...
]
```

### Migrate single object

```jsonc
// Content-Type: application/json
{
    "users": [
        // (Note) Mulitiple users are allowed and they are not necessary participants (e.g., wedding planner)
        {
            // Identity provider id - unique identfier in Auth0
            "id": "auth0|g67sd876sd6dfg8sg6",
            // Login email
            "email": "ben.aimes@htomail.com",
            "marketingOptIn": {
                "email": true
            }
        }
    ],
    "participants": [
        {
            "givenName": "Benjamin",
            "familyName": "Aimes",
            // (Note) Name shows in the "about us" block
            "preferredName": "Ben",
            // (Note) Description to put into "about us" block
            "profile": "Ben loves nothing more than cosy nights in the sofa ...",
            // (Note) Image to be presisted in the new GM and used in the "about us" block
            "image": "https://ui-avatars.com/api/?name=Benjamin+Aimes&rounded=true&size=300&color=ffffff&background=3d5afe"
        },
        {
            "givenName": "Jennifer",
            "familyName": "Grubb",
            "preferredName": "Jen",
            "profile": "Jen loves travelling ...",
            "image": "https://ui-avatars.com/api/?name=Jennifer+Grubb&rounded=true&size=300&color=000000&background=ce93d8"
        }
    ],
    // (Note) Datetime uses in the "countdown clock" block
    // (Note) Unix timestamp in precision down to seconds (For example: 0 = UTC 1970-01-01 00:00:00; 55815 = UTC 1970-01-01 15:30:15)
    "weddingDatetime": 1570752000,
    "websiteSetting": {
        // (Note) Metadata to specify if the wedding website can be indexed by search engine
        "indexable": false,
        "domain": {
            "sub": "bennyandjenny",
            "primary": "ourdayinhistory.co.uk"
        }
    },
    // (Note) If yes, "countdown clock" is set to published
    "showCountdown": true,
    // (Note) Texts *potentially* become "custom-text-block" in the new wedding website; as we only migrate free package features and we don't know if it includes below blocks, they are out of scope for now.
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