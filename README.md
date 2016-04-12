# SlhashSDK for Android

#### Features

#### Getting Started

###### Integrate the SDK

```
compile 'com.slhash.sdk:SlhashSDK:1.0.0'
```

###### Setup the SDK

You must place `Slhash.setup()` in the `onCreate()` method of your `Application` subclass. Since Slhash needs Twitter to work, you have to set the Twitter consumer key and secret related to your app. Twitter consumer keys can be generated at [apps.twitter.com](https://apps.twitter.com).

```
Slhash.setup(this, TWITTER_CONSUMER_KEY, TWITTER_CONSUMER_SECRET, settings.getSession());
```

```
Slhash.sharedInstance().setOrganization(AppConfig.target == null ? null : AppConfig.target.getCode());
```

