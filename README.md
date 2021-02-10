# Travis switching from OAuth to GitHub App

As you may have heard GitHub discontinues GitHub Oauth App's for integrations in May 2021. We've received all your feedback from users signing up on [travis-ci.com](http://www.travis-ci.com). We understand the access rights/permissions message that's issued by GitHub is causing a lot of anxiety from our users even though the GitHub App Install is actually used to access the repo's. 

## So, what's changing? 

Travis is going to change the authorization strategy we have currently, from logging into Travis CI via user by OAUth app, to logging in to Travis CI by using a GitHub App. 

## Why? 

There are several reasons as why this is needed to be done: 

- OAuth Application Authorizaion will be deprecated by GitHub in May 2021. 
- A lot of users don't want to grant permissions for private repos, if you are logging into Travis by OAuth App Travis CI will be asking about peromisisons for all repos. With the GitHub App installation the user will login with the base GitHub permissions, with access to his/her email (we have to store this into our databse). After logging in, the user will be asked to install the GitHub application on his/her GitHub Travis account or for their org. He/She will be able to select which repositories should have been shared with Travis CI. 

## What should we explain? 

- We need code snippets
- Transparency items

## Changes in present Travis CI GitHub application 

- We have to extend permissions into the GitHub Application
- Repo Admin read/write is needed for adding/deleting deploy keys
- Emails access for user account, - we need this for confirmation email, notifcations and pricing. 

After the change in app permissions, the GitHub/Travis user will receive an email from GitHub that the Travis CI app needs to be accepted, please accept to continue.
