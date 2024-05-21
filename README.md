# Stripe-Documentation
Steps and requirements to integrate Stripe in Flutter app
<details open>
  <summary><i>Click to read more/less...</i></summary>
  
- [ ] Description
- [ ] Stripe APIs (connect-account, payment-intent) https://docs.stripe.com/api
- [ ] Webhook events

## Prerequisites
<details >
  <summary><i>Click to read more/less...</i></summary>
  
> - ***Stripe Account :*** Create an account on [Stripe](https://dashboard.stripe.com/register) if you haven't already.
> - ***Flutter SDK :*** Make sure you have Flutter installed.
> - ***Node.js :*** Make sure you have Node.js installed. You can download it from [here](https://nodejs.org/en).
> - ***Firebase Project :*** Create a project on Firebase.
</details>

## 1. Stripe Dashboard Setting

## 2. Dependencies in pubspec.yaml
<details >
  <summary><i>Click to read more/less...</i></summary>
  
add following packages with the latest compatible versions in your pubspec.yaml file
- flutter_stripe:
- webview_flutter:
- firebase_core:
- cloud_functions:
</details>

## 3. Firebase Integration
<details >
  <summary><i>Click to read more/less...</i></summary>
  
> - ***Firebase CLI :*** Install the Firebase CLI by running below command in your terminal.

    npm install -g firebase-tools
      
> - ***Firebase Authentication:*** Authenticate your Firebase account by running below command in your terminal.

    firebase login


</details>
</details>

## 4. Set up Cloud Functions
<details >
  <summary><i>Click to read more/less...</i></summary>
  
- [Read this to get started with cloud functions](https://firebase.google.com/docs/functions/get-started?gen=2nd) follow to step 5

- Create a new folder `cloud_functions` in your project and run the below commands in your terminal.
> - Navigate to `cloud_functions` directory

    cd cloud_functions
> - Initialize Firebase Cloud Functions in your project

    firebase init functions
> - Navigate to the functions directory 

    cd functions
> - Install the Stripe Node.js package

    npm install stripe --save
</details>
  
### Service Account 
<details >
  <summary><i>Click to read more/less...</i></summary>
  
> service_key.json

Required to operate Cloud Functions for Firebase
</details>

### Cloud Function Code
<details open>
  <summary><i>Click to read more/less...</i></summary>
-
  
> In `index.ts` file add below code:

    const serviceAccount = require('../service_key.json');
    import * as admin from 'firebase-admin';
    import * as functions from 'firebase-functions';
    import { setGlobalOptions } from "firebase-functions/v2";
    import * as express from 'express';
    import { Request, Response } from 'express';

    admin.initializeApp({
        credential: admin.credential.cert(serviceAccount as admin.ServiceAccount),
        databaseURL: 'https://swfty-app.firebaseio.com'
    });
    setGlobalOptions({ maxInstances: 10 });
    admin.firestore().settings({ ignoreUndefinedProperties: true });
    
    const app = express();
    app.use(express.json());

    export const stripeApi = functions.https.onRequest(app);
    
    /* const Stripe = require('stripe');
    const stripe = Stripe('sk_test_51OhxzvKwFratyVywo9ZPCc5YqdHKYcINNdxj5ZBmlHQs3zG3Dy9hL9cctqOmBO4dobfgpUf7ZtLkSS7XJs5YSBRn00ZgCgs71C'); */
    
</details>

## 5. Connect Account

> - createAccount Stripe Api in index.ts

    import { stripe, userCollection } from '../utils/constants'
      
    app.get('/createAccount', async (req: Request, res: Response) => {
        if (req.query.userId === undefined || req.query.userName === undefined) {
            res.send('Missing parameters');
            return;
        }

    const userId: string = req.query.userId as string,
    const userName: string = req.query.userName as string,
    const stripeAccountId = req.query.stripeAccountId,
        let result;

    try {
        let account
        if (!stripeAccountId) {
            account = await stripe.accounts.create({
                country: 'US',
                type: 'custom',
                business_type: 'individual',
                individual: {
                    first_name: userName,
                    last_name: userName
                },
                business_profile: {
                    mcc: '8999',
                    url: 'https://techanion.com'
                },
                metadata: {
                    // store any custom data associated with the account! as:
                    // you can later use the Stripe API to retrieve the account and access this custom data
                    // user_id: userId,
                },
                tos_acceptance: {
                    date: Math.floor(Date.now() / 1000),
                    ip: '192.168.20.20'
                },
                settings: {
                    payouts: {
                        schedule: {
                            delay_days: 3,
                            interval: 'daily',
                        }
                    }
                },
                capabilities: {
                    card_payments: {
                        requested: true
                    },
                    transfers: {
                        requested: true
                    }
                }
            })
            userCollection.doc(userId).set({ stripeAccountId: account.id, verified: false }, { merge: true })
            console.log(account)
        }
        const accountLinks = await stripe.accountLinks.create({
            account: stripeAccountId ?? account?.id ?? '',
            refresh_url: 'https://www.techanion.com/refresh',
            return_url: 'https://www.techanion.com/return',
            type: stripeAccountId ? 'account_update' : 'account_onboarding'
        })
        console.log(accountLinks)
        result = accountLinks;
    } catch (e) {
        console.log(e)
        result = e;
    }
    if (result) {
        console.log("check url", result);
        res.send(result).status(200);
    } else {
        res.send('Error').status(400);
    }
    }); 

    
## 6. Payment Intent 



## 7. Webhooks

### Deploy Cloud Functions
> [!NOTE]
> you must navigate to the `functions` directory in terminal, before deploying the cloudFunctions

<details >
  <summary><i>Click to read more/less...</i></summary>


- Run one of the below commands in terminal to deploy:
> To deploy all cloud functions

    firebase deploy --only functions

OR
    
> To deploy single cloud function

    firebase deploy --only functions:<function_name_here>
  
</details>
