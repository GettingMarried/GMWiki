This wiki documents the necessary credentials details for development.

## GM default admin

Local / development
- https://gettingmarried.ampdev.co/admin
- Username: `tt+gm+dev+admin@amp.co`
- Password: `gettingmarried123!`

Authentication uses Auth0 service for both Admin view and couple view.
 
You must have a valid user setup and active into their backend. To create an admin account, log in to Auth0 portal  with corresponding Auth0 credentials and create a new user at [Users](https://manage.auth0.com/#/users). 

## GM data fixture domains

Local
- https://emilyandarchie.gettingmarried-local.ampdev.co
- https://aliceandbob.gettingmarried-local.ampdev.co
- https://invalid.gettingmarried-local.ampdev.co (any domain that contains the keyword `invalid` will fail)

Dev
- https://emilyandarchie.gettingmarried.ampdev.co
- https://aliceandbob.gettingmarried.ampdev.co

QA
- https://emilyandarchie.gettingmarried-qa.ampdev.co
- https://aliceandbob.gettingmarried-qa.ampdev.co

For Dev and QA, two DNS records (`emilyandarchie` and `aiceandbob`)
are created.

For local, use `invalid` keyword for testing, as we don't have DNS
server setup locally.

## GM data fixture user

Local / development
- https://gettingmarried.ampdev.co/login
- Username: `tt+gm+dev+user@amp.co`
- Password: `gettingmarried123!`
- Guest view: https://gettingmarried.ampdev.co/wedding/guest/000000ff-0000-1000-8000-000000000000
- Subscribed Packages: `Free`
- Auth0 ID: `auth0|5c7d3fd90c26462c04c496ce`

There are also 3 spare accounts to facilitate development and QA. (Password is the same)

- `tt+gm+dev+user+2@amp.co`

    https://gettingmarried.ampdev.co/wedding/guest/00000100-0000-1000-8000-000000000000

    - Subscribed Packages: `Free` and `Creative Suite`
    - Auth0 ID: `auth0|5c9b4ae1f2c8a911a283f4f9`

- `tt+gm+dev+user+3@amp.co`

    https://gettingmarried.ampdev.co/wedding/guest/00000101-0000-1000-8000-000000000000

    - Subscribed Packages: `Free`
    - Auth0 ID: `auth0|5c9b4b183e678c11ada56e52`

- `tt+gm+dev+user+4@amp.co`

    https://gettingmarried.ampdev.co/wedding/guest/00000102-0000-1000-8000-000000000000

    - Subscribed Packages: `Free`
    - Auth0 ID: `auth0|5c9b4b63c0df337b458620a9`

- `tt+gm+dev+user+suspended@amp.co`

    https://gettingmarried.ampdev.co/wedding/guest/00000103-0000-1000-8000-000000000000

    - Subscribed Packages: `Free`, `Creative Suite`
    - Auth0 ID: `auth0|5d24a9c749d3b20ed08bb34a`
    - Note: User with a billiable subscription which is **suspended**

- `tt+gm+dev+user+cancelled@amp.co`

    https://gettingmarried.ampdev.co/wedding/guest/00000104-0000-1000-8000-000000000000

    - Subscribed Packages: `Free`, `Creative Suite`
    - Auth0 ID: `auth0|5d24a9dfd5a5980de9f7a6d5`
    - Note: User with a billiable subscription which is **cancelled**

This user is pre-populated with data fixture to enable QA

### Force a subscription into suspended or cancelled state

To facilitate QA and also cover complicated scenario, e.g., verifying that the website editor's blocks and data stay still after resuming payment with a suspended account, scripts are created to force specific account in QA / Development environment into suspended or cancelled state.

#### Example scenario

1. Log in to any user account (new or data fixture one, e.g., `tt+gm+dev+user+3@amp.co`)
1. Subscribe to billable package (e.g., `Creative Suite`)
1. Configure website editor to use blocks and themes from the billable package
1. **Force the user account into suspended state (with developer help)**
1. Update credit card and retry payment (the account reactivated automatically)
1. Verify the blocks and theme data remain the same

#### To enforce suspended or cancelled state, please ask any developer to run below script

Prerequisite:

- `cx` is installed locally (https://app.cloud66.com/toolbelt).
- The account (e.g., `tt+gm+dev+user+3@amp.co`) has subscribed billable package

```bash
# To suspend an account
COUPLE_EMAIL="tt+gm+dev+user+3@amp.co" CLOUD66_ENV="gettingmarried" ./tests/scripts/suspend_user.sh

# To cancel an account
COUPLE_EMAIL="tt+gm+dev+user+3@amp.co" CLOUD66_ENV="gettingmarried" ./tests/scripts/cancel_user.sh
```

Note: `COUPLE_EMAIL` is the email of the account against

Note 2: `CLOUD66_ENV` is either `gettingmarried` or `gettingmarried-qa`

Reference:

- https://github.com/AmpersandHQ/gettingmarried/blob/development/tests/scripts/suspend_user.sh
- https://github.com/AmpersandHQ/gettingmarried/blob/development/tests/scripts/cancel_user.sh

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

## MailChimp

Local / development / qa
- https://login.mailchimp.com/
- Username: `ampdeveloper`
- Password: `#7wFxTpEdRFULDDYmdYq`
- API Key: `c5d895c33efba6e9ccbe6e56c75592ed-us3`
- List ID (aka: Audience ID): `da51dd4a04`

Production
- Please check with Torrey, Martha, or Andrew

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