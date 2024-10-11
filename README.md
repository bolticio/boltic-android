# SDK Integration and Usage Guide

This guide provides a step-by-step approach to integrate a custom SDK into your Android application, including the setup of library dependencies and initializing the SDK for event tracking.

## Prerequisites

Ensure you have Android Studio installed and an Android project set up.

## Integration Steps

Open your `app/build.gradle` file and add the following line to the `dependencies` section:

```gradle
    implementation 'io.boltic:analytics:4.11.8'
```

This line instructs Gradle to include any `.aar` files located in the `libs` directory as dependencies for your project.

## Initializing the SDK

To use the SDK's functionalities, you must initialize it with the appropriate configurations.

### 4. SDK Initialization

In your application code, initialize the SDK as follows:

```kotlin
import io.boltic.analytics.* 

private val analytics = Analytics.Builder(context, "YOUR_ACCESS_KEY")
    .collectDeviceId(true)
    .logLevel(if (debugging)
        Analytics.LogLevel.VERBOSE
      else
        Analytics.LogLevel.NONE)
    .trackDeepLinks()
    .crypto(Crypto.none())
    .trackApplicationLifecycleEvents()
    .tag(System.currentTimeMillis().toString()).build()
```

Replace `"YOUR_ACCESS_KEY"` with your actual access key. Adjust the `debugging` variable according to whether you are in a debugging session.

## Tracking Events

The SDK allows you to track events throughout your application. Ensure that you do not call these tracking methods on the main or UI thread to avoid UI blocking.

### 5. Tracking Events Example

```kotlin
val pageTitle = "Sample Page Title"
val pageUrl = "https://example.com"
val event = "Page Viewed"
val page = mapOf("title" to pageTitle, "url" to pageUrl)
val mainContext = Options().putContext("page", page)

// Replace `key-values` with your event-specific key-value pairs
analytics.track(event, Properties().apply { putAll(mapOf("key1" to "value1", "key2" to "value2")) }, mainContext)
```

This example demonstrates how to track a "Page Viewed" event with additional context and properties.

## Conclusion

Following these steps, you can integrate and utilize the SDK in your Android application for analytics tracking. Customize the event tracking as per your application's requirements to gain valuable insights.
