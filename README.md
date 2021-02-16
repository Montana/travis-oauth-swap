# Travis switching from OAuth to GitHub App

As you may have heard GitHub discontinues GitHub Oauth App's for integrations in May 2021. We've received all your feedback from users signing up on [travis-ci.com](http://www.travis-ci.com). We understand the access rights/permissions message that's issued by GitHub is causing a lot of anxiety from our users even though the GitHub App Install is actually used to access the repo's. 

## So, what's changing? 

Travis is going to change the authorization strategy we have currently, from logging into Travis CI via user by OAUth app, to logging in to Travis CI by using a GitHub App. Acessing particular repositories via GitHub App remains unchanged.

## Why? 

There are several reasons as why this is needed to be done: 

- OAuth Application Authorizaion will be deprecated by GitHub in May 2021. 
- A lot of users don't want to grant permissions for private repos, if you are logging into Travis by OAuth App Travis CI will be asking about permisisons which GitHub interprets as access rights for all repos. With the GitHub App installation the user will login with the base GitHub permissions, with access to his/her email (we have to store this into our databse). After logging in, the user will be asked to install the GitHub application on his/her GitHub Travis account or for their org. He/She will be able to select which repositories should have been shared with Travis CI. 

## When?

We will remove GitHub OAuth application integration from https://travis-ci.com completely within a week from publishing this particular blog post.
The https://travis-ci.org will remain active for several more weeks in order to allow users to sign-up with https://travis-ci.com. It will be deactivated before May 2021.

## How Travis CI exercises access rights 

Travis CI uses your GitHub account data to verify your identity with GitHub. The source code for that can be found [in this repository](https://github.com/travis-ci/travis-vcs).

Travis CI uses the access granted by user to GitHub in following scenarios:

1) Travis CI’s system synchronizes certain metadata with GitHub. This metadata is required for proper service functioning. In particular, we sync users, orgs, memberships, repos, permissions and, (optionally) branches. This type of sync happens either once a day by schedule or per the user’s request. You can find more information and source code [in this repository](https://github.com/travis-ci/travis-github-sync#syncs)

2) In order to run builds, Travis CI’s system clones a repository, from which the build is triggered, to the build environment. The build environment is an isolated virtual machine or an LXD container, which gets terminated as soon as the build finishes. Cloning happens only after a build request, and therefore only for the repositories explicitly enabled at GitHub settings.

3) To set up a build environment and prepare the build, Travis CI’s system fetches and processes the .travis.yml config file from the repository and the branch explicitly specified in the build request, triggered by GitHub.

4) Travis CI’s system reports build results back to GitHub via its [Checks API](https://developer.github.com/v3/checks/).

Above is applicable regardless of which authentication and authorization method Travis CI uses with GitHub.

## How the process with GitHub App Installation only will look like?

There are several steps involved, not much changes in the terms of general flow. Please read through the following to understand the details.

### Granting access rights upon sign-up and later

Once a user signs-up with https://travis-ci.com using their GitHub account, Travis CI requests certain access rights. GitHub displays these as follows:

(picture placeholder)

**Please note:** **At this point Travis CI has no access to your repositories.** There's a notification of 'Act on your behalf' in the message rendered by GitHub. This message comes directly from Github and we are fully aware it may be confusing, as it's been raised multiple times by users of applications that integrate with GitHub via GitHub App Installation. Amending the wording here is possible only for amazing GitHub team, therefore we recommend watching [GitHub changelog](https://github.blog/changelog/) and [GitHub Public Roadmap](https://github.com/github/roadmap) for any signs of the change. This is also a reason why we employ full transparency policy on how Travis CI exercises it's access rights as described above. 

You will be prompted for which user or organization account these access rights are to be granted.

When the Travis CI installation has completed, you will see the actual Travis CI GitHub Application installed in [Installed GitHub Apps](https://github.com/settings/installations) section of your GitHub account.

### Granting access rights to all or selected repositories

Once sign-up and Travis CI GitHub App installation is completed, you may select which repositories you want activate for use with Travis CI via https://travis-ci.com:

(picture placeholder)

It'll redirect you to the github...

## Changes in present Travis CI GitHub application 

- We have to extend permissions into the GitHub Application
- Repo Admin read/write is needed for adding/deleting deploy keys
- Emails access for user account, - we need this for confirmation email, notifcations and pricing. 

After the change in app permissions, the GitHub/Travis user will receive an email from GitHub that the Travis CI app needs to be accepted, please accept to continue.
