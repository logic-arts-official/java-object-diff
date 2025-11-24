## Introduction

`java-object-diff` is a simple, yet powerful library to find differences between Java objects. It takes two objects and generates a tree structure that represents any differences between the objects and their children. This tree can then be traversed to extract more information or apply changes to the underlying data structures.

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Maven Central](https://img.shields.io/maven-central/v/de.danielbechler/java-object-diff.svg)](https://search.maven.org/artifact/de.danielbechler/java-object-diff)

## Quick Start

### Installation

#### Maven
```xml
<dependency>
    <groupId>de.danielbechler</groupId>
    <artifactId>java-object-diff</artifactId>
    <version>0.96</version>
</dependency>
```

#### Gradle
```groovy
implementation 'de.danielbechler:java-object-diff:0.96'
```

### Basic Usage

```java
// Create two objects to compare
Map<String, String> working = Collections.singletonMap("item", "foo");
Map<String, String> base = Collections.singletonMap("item", "bar");

// Compare them
DiffNode diff = ObjectDifferBuilder.buildDefault().compare(working, base);

// Check for changes
if (diff.hasChanges()) {
    diff.visit(new DiffNode.Visitor() {
        public void node(DiffNode node, Visit visit) {
            System.out.println(node.getPath() + " => " + node.getState());
        }
    });
}
```

## Key Features

* **Zero Configuration** - Works out-of-the-box with almost any Java object
* **Deep Comparison** - Handles nested objects, collections, and maps
* **Flexible Configuration** - Extensive API to customize behavior
* **Non-Invasive** - No changes required to existing classes
* **Circular Reference Detection** - Handles circular references gracefully
* **Bidirectional Access** - Read and write access to underlying objects
* **Type-Safe** - Strongly typed API
* **Minimal Dependencies** - Only requires SLF4J
* **Java 8+** - Compatible with Java 8 and above

## Documentation

* [Getting Started Guide](getting-started.md) - Learn the basics
* [User Guide](user-guide.md) - Comprehensive API overview
* [Maven/Gradle Setup](maven.md) - Installation instructions
* [Merging Objects](merging.md) - How to merge differences

## Why would you need this?

Sometimes you need to figure out, how one version of an object differs from another one. One of the simplest solutions that'll cross your mind is most certainly to use reflection to scan the object for fields or getters and use them to compare the values of the different object instances. In many cases this is a perfectly valid strategy and the way to go. After all, we want to keep things simple, don't we?

However, there are some cases that can increase the complexity dramatically. What if you need to find differences in collections or maps? What if you have to deal with nested objects that also need to be compared on a per-property basis? Or even worse: what if you need to merge such objects?

You suddenly realize that you need to scan the objects recursively, figure out which collection items have been added, removed or changed; find a way to return your results in a way that allows you to easily access the information you are looking for and provide accessors to apply changes.

While all this isn't exactly rocket science, it is complex enough to add quite a lot of extra code to your project. Code that needs to be tested and maintained. Since the best code is the code you didn't write, this library aims to help you with all things related to diffing and merging of Java objects by providing a robust foundation and a simple, yet powerful API.

This library will hide all the complexities of deep object comparison behind one line of code:

```java
DiffNode root = ObjectDifferBuilder.buildDefault().compare(workingObject, baseObject);
```

This generates a tree structure of the given object type and lets you traverse its nodes via visitors. Each node represents  one property (or collection item) of the underlying object and tells you exactly if and how the value differs from the base version. It also  provides accessors to read, write and remove the value from or to any given instance. This way, all you need to worry about is **how to treat** changes and **not how to find** them.

## Use Cases

This library is ideal for:

* **Activity Streams** - Track and display changes to objects over time
* **Audit Logs** - Generate detailed change logs for compliance
* **Conflict Resolution** - Detect and resolve concurrent modifications
* **Data Synchronization** - Sync objects between different systems
* **Version Control** - Implement versioning for domain objects
* **Permission-Based Updates** - Apply only authorized property changes

## Getting Help

* Check the [documentation](getting-started.md)
* Search [existing issues](https://github.com/logic-arts-official/java-object-diff/issues)
* Ask questions by [opening a new issue](https://github.com/logic-arts-official/java-object-diff/issues/new)

## Contributing

We welcome contributions! See our [Contributing Guide](../.github/CONTRIBUTING.md) to get started.