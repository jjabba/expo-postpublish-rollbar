# expo-postpublish-rollbar

This project allows you to upload sourcemaps to rollbar as your expo powered react native app is beining published.
It closely maps to how expo deals with delivering sourcemaps to their preferred error reporting service sentry.

## Installation

1. `yarn add expo-postpublish-rollbar` in your project.
2. Add the following to your `app.json` within the "expo" key.

```javascript
  "hooks": {
    "postPublish": [
      {
        "file": "expo-postpublish-rollbar",
        "config": {
          "serverItemAccessToken": "YOUR_ROLLBAR_TOKEN",
          "minifiedUrlTemplate": "http://reactnativehost/{{url}}"
        }
      }
    ]
  }
```

3. Note that the minifiedUrlTemplate option is optional. If used, it allows you to customize the `minified_url` parameter passed to rollbar on upload.

## Reporting errors
This project does not deal with the actual integraion of rollbar reporting. But in order for the sourcemaps to work effectively it's important that you use the same `version` string when reporting errors as the one generated and used by this postPublish upload hook:

The currently used format for ios and android is:

     # iOS
     ['ios', iosManifest.ios.bundleIdentifier, iosManifest.ios.buildNumber].join('-')

     # Android
     ['android', androidManifest.android.package, androidManifest.android.versionCode].join('-')
