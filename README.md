Android-RateThisApp
===================

Android-RateThisApp is an library to show "Rate this app" dialog.

![Screen shot](https://raw.github.com/kishandonga/Android-RateThisApp/master/screenshot_resized.png)

The library monitors the following status

* How many times is the app launched
* How long days does it take from the app installation

and show a dialog to engage users to rate the app in Google Play.

## Getting Started

### Dependency

```groovy
allprojects {
	repositories {
		maven { url 'https://jitpack.io' }
	}
}
```

```groovy
dependencies {
    implementation 'com.github.kishandonga:Android-RateThisApp:1.3.0'
}
```

### Basic usage

Call `RateThisApp.onCreate(Context)` and `RateThisApp.showRateDialogIfNeeded(Context)` in your launcher activity's onCreate() method.

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    // Monitor launch times and interval from installation
    RateThisApp.onCreate(this);
    // If the condition is satisfied, "Rate this app" dialog will be shown
    RateThisApp.showRateDialogIfNeeded(this);
}
```

That's all! You can see "Rate this app" dialog at an appropriate timing.

## Advanced usages

### Custom condition

In default, the dialog will be shown when **any of** the following conditions is satisfied.

* App is launched more than 10 times
* App is launched more than 7 days later than installation.

If you want to use your own condition, please call `RateThisApp.init(Configuration)` in your Application or launcher activity onCreate method.

```java
// Custom condition: 3 days and 5 launches
RateThisApp.Config config = new RateThisApp.Config(3, 5);
RateThisApp.init(config);
```

### Custom strings

You can override title, message and button labels.

```java
RateThisApp.Config config = new RateThisApp.Config();
config.setTitle(R.string.my_own_title);
config.setMessage(R.string.my_own_message);
config.setYesButtonText(R.string.my_own_rate);
config.setNoButtonText(R.string.my_own_thanks);
config.setCancelButtonText(R.string.my_own_cancel);
RateThisApp.init(config);
```

### Custom url

In default, rate button navigates to the application page on Google Play. You can override this url as below.

```java
RateThisApp.Config config = new RateThisApp.Config();
config.setUrl("http://www.example.com");
RateThisApp.init(config);
```

### Opt out from your code

If you want to stop showing the rate dialog, use this method in your code.

```java
RateThisApp.stopRateDialog(this);
```

### Callback

You can receive yes/no/cancel button click events.

```java
RateThisApp.setCallback(new RateThisApp.Callback() {
    @Override
    public void onYesClicked() {
        Toast.makeText(MainActivity.this, "Yes event", Toast.LENGTH_SHORT).show();
    }

    @Override
    public void onNoClicked() {
        Toast.makeText(MainActivity.this, "No event", Toast.LENGTH_SHORT).show();
    }

    @Override
    public void onCancelClicked() {
        Toast.makeText(MainActivity.this, "Cancel event", Toast.LENGTH_SHORT).show();
    }
});
```

## Contribute this project

If you want to contribute this project, please send pull request.
