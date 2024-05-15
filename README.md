# Stripe-Documentation
Steps and requirements to integrate Stripe in Flutter app
      
- [ ] Description
- [ ] Stripe APIs (connect-account, payment-intent) https://docs.stripe.com/api
- [ ] Webhook events

## Prerequisites
> - ***Stripe Account :*** Create an account on [Stripe](https://dashboard.stripe.com/register) if you haven't already.
> - ***Flutter SDK :*** Make sure you have Flutter installed.
> - ***Node.js :*** Make sure you have Node.js installed. You can download it from [here](https://nodejs.org/en).
> - ***Firebase Project :*** Create a project on Firebase.

## 1. Stripe Dashboard Setting

## 2. Dependencies in pubspec.yaml
add following packages with the latest compatible versions in your pubspec.yaml file
- flutter_stripe:
- webview_flutter:
- firebase_core:
- cloud_functions:

## 3. Firebase Integration
> - ***Firebase CLI :*** Install the Firebase CLI by running below command in your terminal.

    npm install -g firebase-tools
      
> - ***Firebase Authentication:*** Authenticate your Firebase account by running below command in your terminal.

    firebase login

## 4. Set up Cloud Functions
- [Read this to get started with cloud functions](https://firebase.google.com/docs/functions/get-started?gen=2nd) follow to step 5

- Create a new folder `cloud_functions` in your project and run the below commands in your terminal.
> - Navigate to `cloud_functions` directory
> 

    cd cloud_functions
> - Initialize Firebase Cloud Functions in your project
> 

    firebase init functions
> - Navigate to the functions directory
> 

    cd functions
> - Install the Stripe Node.js package
> 

    npm install stripe --save
  
### Stripe Authentication
You can use the Stripe API in test mode, which doesn’t affect your live data or interact with the banking networks. The API key you use to authenticate the request determines whether the request is live mode or test mode. 
[Read this Document for Reference](https://docs.stripe.com/api/authentication)

> In `index.ts` file add below code:

    const Stripe = require('stripe');
    const stripe = Stripe('sk_test_51OhxzvKwFratyVywo9ZPCc5YqdHKYcINNdxj5ZBmlHQs3zG3Dy9hL9cctqOmBO4dobfgpUf7ZtLkSS7XJs5YSBRn00ZgCgs71C');

### Deploy Cloud Functions
> [!NOTE]
> you must navigate to the `functions` directory in terminal, before deploying the cloudFunctions

- Run one of the below commands in terminal to deploy:
> To deploy all cloud functions

    firebase deploy --only functions

OR
    
> To deploy single cloud function

    firebase deploy --only functions:<function_name_here>
  

## 5. Connect Account

## 6. Payment Intent 

## 7. Webhooks
