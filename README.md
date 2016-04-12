# SlhashSDK for Android

#### Features

#### Getting Started

###### Integrate the SDK

```
compile 'com.slhash.sdk:SlhashSDK:1.0.0'
```

###### Setup the SDK

You must place `Slhash.setup()` in the `onCreate()` method of your `Application` subclass. Since Slhash needs Twitter to work, you have to set the Twitter consumer key and secret related to your app. Twitter consumer keys can be generated at [apps.twitter.com](https://apps.twitter.com). If your app takes care to store the session, you can initialize the SDK with the last retrieved session.

```
Slhash.setup(this, TWITTER_CONSUMER_KEY, TWITTER_CONSUMER_SECRET, settings.getSession());
```

If you are developing an app for an organization registered on Slhash, you can set this information on the SDK. This will filter all the results considered irrelevant for your organization.

```
Slhash.sharedInstance().setOrganization(ORGANIZATION_CODE);
```

