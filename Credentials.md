This wiki documents the necessary credentials details for development.

## GM default admin

Local / development
- https://gettingmarried.ampdev.co/admin
- Username: `tt+gm+dev+admin@amp.co`
- Password: `gettingmarried123!`

Authentication uses Auth0 service for both Admin view and couple view.
 
You must have a valid user setup and active into their backend. To create an admin account, log in to Auth0 portal  with corresponding Auth0 credentials and create a new user at [Users](https://manage.auth0.com/#/users). 

## GM data fixture user

Local / development
- https://gettingmarried.ampdev.co/login
- Username: `tt+gm+dev+user@amp.co`
- Password: `gettingmarried123!`
- Guest view: https://gettingmarried.ampdev.co/wedding/guest/000000ff-0000-1000-8000-000000000000
- Subscribed Packages: `Free`

There are also 3 spare accounts to facilitate development and QA. (Password is the same)

- `tt+gm+dev+user+2@amp.co`

    https://gettingmarried.ampdev.co/wedding/guest/00000100-0000-1000-8000-000000000000

    - Subscribed Packages: `Free` and `Creative Suite`

- `tt+gm+dev+user+3@amp.co`

    https://gettingmarried.ampdev.co/wedding/guest/00000101-0000-1000-8000-000000000000

    - Subscribed Packages: `Free`

- `tt+gm+dev+user+4@amp.co`

    https://gettingmarried.ampdev.co/wedding/guest/00000102-0000-1000-8000-000000000000

    - Subscribed Packages: `Free`

This user is pre-populated with data fixture to enable QA

## Auth0

Local / development / qa
- https://manage.auth0.com
- Username: `development@ampersandit.co.uk`
- Password: `B&IRFno*^gB*)N7v*Pyv`

## Stripe

Local / development / qa
- https://dashboard.stripe.com/login
- Username: `tt@amp.co`
- Password: `*zT9$Hl^5VC^2C6c`

## Booking.com API and Documentation

Development
- HTTP Basic Auth
- Username: `accounts@gettingmarried.co.uk`
- Password: `Tonypandy2015`

Endpoint: `https://distribution-xml.booking.com/2.3/json/{resource}`

## Google Tag Manager

Environment: Local / Dev / QA

- Container ID: `GTM-KPXQ77D`

Login: https://www.google.com/analytics/tag-manager/

Admin: Andrew Hill

*Important:* GTM account is accessed through google account. Ask the admins to grant access.