In this project we have been asked to implement new tracking codes to ensure that anything clickable or trackable is easy to pick up and identify in tracking software, such as Google Tag Manager. 

It has been agreed by the team that all links and buttons should include a data-attribute to ensure that we can correctly log everything, for the following reasons: 
* We might need element `id`s for different reasons, e.g. targeting elements with JavaScript
* If we target element classes, they may be used frequently throughout the site, therefore making the click event non-uniquely identifiable 

Our solutionto this was to add the `data-tracking-id` attribute to our interactive elements, without making the identifiers too personal. Following that, we needed to come up with a suitable naming convention to ensure that we knew: 
* What **page** of the site the user was on
* What **action** the user was trying to do
* What **section** the user was on (e.g. Website Editor 'Edit Content', Inbox 'Open Message')
* What **identifies** the particular element (e.g. Contact Us, Photo Gallery, a message index number)

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