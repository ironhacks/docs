
## Requirements

- node.js
- mongoDB


## Setup

Clone the repo `rcodi/the-ironhacks-platform`

```sh
git clone git@github.com:RCODI/the-ironhacks-platform.git
```

```
cd the-ironhacks-platform
```


Install the dependencies:

```sh
npm install --save-dev
```

Start MongoDB:

```sh
mongod
# or
sudo mongod
```

## Configuration

Before starting the app, you will have to create a file named `.env`, containing:

```env
GITHUB_CLIENT=...
GITHUB_SECRET=...
SENDGRID_KEY=...
MONGODB_URI=mongodb://localhost/purdue_ironhacks
```

You can get the GitHub keys after creating a GitHub application. Do not share these with anyone.



# Setting up the dev environment

You must have installed [node.js](https://nodejs.org/en/) on your local machine. *We assume you already have a firebase project up with the platform*

The first thing you must do is clone this repository to you local machine and install all the npm packages:

```bash
git clone https://github.com/RCODI/the-ironhacks-platform.git
cd the-ironhacks-platform
npm i
```

Now yoy can start the local server via npm start:

```bash
npm start
```
