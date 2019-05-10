In this project we have been asked to implement new tracking codes to ensure that anything clickable or trackable is easy to pick up and identify in tracking software, such as Google Tag Manager. 

It has been agreed by the team that all links and buttons should include a data-attribute to ensure that we can correctly log everything, for the following reasons: 

* We might need element `id`s for different reasons, e.g. targeting elements with JavaScript
* If we target element classes, they may be used frequently throughout the site, therefore making the click event non-uniquely identifiable 

Our solution to this was to add the `data-tracking-id` attribute to our interactive elements, without making the identifiers too personal. Following that, we needed to come up with a suitable naming convention to ensure that we knew: 

* What **page** of the site the user was on (e.g. Website Editor, Guest Management)
	* Where applicable, what **sub-page** a user was on (e.g. Inbox would be considered a sub-page of Guest Management)
* What **action** the user was trying to do
* What **section** the user was on (e.g. Website Editor 'Edit Content', Inbox 'Open Message')
* What **identifies** the particular element (e.g. Contact Us, Photo Gallery, a message index number)

Following this, we settled on the following the format, using `camelCase` where necessary:

```
page-(optionalSubpage)-action-section-identifier
```

With this in mind, the following is a non-exhaustive list of `page`s throughout the project, with their sub-pages where applicable. 

* `mktg` - Marketing site
  * `feature` - Feature page
  * `home` - Homepage
  * `funnel` - Marketing funnel
  * Other pages TBC
* `siteBuilder` - Website editor
* `guestManagement` - Guest Management
  * `overview` - Guest Management Overview
  * `inbox`
  * `guestList`
  * `rsvp` * RSVP * sub-page of GUESTMGMT
  * Other pages TBC
* `giftList` - Gift List
  * `basket`
* `webSettings` - Website Settings
* `acctSettings` - Account Settings
* `dashboard` - Couple Dashboard 

If you can't see your specific page listed, **use your best judgement** and update this document with your choice - this will ensure that we keep everything consistent. 

When it comes to `action`s, `section`s and `identifier`s, again, **use your best judgement**. They don't necessarily need to be documented in this instance; if it makes the points listed above clear enough to understand, it should be fine. 

Below are some usable examples of the format to follow. Some instances utilise `${variable}`s as these are likely to be unique and somewhat dynamic, in case there may be multiple instances thereof. 

* `mktg-funnel-footer-getStarted`
* `siteBuilder-addBlock-editContent-${block.path}`
* `siteBuilder-viewportChange-header-${viewport}`
* `siteBuilder-editBlock-editContent-${block.path}`
* `siteBuilder-open-header-livePreview`
* `guestManagement-inbox-openMessageList-message`

* Action points
 - [x] @lyndsherb - To write up
 - ~~rueGooner - Raise ticket(s) to implement in Marketing site~~ - No longer applicable, we'll just keep things up to date going forward.
 - ~~sonnybooth-amp - Raise ticket(s) to implement in React app (e.g. website editor, dashboard etc. all separate)~~  - No longer applicable, we'll just keep things up to date going forward.