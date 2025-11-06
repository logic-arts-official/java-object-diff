# Using with Maven and Gradle

## Maven

In order to use java-object-diff with Maven, add this dependency to your POM:

```xml
<dependency>
	<groupId>de.danielbechler</groupId>
	<artifactId>java-object-diff</artifactId>
	<version>0.96</version>
</dependency>
```

## Gradle

For Gradle projects, add this to your `build.gradle`:

```groovy
implementation 'de.danielbechler:java-object-diff:0.96'
```

Or for older Gradle versions:

```groovy
compile 'de.danielbechler:java-object-diff:0.96'
```

That's it! Now you're ready to go!

## Dependency not found?

The library is published to Maven Central. It can take up to 2 hours after the release of a new version until it is actually mirrored to the Maven Central repository. So if it isn't available right away, please try again a few hours later. If after a couple of hours it's still not available, feel free to [report the issue](https://github.com/logic-arts-official/java-object-diff/issues), so we can investigate.