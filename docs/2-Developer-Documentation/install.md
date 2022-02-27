
## Requirements

- node.js

## Setup

Clone the repo `rcodi/the-ironhacks-platform`

```sh
git clone git@github.com:ironhacks/ironhacks-app.git
```

```
cd the-ironhacks-platform
```

Install the dependencies:

```sh
npm install --save-dev
```

# Setting up the dev environment

The first thing you must do is clone this repository to your local machine and install all the npm packages:

Now you can start the local server via npm start:

```bash
npm run start
```


## Note

The Firebase config is injected during start or build from values set in the `.env ` file. These values should not be added to version control. 

```sh
REACT_APP_ENV="development"
REACT_APP_FIREBASE_APIKEY=""
REACT_APP_FIREBASE_APIKEY_DEV=""
REACT_APP_MESSAGE=""
```

These values can be found on the Firebase project settings.

https://console.firebase.google.com/
