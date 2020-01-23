
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
