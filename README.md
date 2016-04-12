# SlhashSDK for Android



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

###### Login on Slhash

###### Start and stop the Twitter stream

The SDK uses and includes the Fabric library, so it will be automatically available also for your app. In order to login on Slhash you need to perform the Twitter login first. The `SHAuthenticationManager` takes care of the login on Twitter and Slhash. 

```
SHAuthenticationManager slhashAuthenticationManager = new SHAuthenticationManager(this);
slhashAuthenticationManager.setListener(this);
```

You can choose if use the Fabric's `TwitterLoginButton` and execute the login with `SHAuthenticationManager.loginWithButton(TwitterLoginButton twitterLoginButton)` or if use a custom button and use the method `SHAuthenticationManager.login(Activity activity)`.

```
twitterLoginButton = (TwitterLoginButton) findViewById(R.id.twitter_login_button);
slhashAuthenticationManager.loginWithButton(twitterLoginButton);
```

```
loginButton = (Button) findViewById(R.id.login_button);
		myLoginButton.setOnClickListener(new View.OnClickListener() {
			@Override
			public void onClick(View v) {
				slhashAuthenticationManager.login(LoginActivity.this);
			}
		});
```



