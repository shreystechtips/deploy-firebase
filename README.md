# Deploy to Firebase

A GitHub Action to deploy to Firebase Hosting

- Make sure you have the `firebase.json` file in the repository
- Get the Firebase token by running `firebase login:ci` and [store it](https://help.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets) as the `FIREBASE_TOKEN` secret
- Set the project name in the `FIREBASE_PROJECT` env var

Example workflow

```
name: Build and Deploy
on:
  push:
    branches:
      - prod
jobs:
  build:
    name: Build and Deploy to Firebase Hosting
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repo
        uses: actions/checkout@master
      - name: Change to frontend repo
        run: cd ''
      - name: Install Dependencies
        run: npm install --prefix "/"
      - name: Build
        run: npm run build --prefix "/"
        env: 
      - name: Deploy to Firebase
        uses: shreystechtips/deploy-firebase@master
        env:
          FIREBASE_TOKEN: ${{ secrets.FIREBASE_SECRET }}
          BRANCH_NAME: BRANCH_TO_PUSH
          FIREBASE_PROJECT: FB_PROJ_NAME
          DEPLOY_DIR: /
```
