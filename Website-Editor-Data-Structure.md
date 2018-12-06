This wiki documents the JSON data structure in wedding website (i.e., for both couple view and guest view). BE and FE should follow this skeleton.

When it comes to implement the actual features, we may identify needs to refactor a bit. When it happens, please discuss with Lyndsey (or Torrey) to review and update it.

Related Tickets:
- [GETMARRIED-396](https://ampersand.atlassian.net/browse/GETMARRIED-396)
- [GETMARRIED-128](https://ampersand.atlassian.net/browse/GETMARRIED-128)


```jsonc
{
    // Couple view data
    // (BE - Skeleton Constraint) only show up on couple view
    "editPanel": {
        // Identify what packages are subscribed / purchased (i.e., can be used by the couple)
        // If a package is subscrited, it shows up in the list; otherwise not.
        // (BE - Subscription Constraint) Populate this data base on subscription status
        "subscriptions": [
            "free",
            "creative",
        ],
        // Contains grouped information of [Theme, Colour Palette, Typography] and mapped by packages
        "themePackages": {
            // E.g., Free Package Theme
            // (BE - Subscription Constraint) Populate all subscribable packages provided by different bundles
            "free": {
                "title": "Basis Themes",
                "description": "",
                // each theme within the package resides here
                // (BE - Subscription Constraint) Populate all theme prototypes provided by the same package from different bundles
                "items": [
                    {
                        "name": "rustic",
                        // name of the palette should be unique; this ensures we get the correct stylesheet for the structure
                        // (BE - Skeleton Constraint) Make sure this is unique
                        "selected": false,
                        // each theme has multiple pre-determined palettes
                        "palettes": [
                            {
                                // each palette has the colours in a set order;
                                // these will be applied with styled-components
                                // on the frontend so we don't need to fret about
                                // stylesheets
                                "name": "palette-1",
                                "selected": false,
                                "colours": [
                                    "#00F",
                                    "#FF0"
                                ]
                            },
                            {
                                "name": "palette-2",
                                "selected": false,
                                "colours": [
                                    "#BBB",
                                    "#CCC"
                                ]
                            },
                            {
                                "name": "palette-3",
                                "selected": false,
                                "colours": [
                                    "#ABA",
                                    "#BAB"
                                ]
                            },
                        ],
                        "typographies": [
                            {
                                "title": "Arial",
                                "fontFamily": "Arial,sans-serif",
                                "fontSize": 12,
                                "lineHeight": 6
                            },
                            {
                                "title": "Bromello Script",
                                "fontFamily": "'Bromello Script',cursive",
                                "fontSize": 18,
                                "lineHeight": 6
                            },
                        ],
                    },
                    {
                        "name": "contemporary",
                        "selected": false,
                        "palettes": [
                            {
                                "name": "palette-1",
                                "selected": false,
                                "colours": [
                                    "#000",
                                    "#FFF"
                                ]
                            },
                            {
                                "name": "palette-2",
                                "selected": false,
                                "colours": [
                                    "#AAA",
                                    "#777"
                                ]
                            },
                            {
                                "name": "palette-3",
                                "selected": false,
                                "colours": [
                                    "#F00",
                                    "#0F0"
                                ]
                            },
                            {
                                "name": "custom",
                                "selected": false,
                                "colours": [
                                    "#ABA",
                                    "#BAB"
                                ]
                            },
                        ],
                        "typographies": [
                            {
                                "title": "Arial",
                                "fontFamily": "Arial,sans-serif",
                                "fontSize": 12,
                                "lineHeight": 6
                            },
                            {
                                "title": "Bromello Script",
                                "fontFamily": "'Bromello Script',cursive",
                                "fontSize": 18,
                                "lineHeight": 6
                            },
                        ],
                    }
                ]
            },
            "creative": {
                "title": "Premium Themes",
                "description": "Bla bla bla",
                "items": [
                    {
                        "name": "minimal",
                        "selected": false,
                        "palettes": [
                            {
                                "name": "palette-1",
                                "selected": false,
                                "colours": [
                                    "#00F",
                                    "#FF0"
                                ]
                            },
                            {
                                "name": "palette-2",
                                "selected": false,
                                "colours": [
                                    "#BBB",
                                    "#CCC"
                                ]
                            },
                            {
                                "name": "palette-3",
                                "selected": false,
                                "colours": [
                                    "#ABA",
                                    "#BAB"
                                ]
                            },
                            {
                                "name": "custom",
                                "selected": false,
                                "colours": [
                                    "#ABA",
                                    "#BAB"
                                ]
                            },
                        ],
                        "typographies": [
                            {
                                "title": "Arial",
                                "fontFamily": "Arial,sans-serif",
                                "fontSize": 12,
                                "lineHeight": 6
                            },
                            {
                                "title": "Bromello Script",
                                "fontFamily": "'Bromello Script',cursive",
                                "fontSize": 18,
                                "lineHeight": 6
                            },
                        ],
                    },
                ]
            },
            // this should only be enabled if the customer has purchased
            // a specific upgrade
            // (BE - Subscription Constraint) Show it only if the subscription is active
            "custom": {
                // Base theme of this "custom" theme
                // This custom theme inherits from "contemporary"; missing configs are falled back to
                // the base theme
                // (BE - Feature Constraint) "baseTheme" value must exists in the list above
                "baseTheme": "contemporary",
                // When it is "selected", it is the one used to render guest view
                // (BE - Feature Constraint) There must be one and only one (across all) set to selected=true
                "selected": true,
                // Belong to a package called "creative"
                // When "creative" is subscribed, this becomes usable; otherwise, greyed out
                "subscription": "creavitve",
                "palettes": [
                    {
                        "name": "palette-1",
                        // This "selected" can be "true", only if its parenet.selected is also "true"
                        // (BE - Feature Constraint) There must be one and only one (across all) set to selected=true
                        // (BE - Feature Constraint) This "selected" can be "true", only if its parenet.selected is also "true"
                        "selected": true,
                        "colours": [
                            "#ABA",
                            "#BAB"
                        ]
                    }
                ]
            },
        },
        // These blocks are the ones currently active on the couple view - some of them are also
        // available on the guest view dependant on their parameters
        // (BE - Subscription constraint) The blocks which belong to expired subscription should be moved to inactive
        "activeBlocks": [
            {
                // Each block needs a unique ID to prevent it form being confused
                // with other content
                // The ID is also used as the hyperlink to the content on the page
                // (BE - Subscription constraint) Unquite identifier across blocks
                "id": "hero-banner",
                // This determines if the block is visible on guest view
                "published": true,
                // This determines what type of block we should load
                // (BE - Feature Constraint) Only pre-defined values (probably hard-coded) are allowed
                "type": "hero-banner",
                // Block position
                "order": 1,
                // Name shown on the edit panel
                "name": "Hero banner",
                // Other data for the block
                "title": "We're getting married!",
                "weddingDate": "21st June 2019",
                "showRsvp": true
            },
            {
                "id": "about-us",
                "published": true,
                "type": "custom-text-block",
                "order": 3,
                "name": "About us",
                "title": "About us",
                "content": "Blah blah blah"
            },
            {
                "id": "ceremony",
                "published": false,
                "type": "event",
                "order": 2,
                "name": "Ceremony",
                "title": "Ceremony",
                "addressLine": [
                    "123 Market Street",
                    "Nowhere"
                ],
                "coords": {
                    "lat": 0,
                    "lng": 0
                }
            }
        ],
        // blockPackages are blocks that the user is currently not using at the current time,
        // but may be available to them.
        "blockPackages": {
            // (BE - Subscription Constraint) Populate by each subscribable package
            "free": [
                {
                    "id": "default",
                    "type": "event",
                    "name": "Event",
                    "title": "Event",
                    // On higher tiers, some blocks can be duplicated; as such,
                    // we want to track what is an instance of a block type
                    // and what is the base block type to clone from.
                    // (BE - Feature Constraint) if isInstance=false, completely managed by BE to populate
                    "isInstance": false,
                    "order": 0,
                },
                {
                    "id": "default",
                    "type": "countdown",
                    "name": "Countdown Clock",
                    "title": "Countdown",
                    "isInstance": false,
                    "order": 0,
                },
            ],
            "creative": [
                {
                    "id": "default",
                    "type": "custom-block",
                    "name": "Custom Block",
                    "title": "Custom block",
                    "isInstance": false,
                    "order": 0,
                    "content": null
                },
                {
                    "id": "default",
                    "type": "custom-events",
                    "name": "Custom Event",
                    "title": "Custom event",
                    "isInstance": false,
                    "order": 0,
                    "addressLine": [
                        "123 Market Street",
                        "Nowhere"
                    ],
                    "coords": {
                        "lat": 0,
                        "lng": 0
                    }
                },
                // This is a block as customised by the user; if we keep their data,
                // even if their subscription has expired, then it may encourage them
                // to return in the future.
                {
                    "id": "something",
                    "type": "custom-events",
                    "name": "Custom Event - something something",
                    "title": "something something",
                    "isInstance": true,
                    "order": 0,
                    "addressLine": [
                        "999 Letsby Avenue",
                        "Sheffield"
                    ],
                    "coords": {
                        "lat": 709,
                        "lng": 80
                    }
                }
            ],
        }
    },
    // guest view data
    // Theme data for the actual site view. Includes the theme name
    // to get the correct stylesheet and the colours to generate
    // for the theme proper.
    "view": {
        // (BE - Subscription Constraint) Offer it only if the subscription is active; if the subscription of
        // of this theme is expired, fall back to the FREE subscription's default theme
        "theme": {
            "themeName": "contemporary",
            "colours": [
                "#AAA",
                "#777"
            ]
        },
        // Header is not a custom block - it should always be there.
        // Includes the title and site navigation.
        "header": {
            "title": "Emily & Archie",
            // Site navigation is based on the blocks above; the order they're in
            // depends on where they appear in the navigation as well
            "navigation": [
                // (BE - Subscription Constraint) Offer it only if the subscription is active; Do not render it
                // if the subscription is inactive;
                {
                    "title": "About Us",
                    "path": "about-us"
                },
                {
                    "title": "Ceremony",
                    "path": "ceremony"
                }
            ]
        },
        // This is just the guest version of the blocks list above; this filters out the
        // blocks that are not active (for guest view).
        "blocks": [
            // (BE - Subscription Constraint) Offer it only if the subscription is active; Do not render it
            // if the subscription is inactive;
            {
                "type": "hero-banner",
                "path": null,
                "text": "We're getting married!",
                "weddingDate": "21st June 2019",
                "showRsvp": true,
                "order": 1
            },
            {
                "type": "about-us",
                "path": "about-us",
                "title": "About us",
                "content": "Blah blah blah",
                "order": 3
            }
        ]
    }
}
```