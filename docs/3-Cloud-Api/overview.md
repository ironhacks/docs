## Introduction


This repository contains the Firebase Cloud Function project that take care of the server duties on the IronHacks platform (the platform).

Keep in mind that the platform doesn't have a proper backend, the following cloud functions are all the platform needs in order to communicate with the firebase database (both the db and the storage).

For documentation about the client, go to [The IronHacks Platform repository.](https://github.com/RCODI/the-ironhacks-platform)

---

The need for a backend on the platform obey to three major components: the admin side, the previsualization of a project on the editor and the GitHub integration. All of these requirements are solve using one or more cloud function, saving us the cost of server maintenance.


## Repository


## References


## Development

__Dev Scripts and Build Utilities__

- serve
- start
- shell 


### Deploying

Once the configuration is done, the next step is to deploy your functions using the Firebase CLI:

```bash
firebase deploy --only functions
```

This command will deploy all the functions on the project, and know we can actually talk about the functions:
