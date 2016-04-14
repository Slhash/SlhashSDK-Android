# SlhashSDK for Android



#### Getting Started

###### Integrate the SDK

Add to your app build.gradle file

```
repositories {
    maven {
        url "https://dl.bintray.com/slhash/maven"
    }
}

dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    testCompile 'junit:junit:4.12'
    
    compile ('com.slhash.sdk:slhash-sdk:1.0.0') {
        transitive = false
    }
}
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
#### Login on Slhash

The SDK uses and includes the Fabric library, so it will be automatically available also for your app. In order to login on Slhash you need to perform the Twitter login first. The `SHAuthenticationManager` takes care of the login on Twitter and Slhash. You have to implement the `SHAuthenticationManagerListener` in order to be notified when an event occurs (such us for example when the login has been succesfully executed).

```
SHAuthenticationManager slhashAuthenticationManager = new SHAuthenticationManager(this);
slhashAuthenticationManager.setListener(new SHAuthenticationManagerListener() {
	@Override
	public void willLogIn() {
		// Login process has started.
	}

	@Override
	public void didLoggedIn(SHSession session) {
		// Succesfully logged in, store the session and enter the app.
	}

	@Override
	public void didLoggedOut() {
		// Succesfully logged out, clear the session and exit the app.
	}

	@Override
	public void didFailLoginWithError(Exception error) {
		// Failed to log in, manage the error.
	}
});
```

You can choose beetween useing the Fabric's `TwitterLoginButton` and a custom button to execute the login.

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

#### Start and stop the Twitter stream

Slhas uses the Twitter user stream in order to get updates. You can start and stop it easely.

```
Slhash.sharedInstance().startStream();
```

```
Slhash.sharedInstance().stopStream();
```

#### Listen for Slhash updates and events

By implementing and registering an `SHEventsListener` your app will be notified about transaction update events or when the session is expired. You can register as many listener as you want.

```
public interface SHEventsListener {
	void onSlhashTransactionUpdated(SHTransaction transaction, SHTweet tweet);
	void onSlhashSessionExpired();
}
```

```
Slhash.sharedInstance().registerListener(listener);
```

```
Slhash.sharedInstance().unregisterListener(listener);
```
#### Slhash Syntax

SlHash uses a @,#, / triplet to specify command, actions, replies and transaction requests over ordinary Twitter messages. Ordinary text is intermixed with Twitter standard notations like @ and # and SlHash characteristic notation, that is  /. 

A SlHash message is composed by the following parts:
* source: it is implicitly defined;
* destination: it should appear in text but it could be implicitly defined;
* type of message: it is defined on the receive side and must be specified at the sending end;
* text: the actual text that follow the SlHash specification; 
* image: can be  optionally attached to a message and can contain a QRCode used to share a larger amount of data;
* options: define specific characteristics of the message.

A special option is the 4-hex code added at the end of each message to make it unique between a sender and  a receiver on Twitter.

The service syntax definition is
* `#<service>`
* if not defined a default behavior is invoked, ordinarily a #INFO service

The command syntax definition is:
* `/<command>`
* `/<command>=<value>` (`<param>` is implicit)
* `/<command>[=<param>:<value>[+<param1>:<value1>+…+<paramN>:<valueN>]]`
* `/<param>:<value>` (`<command>` is implicit)
* `/:<value>` (`<param>` and `<command>` are implicit)
* if not defined a default behavior is invoked, ordinarily a /info command

The `/#<command>=<value>` syntax  is left for SlHash system related communication (i.e. /#qr, /#cqr, /#app).

```
@SlhashOwner #SERVICE /command +param1=value1 +param2=value2 /#opt
```

#### Model

* `SHUser`: it rapresents a Slhash user (standard or owner).
* `SHTwitterUser`: it rapresents the Twitter user connected to a Slhash user.
* `SHServiceContainer`: it rapresents the service container structure defined for an owner.
	* `SHService`: 
	* `SHCommand`:
	* `SHParameter`:
* `SHTransaction`
	* `SHTransactionItem`

#### Services

Some of the [Slhash Rest APIs](http://slhash.ennova-research.com/documentation/api/service/index.html) are integrated in the SDK. `SHUserService` allows you to retrieve the user profile


#### Storage

[TODO]


