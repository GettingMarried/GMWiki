```jsonc

/**
 * Assumptions
 *
 * (1) When a theme's subscription gets expiried, the theme (and its palette and font) remain selected but not configurable
 *
 * General idea
 *
 * (1) FE manage content data
 * (2) BE manage subscription status and check / remove expired features "view"
 * (3) For visual features (e.g., theme / font), when they expire, they become readonly (we don't actually disable them)
 *     this is to avoid breaking the site too much
 * (4) For functional features (e.g., RSVP), when they expire, BE remove them from "view".
 *     this is to encourage the couple to subscribe the package again
 */
{
  // (Note) Couple view data
  // (BE Constraint) only show up on couple view
  "editPanel": {
    // (Note) Identify what packages are subscribed / purchased (i.e., can be used by the couple)
    //        If a package is subscrited, it shows up in the list; otherwise not.
    // (Note) Manage by BE
    // (BE Constraint) Populate this data base on subscription status so that FE can disable features which are not subscribed
    // (FE Constraint) FE should only enable features subscribed in EditPanel
    "subscribedPackages": [
      "f7d16f36-0eb0-11e9-808d-f0189893d2b2",
      // UUID for "Free" package
      "5bd4f732-0eb1-11e9-a0ed-f0189893d2b2",
      // UUID for "Creative" package
    ],
    // (Note) Manage by BE
    // (BE Constraint) Populate all "public" (i.e., ever-subscribable) packages so that we can render disabled features to encourage subscription
    "packages": [
      {
        "id": "f7d16f36-0eb0-11e9-808d-f0189893d2b2",
        "title": "Free",
        "features": [
          // (BE Constraint) Populate features assigned to the package
          // (Note) These are feature codes and they are uniquely identifier representing the features
          "basic_themes",
          "free_font_family",
          "theme_palettes",
          "event",
          "countdown",
        ],
      },
      {
        "id": "5bd4f732-0eb1-11e9-a0ed-f0189893d2b2",
        "title": "Creative Suite",
        "features": [
          "premium_themes",
          "custom_font_family",
          "custom_palettes",
          "rsvp",
          "custom_text_block",
          "custom_event",
        ],
      },
    ],
    // (Note) Manage by FE
    // (Note) Contains grouped information of [Theme, Colour Palette, Typography]
    //        and linked to features
    "themes": [
      {
        // (Note) code of the palette should be unique; this ensures we get the correct stylesheet for the structure
        "code": "rustic",
        "type": "theme",
        "feature": "basic_themes",
        "title": "Rustic",
        // (BE - Constraint) Selected on theme.palettes level
        "selected": true,
        // (Note) each theme has multiple pre-determined palettes
        "palettes": [
          {
            // (Note) Each palette has the colours in a set order;
            //        these will be applied with styled-components on the frontend
            //        so we don't need to fret about stylesheets
            "title": "Gold & Green",
            "type": "static-palette",
            // (BE - Constraint) Populate by feature so FE can group them for rendering and enabling
            "feature": "theme_palettes",
            "selected": false,
            "colours": [
              "#00F",
              "#FF0"
            ]
          },
          {
            "title": "Floral",
            "type": "static-palette",
            "feature": "theme_palettes",
            "selected": false,
            "colours": [
              "#BBB",
              "#CCC"
            ]
          },
          {
            "title": "Masculine",
            "type": "static-palette",
            "feature": "theme_palettes",
            "selected": false,
            "colours": [
              "#ABA",
              "#BAB"
            ]
          },
          {
            "title": "Custom Palette",
            "type": "custom-palette",
            "feature": "custom_palettes",
            // (BE - Constraint) Selected on theme.palettes level
            "selected": true,
            // (BE - Constraint) Read only if the feature is NOT subscribed
            // (FE - Constraint) Read only if the feature is NOT subscribed
            "colours": [
              "#ABA",
              "#BAB"
            ]
          },
        ],
        "typographies": [
          {
            "type": "font-family",
            "feature": "free_font_family",
            "title": "Arial",
            "fontFamily": "Arial,sans-serif",
            "fontSize": 12,
            "lineHeight": 6,
            // (BE - Constraint) Selected on theme.typographies level
            "selected": true,
          },
          {
            "type": "font-family",
            "feature": "free_font_family",
            "title": "Bromello Script",
            "fontFamily": "'Bromello Script',cursive",
            "fontSize": 18,
            "lineHeight": 6,
            "selected": false,
          },
        ],
      },
      {
        "code": "contemporary",
        "type": "theme",
        "feature": "basic_themes",
        "title": "Contemporary",
        "selected": false,
        "palettes": [
          {
            "title": "Gold & Green",
            "type": "static-palette",
            "feature": "theme_palettes",
            "selected": true,
            "colours": [
              "#00F",
              "#FF0"
            ]
          },
          {
            "title": "Floral",
            "type": "static-palette",
            "feature": "theme_palettes",
            "selected": false,
            "colours": [
              "#BBB",
              "#CCC"
            ]
          },
          {
            "title": "Masculine",
            "type": "static-palette",
            "feature": "theme_palettes",
            "selected": false,
            "colours": [
              "#ABA",
              "#BAB"
            ]
          },
          {
            "title": "Custom Palette",
            "type": "custom-palette",
            "feature": "custom_palettes",
            "selected": false,
            "readonly": false,
            "colours": [
              "#ABA",
              "#BAB"
            ]
          },
        ],
        "typographies": [
          {
            "type": "font-family",
            "feature": "free_font_family",
            "title": "Arial",
            "fontFamily": "Arial,sans-serif",
            "fontSize": 12,
            "lineHeight": 6,
            "selected": true,
          },
          {
            "type": "font-family",
            "feature": "free_font_family",
            "title": "Bromello Script",
            "fontFamily": "'Bromello Script',cursive",
            "fontSize": 18,
            "lineHeight": 6,
            "selected": false,
          },
        ],
      },
      {
        "code": "minimal",
        "type": "theme",
        // (BE Constraint) As this belong to the "premium_themes" feature, this theme should be readonly if creative suite is not subscribed
        // (FE Constraint) As this belong to the "premium_themes" feature, this theme should be readonly if creative suite is not subscribed
        "feature": "premium_themes",
        "title": "Minimal",
        "selected": false,
        "palettes": [
          {
            "title": "Gold & Green",
            "type": "static-palette",
            "feature": "theme_palettes",
            "selected": true,
            "colours": [
              "#00F",
              "#FF0"
            ]
          },
          {
            "title": "Custom Palette",
            "type": "custom-palette",
            "feature": "custom_palettes",
            "selected": false,
            "readonly": false,
            "colours": [
              "#ABA",
              "#BAB"
            ]
          },
        ],
        "typographies": [
          {
            "type": "font-family",
            "feature": "custom_font_family",
            "title": "Arial",
            "fontFamily": "Arial,sans-serif",
            "fontSize": 12,
            "lineHeight": 6
          },
          {
            "type": "font-family",
            "feature": "custom_font_family",
            "title": "Bromello Script",
            "fontFamily": "'Bromello Script',cursive",
            "fontSize": 18,
            "lineHeight": 6
          },
        ],
      },
    ],
    // (Note) These blocks are the prototype which is just a boilerplate with default config
    //        Couple will create block-instances from these blocks and once created, put in active blocks list
    // (Note) Manage by BE
    "blocks": [
      {
        "code": "hero-banner",
        "name": "Hero Banner",
        "path": "we-re-getting-married",
        "feature": "hero_banner",
        "type": "hero-banner",
        "published": false,
        "subscribed": false,
        "order": 0,
        "title": "We're getting married!",
        "weddingDate": "21st June 2019",
      },
      {
        "code": "rsvp",
        "name": "RSVP",
        "path": "rsvp",
        "feature": "rsvp",
        "type": "rsvp",
        "published": false,
        "subscribed": false,
        "order": 0,
      },
      {
        "code": "about-us",
        "name": "About us",
        "path": "about-us",
        "feature": "custom_text_block",
        "type": "custom-text-block",
        "published": false,
        "subscribed": false,
        "order": 3,
        "title": "Our Story",
        "content": "We met back in the summer of ..."
      },
      {
        "code": "ceremony",
        "name": "Ceremony",
        "path": "ceremony",
        "type": "event",
        "published": false,
        "subscribed": false,
        "order": 2,
        "title": "Ceremony",
        "addressLines": [
          "123 Market Street",
          "Nowhere"
        ],
        "coords": {
          "lat": 0,
          "lng": 0
        }
      },
      {
        "code": "event",
        "name": "Event",
        "path": "event",
        "feature": "event",
        "type": "event",
        "published": false,
        "subscribed": false,
        "title": "Event",
        "order": 0,
      },
      {
        "code": "countdown_clock",
        "name": "Countdown Clock",
        "path": "countdown-clock",
        "feature": "countdown",
        "type": "countdown",
        "published": false,
        "subscribed": false,
        "title": "Countdown",
        "order": 0,
      },
      // (FE Constraint) As this block is offered by "custom_text_block" feature, should be disabled if the feature is not subscribed
      {
        "code": "custom_block",
        "name": "Custom Block",
        "path": "custom-block",
        "feature": "custom_block",
        "type": "custom-block",
        "published": false,
        "subscribed": false,
        "title": "Custom block",
        "order": 0,
        "content": "",
      },
      {
        "code": "custom_event",
        "name": "Custom Event",
        "path": "custom-event",
        "feature": "custom_event",
        "type": "custom-event",
        "published": false,
        "subscribed": false,
        "title": "Custom event",
        "order": 0,
        "addressLines": [
          "123 Market Street",
          "Nowhere"
        ],
        "coords": {
          "lat": 0,
          "lng": 0
        }
      },
    ],
    // (Note) These blocks are the ones currently active on the couple view
    //        some of them are also available on the guest view dependant on their parameters
    // (Note) Manage by FE
    // (BE - Constraint) If the block's feature expires force to "public=false"
    // (FE - Constraint) If the block's feature expires force to "public=false"
    "activeBlocks": [
      {
        // (Note) Each block needs a unique ID to prevent it form being confused
        //        with other content
        // (BE - Constraint) Unquite identifier across blocks
        // (FE - Constraint) Unquite identifier across blocks
        //                   It is generated from name
        "code": "hero-banner",
        // (Note) Name shown on the edit panel
        "name": "Hero Banner",
        // (Note) The hyperlink to the content on the page
        //        It is generated from code
        "path": "we-re-getting-married",
        // (BE Constraint) the block become readonly if the feature is not subscribed
        // (FE Constraint) the block become readonly if the feature is not subscribed
        "feature": "hero_banner",
        // (Note) This determines what type of block we should load
        "type": "hero-banner",
        // (Note) This determines if the block is visible on guest view
        // (BE Constraint) force to always "false" if the feature is not subscribed
        // (FE Constraint) force to always "false" if the feature is not subscribed
        "published": true,
        // (Note) This is a flag to help FE minimise computing on the subscription status while allow it to
        //        decide if the block is subscribed - i.e., should be editable or not
        // (BE Constraint) On retrieval, compute this value based on the subscription status
        "subscribed": true,
        // (Note) Block position
        "order": 0,
        // (Note) Other data for the block
        "title": "We're getting married!",
        "weddingDate": "21st June 2019",
      },
      {
        "code": "rsvp",
        "name": "RSVP",
        "path": "rsvp",
        "feature": "rsvp",
        "type": "rsvp",
        "published": true,
        "subscribed": true,
        "order": 1,
      },
      {
        "code": "about-us",
        "name": "About us",
        "path": "about-us",
        "feature": "custom_text_block",
        "type": "custom-text-block",
        "published": true,
        "subscribed": true,
        "order": 3,
        // (Note) Other data for the block
        "title": "About us",
        "content": "Blah blah blah"
      },
      {
        "code": "ceremony",
        "name": "Ceremony",
        "path": "ceremony",
        "type": "event",
        "published": false,
        "subscribed": true,
        "order": 2,
        "title": "Ceremony",
        "addressLines": [
          "123 Market Street",
          "Nowhere"
        ],
        "coords": {
          "lat": 0,
          "lng": 0
        }
      }
    ],
  },
  // (Note) Guest view data
  "view": {
    // (Note) Only "selected" is populated in this array
    //        The only reason to implement this plural form is to simplify the data structure to maintain
    // (BE Constraint) Validate and make sure the theme code exists
    // (BE Constraint) On persistence, throw an error if more than one element is offered
    // (BE Constraint) On persistence, throw an error if the element does not match those defined in editPanel
    // (FE Constraint) Validate and offer only selected elements
    "themes": [
      {
        "code": "rustic",
        "type": "theme",
        "feature": "basic_themes",
        "title": "Rustic",
        "selected": true,
        // (BE Constraint) On persistence, throw an error if more than one element is offered
        "palettes": [
          {
            "title": "Custom Palette",
            "type": "custom-palette",
            "feature": "custom_palettes",
            "selected": true,
            "colours": [
              "#ABA",
              "#BAB"
            ]
          },
        ],
        // (BE Constraint) On persistence, throw an error if more than one element is offered
        "typographies": [
          {
            "type": "font-family",
            "feature": "free_font_family",
            "title": "Arial",
            "fontFamily": "Arial,sans-serif",
            "fontSize": 12,
            "lineHeight": 6,
            "selected": true,
          },
        ],
      },
    ],
    "header": {
      "title": "Emily & Archie",
      "navigation": [
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
    "activeBlocks": [
      {
        "code": "rsvp",
        "name": "RSVP",
        "path": "rsvp",
        "feature": "rsvp",
        "type": "rsvp",
        "published": true,
        "order": 1,
        "title": "We're getting married!",
        "weddingDate": "21st June 2019",
        "showRsvp": true,
      },
      {
        "code": "about-us",
        "name": "About us",
        "path": "about-us",
        "feature": "custom_text_block",
        "type": "custom-text-block",
        "published": true,
        "order": 3,
        "title": "About us",
        "content": "Blah blah blah"
      },
    ]
  }
}
```