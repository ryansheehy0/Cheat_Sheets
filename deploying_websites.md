[Home](./README.md)

# Deploying Websites

## Table of Contents
<!-- TOC -->

- [Deploying Websites](#deploying-websites)
  - [Table of Contents](#table-of-contents)
  - [Github Pages](#github-pages)
  - [Heroku](#heroku)
    - [Website](#website)
    - [Terminal](#terminal)
    - [Using keys](#using-keys)
    - [MySQL](#mysql)
  - [Netlify](#netlify)

<!-- /TOC -->

## [Github Pages](#table-of-contents)
1. Push your code to git. Have your deployable code in the "docs" folder
  - Make sure it is all correct because it maybe hard to change the website once it is deployed
1. Go to "Settings" tab and click "Pages" on the left side
1. Change "none" to your branch you want ot deploy from
1. Change "/(root)" to "/docs"
1. Click "Save" and wait. It may take a while
  - Any new pushes to that branch should be automatically deployed
  - If any new changes are taking a very long time to deploy then you need to create a new repo with your code and deploy from that.

## [Heroku](#table-of-contents)

### [Website](#table-of-contents)
1. Login or create Heroku account at `https://id.heroku.com/login`
1. Click on top right "New" and click "Create new app"
1. Give an app name of `{github username}-{github repo name}`
  - Make sure to replace any spaces or underscores with dashes
  - You can name it whatever you want, but this is the recommended naming convention
1. Click create app
1. Go to "Deploy" tab and set your deployment method to github and connect your github repo
1. Got to "Settings" tab and set your buildpack to what your app is using.

### [Terminal](#table-of-contents)
1. Make sure to have the Heroku CLI installed at this link https://devcenter.heroku.com/articles/heroku-cli
  - On Linux: `curl https://cli-assets.heroku.com/install-ubuntu.sh | sh`
1. Run `heroku login` in the terminal
  - A website should popup and make sure to login there
1. Make sure your code is pushed to your git branch
1. Run `heroku git:remote -a my-app`, but replace my-app with the app name you gave.
  - This should create a new heroku location for git
1. Run `git subtree push --prefix my-subdirectory heroku master`, but replace my-subdirectory with your root directory and replace master with your branch you want to deploy from.
  - This will make Heroku use my-subdirectory as the root directory

### [Using keys](#table-of-contents)
- On the Heroku website go to Settings and click Show Config Vars
- In nodeJS use the package dotenv and use the Keys that are in your Config Vars

### [MySQL](#table-of-contents)
1. Go to Resources
1. Search for JawsDB MySQL
1. JAWSDB_URL should be automatically added in your config vars

## [Netlify](#table-of-contents)
1. `npm run build` to get a dist folder
2. Go to [netlify](https://app.netlify.com/)
3. Drag and drop dist folder into sites in netlify