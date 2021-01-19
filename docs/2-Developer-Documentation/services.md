
# Preparation

The Ironhacks Platform (the platform) use the following firebase services:

+ [Authentication](https://firebase.google.com/docs/auth)
+ [Cloud Firestore](https://firebase.google.com/docs/firestore)
+ [Storage](https://firebase.google.com/docs/storage)
+ [Hosting](https://firebase.google.com/docs/hosting)
+ [Cloud Functions](https://firebase.google.com/docs/functions)
+ [Firebase Auth UI](https://firebase.google.com/docs/auth/web/firebaseui)

We assume you are familiarized with all these services, how they work, and how to code using them. If you are not familiarized with them please check the Firebase documentation.

The platform also use the following frameworks/third party libraries:

+ [React](https://reactjs.org/docs/getting-started.html)
+ [react-router-dom](https://reacttraining.com/react-router/)
+ [Styled-components](https://www.styled-components.com/)
+ [react-codemirror2](https://github.com/scniro/react-codemirror2)
+ [Bootstrap](https://getbootstrap.com/) *Deprecated - we are removing this library in future versions. If you are going to update the repo, __don't use it.__*
+ [Moment-js](https://momentjs.com/)
+ [react-moment](https://github.com/headzoo/react-moment#readme)
+ [react-day-picker](https://react-day-picker.js.org/)
+ [react-mde](https://github.com/andrerpena/react-mde#readme)
+ [sweetalert2](https://sweetalert2.github.io/)
+ [react-treebeard](https://github.com/storybookjs/react-treebeard)

We assume you are familiarized with all these librarires, how they work, and how to code using them. If you are not familiarized with them please check the documentation of each one.

# Project structure

The platform is a follow the react-create-app structure:

- ./
- .gitignore
- firebase.json
- package.json
- readme.md
- public/
  - All the standard react-create-app files
- source/
  - img/
    - Global images
  - js/
    - source files and entry point.

We will get into details on the contents below.
