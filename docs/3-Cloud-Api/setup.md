
## Setting up the dev environment

This is a clasic Firebase Cloud Functions project, so the "installation process" is just deploy the functions (AKA this project) into your firebase project.

In that matter, we recommend you to use this project as template for your implementation of the platform. In order to set it up, do the following:

### Setting up the Firebase Cloud Functions project

+ Create a Firebase Project from [The Firebase Console](https://console.firebase.google.com) (If you start by the [Platform Repository](https://github.com/RCODI/the-ironhacks-platform) you propably arlready did this)
+ Initialize the Cloud Functions in your project ([Getting Started Cloud Funtions](https://firebase.google.com/docs/functions))
+ Clone this repo into a diferent folder in your local machine:

  ```bash
  git clone https://github.com/RCODI/the-ironhacks-platform-backend.git
  ```

Now, go to your project folder and copy the `service-account.json` file located in the `functions` folder.

Paste into the `the-ironhacks-platform-backend` repo you just clone, in the same `functions` folder.

This will link the functions on this project with your own Firebase project.

Now we need to add the Amazon SES and the Github V3 API keys in order to enable the notifications (via email) for the forum and the automatic repository creation on github.

### Setting the enviroment variables

If you are not familiar with the base Environment configuration, check [the docs](https://firebase.google.com/docs/functions/config-env).
In order to make it work, you must set the following env variables:

+ From your firebase project:
  + database.url = "Realtime database URL" (Keep in mind we don't use it, this is just to create the admin instance.) [Docs](https://firebase.google.com/docs/admin/setup)
  + database.bucket = "Your storage bucket URL" [Docs](https://firebase.google.com/docs/storage/web/start)


NOTE: You need to create the service-account.json file on the Firebase console

see url: ___

Do not commit this file to the project repo.



## Initialization

Keep in mind that once you set these variables, they are stored in the firebase project itself, not in your local machine. There is no need to set them again if you switch to another computer.

**IMPORTANT:** *The pirvate keys ARE PRIVATE, do not upload to github nor share those key in the web. This is sensitive data that should remain saved on a local machine, under the responsibility of the administrator of the project.*

If you are not sure about how to get these keys, please refer to the documentation of each library.
