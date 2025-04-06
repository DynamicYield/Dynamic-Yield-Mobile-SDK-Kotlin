# Dynamic Yield Kotlin SDK

## Overview

The **Dynamic Yield Kotlin SDK**  provides a complete interface to our Experience API that covers all major implementation aspects, including tracking pageviews, assigning targeted experiences, and tracking clicks and events.

## Documentation & Resources

For detailed implementation guides, SDK references, and troubleshooting, refer to the following resources:

- [Implement Mobile SDKs on Your App](https://dy.dev/docs/implement-mobile-sdk)
- [Kotlin SDK Documentation](https://dy.dev/docs/kotlin)
- [Release Notes](https://github.com/DynamicYield/Dynamic-Yield-Mobile-SDK-Kotlin/releases)

## Installation Prerequisites

| OS      | MinSDK | Prerequisite                        |
| ------- | ------ | ----------------------------------- |
| Android | 24     | GitHub user & Personal Access Token |

### Generate a personal access token for GitHub

In you GitHub account:

1. If you don't have a user, register to Github.
2. Go to **Settings › Developer Settings › [Personal Access Tokens](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-personal-access-token-classic) ›[Generate new token](https://github.com/settings/tokens)**
3. Make sure you select the following scopes: ("`read:packages`") and Generate a token
4. Make sure to**copy your new personal access token. You won't be able to see it again!** Your only option if it's lost is to generate a new key.

## Installing the Kotlin SDK

### Add a dependency

Include the following dependency in your project, with the specific SDK version as follows (see examples):

- **Kotlin DSL:**  `build.gradle.kts`
- **Groovy:**`build.gradle`

```kotlin
dependencies {
    implementation("com.dynamicyield:dy-android-sdk:<VERSION>")
}
```

```java Groovy
dependencies {
    implementation 'com.dynamicyield:dy-android-sdk:<VERSION>'
}
```

### Add authentication

Because the package is hosted on GitHub Packages, authentication is required. Ensure that your `gradle.properties` contains:

```java Kotlin
github.username=GITHUB_USERNAME
github.token=GITHUB_PERSONAL_ACCESS_TOKEN
```

```groovy Groovy
github.username=GITHUB_USERNAME
github.token=GITHUB_PERSONAL_ACCESS_TOKEN
```

And update your repositories block in `build.gradle.kts` or `settings.gradle.kts`

```java Kotlin
import java.util.Properties

repositories {
        maven {
            val properties = Properties()
            file("gradle.properties").inputStream().use {
                properties.load(it)
            }
            url = uri("https://maven.pkg.github.com/DynamicYield/Dynamic-Yield-Mobile-SDK-Kotlin")
            credentials {
                username =
                    System.getenv("GITHUB_USERNAME") ?: properties.getProperty("github.username")
                password = System.getenv("GITHUB_TOKEN") ?: properties.getProperty("github.token")
            }
        }
}
```

```java Groovy
repositories {
    google()
    mavenCentral()
    maven {
        def properties = new Properties()
        file("gradle.properties").withInputStream { properties.load(it) }

        url = uri("https://maven.pkg.github.com/DynamicYield/DY-Android-SDK")
        credentials {
            username = System.getenv("GITHUB_USERNAME") ?: properties.getProperty("github.username")
            password = System.getenv("GITHUB_TOKEN") ?: properties.getProperty("github.token")
        }
    }
}
```

## Set up app permissions for network access (Android)

Because our SDK uses Experience APIs and makes network calls, it's mandatory to declare the necessary permissions in the `AndroidManifest.xml` file. This ensures that the app has the appropriate access to the internet for seamless API interactions.

To add network access, add the following permissions to your `AndroidManifest.xml` file:

```xml
<uses-permission android:name="android.permission.INTERNET" />
```
