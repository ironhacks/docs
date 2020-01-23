
__Dependencies__ 

The Ironhacks Platform (the platform) use the following firebase services:

+ [Authentication](https://firebase.google.com/docs/auth)
+ [Cloud Firestore](https://firebase.google.com/docs/firestore)
+ [Storage](https://firebase.google.com/docs/storage)
+ [Hosting](https://firebase.google.com/docs/hosting)
+ [Cloud Functions](https://firebase.google.com/docs/functions)
+ [Firebase Auth UI](https://firebase.google.com/docs/auth/web/firebaseui)

We assume you are familiarized with all these services, how they work, and how to code using them. If you are not familiarized with them please check the Firebase documentation.

In addition, we use the following libraries/third party utilities:

+ [Octonode (A nodeJS library to access Github V3 API)](https://github.com/pksunkara/octonode)
+ [AWS-SKD](https://aws.amazon.com/developers/getting-started/nodejs/)
+ [Amazon SES](https://aws.amazon.com/ses/getting-started/)

We assume you are familiarized with all these librarires, how they work, and how to code using them. If you are not familiarized with them please check the documentation of each one.

This Firebase project performs third party calls, therefore it must be enrolled in a paid plan (we suggest the Blaze plan), however, this is not completely necessary, since you can opt to not have neither email notifications (via Amazon SES) nor GitHub support.

If you choose to use them, you will have to setup the amazon SES service, and since the platform creates private repositories into GitHub, you will also have to have a PRO account.
