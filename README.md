# Stripe-Documentation
Steps and requirements to integrate Stripe in Flutter
- [ ] Description
- [ ] Stripe APIs (connect-account, payment-intent) https://docs.stripe.com/api
- [ ] Webhook events

### 1. Stripe Dashboar Setting

## 2. Dependencies in pubYaml 
- flutter_stripe
- webview_flutter

## 3. Cloud Functions
- create a cloud_functions folder in your project
- [Read this to get started with cloud functions](https://firebase.google.com/docs/functions/get-started?gen=2nd) follow to step 5
##### Terminal commands:
- Navigate to functions directory as `cd cloud_functions/functions`
- Initialize Node `npm init`
- Install stripe library `npm install stripe --save`
##### Stripe Authentication
[Read this Document for Reference](https://docs.stripe.com/api/authentication)

In `index.ts` file add below code:

    const Stripe = require('stripe');
    const stripe = Stripe('sk_test_51OhxzvKwFratyVywo9ZPCc5YqdHKYcINNdxj5ZBmlHQs3zG3Dy9hL9cctqOmBO4dobfgpUf7ZtLkSS7XJs5YSBRn00ZgCgs71C');



## 4. Connect Account

## 5. Payment Intent 

## 6. Webhooks
