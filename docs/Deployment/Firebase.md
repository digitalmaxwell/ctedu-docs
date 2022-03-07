# Firebase

CTEDU Projects are hosted on Firebase, which provides us with an easy to use graphical backend interface. Firebase has an extensive tool set helping manage your domains, storage, authentication, realtime analytics and much more.

## Getting Started :fire:

You can access our dashboard here: https://console.firebase.google.com/u/1/project/ctedu-home-static/overview

In order to interact with firebase via CLI in a CTEDU project install firebase tools. [Learn More.](https://firebase.google.com/docs/functions/get-started#set-up-node.js-and-the-firebase-cli)


```
npm install -g firebase-tools
```

## Cloud Functions

The Firebase Cloud Functions give you access to a stripped down Node.js environment where you can quickly build APIs. It is very similiar to a AWS lambda function. [Learn More.](https://firebase.google.com/docs/functions/get-started#deploy-functions-to-a-production-environment)

We utilize this API within our app to submit data..


## Testing Locally

... more to come

```
firebase deploy --only functions
```