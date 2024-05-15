# Stripe-Documentation

 Steps and requirements to integrate Stripe in Flutter
      
- [ ] Description
- [ ] Stripe APIs (connect-account, payment-intent) https://docs.stripe.com/api
- [ ] Webhook events

## Prerequisites
> - ***Flutter SDK :*** Make sure you have Flutter installed.
> - ***Stripe Account :*** Create an account on [Stripe](https://dashboard.stripe.com/register) if you haven't already.
> - ***Firebase Account :*** Create a project on Firebase.
> - ***Node.js :*** Make sure you have Node.js installed. You can download it from [here](https://nodejs.org/en).
> - ***Firebase CLI :*** Install the Firebase CLI by running below command in your terminal.

    npm install -g firebase-tools
      
> - ***Firebase Authentication:*** Authenticate your Firebase account by running below command in your terminal.

    firebase login

## 1. Stripe Dashboar Setting

## 2. Dependencies in pubYaml 
- flutter_stripe
- webview_flutter

## 3. Set up Cloud Functions
- [Read this to get started with cloud functions](https://firebase.google.com/docs/functions/get-started?gen=2nd) follow to step 5

1. Create a cloud_functions folder in your project
2. Navigate to `cloud_functions` directory
> 

    cd cloud_functions
3. Initialize Firebase Cloud Functions in your project
> 

    firebase init functions
4. Navigate to the functions directory
> 

    cd functions
4. Install the Stripe Node.js package
> 

    npm install stripe --save
  
5. Stripe Authentication
> [Read this Document for Reference](https://docs.stripe.com/api/authentication)

> In `index.ts` file add below code:

    const Stripe = require('stripe');
    const stripe = Stripe('sk_test_51OhxzvKwFratyVywo9ZPCc5YqdHKYcINNdxj5ZBmlHQs3zG3Dy9hL9cctqOmBO4dobfgpUf7ZtLkSS7XJs5YSBRn00ZgCgs71C');



## 4. Connect Account

## 5. Payment Intent 

## 6. Webhooks
