* Our current process (and why we're doing it)
    - Passing `trackId` prop to buttons (or adding `data-tracking-id`)
    - Only buttons currently have this - should apply to anything clickable

* What we can do to improve it
    - Currently, tracking-id seems to be the best thing to do for now

* Our current naming convention
    - `web-editor-theme-theme`
    - `web-editor-${view.id}`
    - `web-editor-block-open-contact-us`

* Making it consistent
    - Not caps, that's just to make it easier lol
    - PAGE-(OPTIONAL-SUBPAGE)-ACTION-SECTION-IDENTIFIER

    e.g. - MKTG-FUNNEL-FOOTER-GETSTARTED
         - SITEBUILDER-ADDBLOCK-EDITCONTENT-PHOTOGALLERY
         - SITEBUILDER-VIEWPORTCHANGE-HEADER-${viewport}
         - SITEBUILDER-EDITBLOCK-EDITCONTENT-PHOTOGALLERY
         - SITEBUILDER-EDITBLOCK-PREVIEW-PHOTOGALLERY
         - GUESTMGMT-INBOX-OPEN-MSGLIST-MESSAGE${msgIndex}

* Pages
    - MKTG - Marketing site
        - FEATURE - Feature page
        - HOME - Homepage
        - ... etc
    - SITEBUILDER - Website editor
    - GUESTMGMT - Guest Management
        - OVERVIEW - Guest Mgmt Overview
        - INBOX - obvs (obviously) - sub-page of GUESTMGMT
        - GUESTLIST - Guest List - sub-page of GUESTMGMT
        - LIFTSHARE - Lift Sharing - sub-page of GUESTMGMT
        - RSVP - RSVP - sub-page of GUESTMGMT
        - TABLEPLAN - Table Plan - sub-page of GUESTMGMT
        - ... etc
    - GIFTLIST - Gift List
    - WEBSETTINGS - Website Settings
    - ACCTSETTINGS - Account Settings
    - DASHBOARD - Couple Dashboard 

* ACTION-SECTION-IDENTIFIER - should use your best judgement

* Action points
 - [ ] @lyndsherb - To write up
 - [ ] @rueGooner - Raise ticket(s) to implement in Marketing site
 - [ ] @sonnybooth-amp - Raise ticket(s) to implement in React app (e.g. website editor, dashboard etc. all separate)