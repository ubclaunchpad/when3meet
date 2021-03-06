# HappyHour

## Scripts

### Project setup

First, make sure you have your local environment variables set up. To get access to the necessary keys, check the pins in the `#tm-when3meet` channel on Slack. Copy that file and save it as `.env.development.local` in the root directory.

Next, install dependencies:

```
yarn install
```

### Compiles and hot-reloads for development

```
yarn serve
```

### Compiles and minifies for production

```
yarn build
```

### Lints and fixes files

```
yarn lint
```

### Customize configuration

See [Configuration Reference](https://cli.vuejs.org/config/).

## Structure

### Feature Folders

We organized the folder structure using a feature-based approach. This means that views, components, and modules are organized based on the corresponding feature that they implement. For example, anything related to a user should be put in the `/user` folder.

Every feature folder contains two subfolders and at least a `client.ts` file:

```
<feature>/
├── components/
│   ├── PageSpecificComponent.vue
├── views/
│   ├── PageOne.vue
│   └── PageTwo.vue
└── client.ts
```

- The `views/` folder contains all _screens_ related to this feature. A screen is defined as a component that you can access by going to a particular URL (e.g. `/event`).
- The `components/` folder contains all components used _exclusively_ in the screens for this feature. If a component can be reused in multiple screens, it should belong in the root `common` folder.
- `client.ts` contains all the possible actions available for this feature. For a user for example, this can include things like `login()`, `loginWithGoogle()`, `register()`, etc.

### Common Modules

Everything that can be reused across multiple features belong in the root directory.

- The `common/` folder contains generic components that can be reused across screens. This includes things like `AppButton`, `AppSnackbar`, etc.
- The `assets/` folder contains miscellaneous media.
- `db.ts` is the entry point to `firestore`. This should be reused across the various `client.ts` files.

### Google Calendar

In addition to the Firebase environment variables, the following environment variables need to be added to `.env.development.local` to use the [Google Calendar client library](https://www.npmjs.com/package/@types/gapi).
1. VUE_APP_GOOGLE_SCOPE=https://www.googleapis.com/auth/calendar
2. VUE_APP_GOOGLE_CLIENT_ID=<Google OAuth 2.0 client ID>
The client ID can be obtained by navigating to the Google cloud console using team's Google account, choosing project with ID `happyhour-8606c`, navigating to APIs & Services, and then the client ID is found under `Credentials - OAuth 2.0 client ID`.