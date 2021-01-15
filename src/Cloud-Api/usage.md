
## GitHub API

- [__commitToGitHub__](#committogithub)
- [__createGitHubRepo__](#creategithubrepo)


The flow here is quite simple, we a user creates a project, create that project in two different places: The user's firebase storage folder and the GitHub organization specified on the initialization section.

The user will query the Firebase storage when using the platform, so we always store the latest version of the user project there. However, for the judger to work, we ask the user to "push" the version that is going to be evaluated. This "push" actually pushes the files to the GitHub repo.

So the judger can retrieve them from GitHub.

Keep in mind that this is transparent for the user.

__Github Configuration__

```js
const github = require("octonode");
const githubPersonalAccessToken = process.env.GITHUB_ACCESS_TOKEN;
const client = github.client(githubPersonalAccessToken);
const ghme = client.me();
const ghorg = client.org("UNALIronHacks");

module.exports = {
  github: github,
  client: client,
  me: ghme,
  org: ghorg,
};
```



Let's start by the GitHub repository creation:

### createGithubRepo

Parameters:

```javascript
const newRepoConfig = {
  name: projectName,
  description: 'UNAL-ironhacks-spring-2019',
  private: true,
  auto_init: true,
}
```

```javascript
exports.createGitHubRepo = functions.https.onCall(async (data, context) => {
  try {
    const result = await ghorg.repoAsync(data);
    return result;
  } catch(err) {
    return {message: 'Error', error: err, status: 500};
  }  
})
```

This function is really simple, is just a call to the Octonode library (check [their docs](https://github.com/pksunkara/octonode)) to create a new empty repo.


Please refer to the [Octonode docs](https://github.com/pksunkara/octonode) to understand how ```ghrepo.contentsAsync```, ```ghrepo.updateContentsAsync``` and ```ghrepo.createContentsAsync``` works.


### commitToGitHub

Main function that submits the committed files to the GitHub API

```js
const commitToGitHub = functions.https.onCall(async (data, context) => {
  const ghrepo = gh.client.repo("UNALIronHacks/" + data.name);

  const { commitMessage, files } = data;
  const result = await commitChanges(commitMessage, files, ghrepo);
  return result;
});
```


### Project Editor

- __previewWebServer__

### Account Management

- __registerUser__


### Utilities

- __getPhaseResults__
- __getTaskDoc__
- __saveLikedCompetitors__
- __saveStat__

### Amazon SES & Forum

- __newThreadEmailNotification__



```javascript
admin.initializeApp({
  credential: admin.credential.cert(serviceAccount),
  databaseURL: functions.config().database.url
});

```

Besides import the libraries required (we will address them on the fuctions in where they are used, if needed), there are some importants things you should check:

```javascript
const newThreadEmailNotification = require('./amazonSESfunctions');
```
The email functionality is in it own js file, and we import them here just to export it amogn the bundle. (We will address it at the end)

```javascript
const serviceAccount = require('./service-account.json');
```

Here we import our Firebase project keys from a local file, remember, you *__should not__* upload this file to the repository.

And just after that, we initialized the Firebase admin library:

```javascript
admin.initializeApp({
  credential: admin.credential.cert(serviceAccount),
  databaseURL: functions.config().database.url
});
```

Notice how we access to the env variables in order to get the database URL.

Here we catch the personal key from the env variables, then we use it to create the instance of github octonode.

```javascript
const githubPersonalAccessToken = functions.config().githubapi.personalkey;
```

And then we create the "user" object and also select the organization on which we will create the repositories of the projects. Remember that this have to be a PRO user and a PRO organization in order to be able to create private repos.

(Please check the [Octonode docs](https://github.com/pksunkara/octonode) if you feel rusty here); in this case the organization is called "UNALIronhacks", this was the one we used back then, you should put your own one there.

```javascript
const ghme = client.me();
const ghorg = client.org('UNALIronHacks');
```

## Registration Process

The first group of functions is related with the registration process of an user and is composed by two functions:

```javascript
exports.registerUser = functions.https.onCall((data, context) => {...})
const getNewParticipantForumId = (hackId, userId) => {...}
```

As you can see, only one function is exported, `registerUser`.

`getPartipantForumId` is and utility used by the first one.

---

### registerUser(hackID)

On ```./functions/index.js```

Parameters:

```json
{ "hackId": "hackId"}
```

hackId is the id from a hack documment on the database.


```javascript
exports.registerUser = functions.https.onCall((data, context) => {
  return db.collection("adminHackData")
  .doc(data.hackId)
  .set({
    registeredUsers: admin.firestore.FieldValue.arrayUnion(context.auth.uid)
  }, {merge: true})
  .then((result) => {
    return getNewParticipantForumId(data.hackId, context.auth.uid)
    .then((forum) => {
      return db.collection('users')
      .doc(context.auth.uid)
      .set({
        hacks: admin.firestore.FieldValue.arrayUnion(data.hackId),
        forums: forum,
      }, {merge: true})
      .then((result) => {
        return {message: 'success', status: 200};
      })
      .catch(error => {
        return {message: error, status: 500};
      })
    })
    .catch(error => {
      return {message: error, status: 500};
    })
  })
  .catch(error => {
      return {message: error, status: 500};
  })
});
```

This function will retrieve the hack data corresponding with the hackId sended as parameter from the adminHackData colletion, it will add the userID to the registeredUsers array and update the hack document. Then, it will ask for the forumID the user was register on and will update the user's documment, adding the hackID and the forumID to it.

---

### getNewParticipantForumId(hackId, userId)

On ```./functions/index.js```

Parameters:

```
hackID : String
userID : String
```

```javascript
const getNewParticipantForumId = (hackId, userId) => {
  return db.collection("forums")
  .where('hack', '==', hackId)
  .get()
  .then((querySnapshot) => {
    let selectedForum;
    let forumParticipants = -1;
    querySnapshot.forEach((doc) => {
      const legth = Object.keys(doc.data().participants)
      if(forumParticipants === -1){
        selectedForum = doc;
        forumParticipants = Object.keys(doc.data().participants);
      }else if(Object.keys(doc.data().participants).length < forumParticipants.length){
        selectedForum = doc;
        forumParticipants = Object.keys(doc.data().participants);
      }
    });
    return db.collection('forums').doc(selectedForum.id)
    .set({participants: {[userId]: `Hacker ${forumParticipants.length + 1}`}}, {merge: true})
    .then(() => {
      const forum = {};
      forum[hackId] = {id: selectedForum.id};
      return forum;
    })
    .catch(error => {
      return {message: error, status: 500};
    })
  }).catch(error => {
      return {message: error, status: 500};
  })
}
```

This function will search into the formus of a given hack (hackID) the one which have the less participants registered on, then it will register the new participant (userID) on it and will return the forum id.

## Project Editor

Now we are going to describe the function related with the project editor:

```javascript
exports.previewWebServer = functions.https.onRequest((req, res) => {...})
```

Although you could say that the Github API are also related, for the sake of consistency, we are going to separate the thirdh party ones from this group.

One of the biggest needs to the platform is to be able to preview the mockup that is being developed by a participant. Basically, to have a web server. However, What the platform tryes to do here is to mimik the behaviour of a web server, using only cloud functions. Even if a first glance it looks like an over engineered solution, the idea here is to have the less amount of compoenents posible and create a platform easy to use.

### Preview (AKA Web Server)

The preview system relies on to key components, the ```previewWebServer``` function and the rewrite is defined on the config file:

On ```./firebase.json```

```json
...
  "rewrites": [
    {
      "source": "/preview/**",
      "function": "previewWebServer"
    },
    {
      "source": "**",
      "destination": "/index.html"
    }
  ]
},
...
```

First, let's look the config file: We are redirecting everything that go to the preview url to call the previewWebServer function, this allow the function to be triggered whenever a file for a given is requested. Let's check the function itself:

```javascript
exports.previewWebServer = functions.https.onRequest((req, res) => {
  const filePathStorage = req.originalUrl.replace('/preview', '');
  const fileName = path.basename(filePathStorage);

  const tempPath = path.join(os.tmpdir(), `${fileName}`);
  return storage
  .bucket(functions.config().database.bucket)
  .file(filePathStorage)
  .download({
    destination: tempPath,
  }).then(() => {
    res.sendFile(tempPath, (err) => {
      if (err) {
        return res.end();
      }else{
        return res.end();
      }
    });
  }).catch((error) => {
    console.error(error.message);
    if(error.message === 'Not Found') {
      console.error('File not found', filePathStorage);
      return res.status(404).send('File not found on storage');
    }else{
      return res.status(500).send(error.message);
    }
  })
});
```

We call this function directly from the browser (since the idea is to replicate a web server), and the structure of the URL is the following:

```javascript
const projectURL = `${Constants.cloudFunctionsProdEndPoint}/previewWebServer/${this.state.user.uid}/${this.state.projectName}/index.html`;
```

The Constants.cloudFunctionsProdEnd is the endpoint of your firebase cloud functions project.

This function will retrieve the resource requested on the path, in this case, we allways start by de index.html. Once the index.html is loaded by the browser, it will call again the same function in order to load additional assets, for example, a javascript file.

Since we rewrite de function, everytime the browser request other file, like ```js/main.js``` it will be redirected to the previewWebServer function, and it will retrieve the file.

Keep in mind that this function retrieve the files from the Firebase storage service.


# Experiment related functions

Since the main idea of the platform is to create specific conditions related with the experiment that is being done, the platform exposes 4 particular functions that will help you to do that:

```javascript
exports.getTaskDoc = functions.https.onCall((data, context) => {...}
exports.saveStat = functions.https.onCall((data, context) => {...}
exports.getPhaseResults = functions.https.onCall((data, context) => {...}
exports.saveLikedCompetitors = functions.https.onCall((data, context) => {...}
```

Let's start by the most basic:

### getTaskDoc

This function return the Task document, this is the documment that contains the challenge or problem the participants of a hack will face. Keep in mind that the document will only be served if the publish date already pass. Also keep in mind that the content of the file is encode in base64.

```javascript
exports.getTaskDoc = functions.https.onCall((data, context) => {
  const currentDate = new Date();
  return db.collection("adminHackData")
  .doc(data.hackId)
  .get()
  .then((doc) => {
    const seconds = doc.data().task.releaseDate._seconds
    const nanoseconds = doc.data().task.releaseDate._nanoseconds
    const releaseDate = new admin.firestore.Timestamp(seconds, nanoseconds).toDate();
    if(releaseDate < currentDate){
      return {task: doc.data().task.doc};
    }else {
      return {error: 'To early', status: 500};
    }
  })
  .catch(error => {
    console.error(error);
    return {message: error, status: 500};
  })
});
```

### saveStat

The platform allows you to collect stats, you can pretty much collect every single interaction and saving it on the database by calling this function:

```javascript
exports.saveStat = functions.https.onCall((data, context) => {
  const currentDate = new Date();
  data.date = currentDate;
  return db.collection("stats")
  .add(data)
  .then(function(docRef) {
    return {"result": "job done", "status": 204};
  })
  .catch(function(error) {
    console.error("Error adding document: ", error);
    return {"error": error, "status": 500};
  });
});
```

Basically, you call it from the client, and sent an object as parameter, this object should keep the following structure:

```javascript
stat = {
  event: 'the name of the stat',
  metadata: {...},
  userId: 'a user id',
}
```

On the metadata object you can store pretty much anything, is just complementary information to the stat itself.

# Amazon SES

The integration with Amazon SES is pretty simple, we set a trigger on the comments collection that is activated when a new documment is done on that collection:

```javascript
exports.newThreadEmailNotification = functions.firestore
.document('comments/{commentId}')
.onCreate(newThreadEmailNotification);
```
The function called on the trigger is ```newThreadEmailNotification```

*On: ./funtions/amazonSESFunctions*

```javascript
module.exports = newThreadEmailNotification = (doc, context) => {
  const commentData = doc.data();
  let subject = 'The Ironhacks Platform - There is a new comment on a topic you commented! check it out!'
  commentData.id = doc.id;

  if (commentData.forumId) {
    subject = 'The Ironhacks Platform - There is a new topic on the forum! check it out!'
  }

  const params = {
    Destination: {
      ToAddresses: [
        'example@example.com',
      ],
    },
    Message: {
      Body: {
        Html: {
          Charset: 'UTF-8',
          Data: forumActivityTemplate
          .replace('[topic-title]', 'a title')
          .replace('[comment-body]', commentData.body)
          .replace('[thread-id]', commentData.threadID),
        },
        Text: {
          Charset: 'UTF-8',
          Data: `
           The Ironhacks <Platform></Platform>

           Hey! there is a new [item-type] posted on the forum! check it out!

           ${commentData.title}
           ${commentData.body}

           https://ironhacks.com/forum/thread/${commentData.id}


           This is an automatic email, do not reply.
           `,
        },
      },
      Subject: {
        Charset: 'UTF-8',
        Data: subject,
      },
    },
    Source: 'RCODI <researchopendigitalinnovation@gmail.com>',
    ReplyToAddresses: [
      'researchopendigitalinnovation@gmail.com',
    ],
  };

  const sendPromise = new AWS.SES({
    apiVersion: '2010-12-01',
  }).sendEmail(params).promise();

  return sendPromise.then((data) => {
    console.log(`Forum activity email sent ${data.MessageId}`);
    return true;
  }).catch((error) => {
    console.error('Forum activity email not sent', error, error.stack);
  });
};
```
