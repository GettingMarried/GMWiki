## Proposed data structure (NOT CONFIRMED YET)

```jsonc
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
            "preferredName": "Ben",
            // Question: What is a profile?
            "profile": "aaa aaa",
            //S3 url
            "image": "https://"
        },
        {
            "givenName": "Jennifer",
            "familyName": "Grubb",
            "preferredName": "Jen",
            //text
            "profile": "aaa aaa",
            //s3 url
            "image": "https://"
        }
    ],
    // Unix timestamp (For example: 0 = UTC 1970-01-01)
    "weddingDate": 1570752000,
    "websiteSettings": {
        "indexableSeo": false,
        "domain": {
            "sub": "bennyandjenny",
            "primary": "ourdayinhistory.co.uk"
        }
    },
    "showCountdown": true,
    // Texts potentially become "custom-text-block" in the new wedding website
    "texts": [
        {
            // site_intro_text
            "title": "Introduction",
            "content": "We\u0026#39;re getting married! ..."
        },
        {
            // how_we_met_text
            "title": "How we met",
            "content": "As most of you know ..."
        },
        {
            // proposal_text
            "title": "Proposal text",
            "content": "It was a lovely ..."
        }
    ],
    "events": [
        {
            "title": "Ceremony",
            // Unix timestamp (For example: 0 = UTC 1970-01-01)
            "weddingDate": 1570806000,
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
        {
            "title": "Reception",
            // Unix timestamp (For example: 0 = UTC 1970-01-01)
            "weddingDate": 1570806000,
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