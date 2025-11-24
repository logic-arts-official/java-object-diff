# Contributing

You discovered a bug or have an idea for a new feature? Great, why don't you send us a [Pull 
Request (PR)](https://help.github.com/articles/using-pull-requests) so everyone can benefit from it?

## Quick Setup for Developers

Getting started is easy. Follow these steps to check out and get up and running:

### Prerequisites

* Java 8 or higher (Java 17+ recommended)
* Git

### Setup Instructions

1. **Fork the repository**
   ```bash
   # Fork the java-object-diff repository on GitHub
   ```

2. **Clone your fork**
   ```bash
   git clone https://github.com/YOUR_USERNAME/java-object-diff.git
   cd java-object-diff
   ```

3. **Build the project**
   ```bash
   ./gradlew clean build
   ```
   
   This will:
   - Download dependencies
   - Compile the code
   - Run all tests
   - Generate JARs

4. **Run tests only**
   ```bash
   ./gradlew test
   ```

5. **Generate code coverage report**
   ```bash
   ./gradlew jacocoTestReport
   # Report will be in build/reports/jacoco/test/html/index.html
   ```

6. **Check for dependency updates**
   ```bash
   ./gradlew dependencyUpdates
   ```

### IDE Setup

**IntelliJ IDEA:**
1. Open the project directory
2. IDEA will auto-detect the Gradle project
3. Wait for dependency download to complete

**Eclipse:**
1. Import as Gradle project
2. Run `./gradlew eclipse` first if needed

### Making Changes

1. Create a new branch for your work:
   ```bash
   git checkout -b feature/my-new-feature
   ```

2. Make your changes

3. Build and test:
   ```bash
   ./gradlew clean build
   ```

4. Commit and push:
   ```bash
   git add .
   git commit -m "Description of changes"
   git push origin feature/my-new-feature
   ```

5. Create a Pull Request on GitHub

## Development Guidelines
  
There are some things to help you getting started:

* Make yourself familiar with the [__User Guide__](../docs/user-guide.md), so you understand the basic architecture.
* [__Check for open issues__](https://github.com/logic-arts-official/java-object-diff/issues) that interest you or look for issues with the __Help Wanted__ or __Good First Issue__ tags. These issues are especially well suited to get more familiar with the codebase without being overwhelming.
* In case you have an idea for a new feature, check the issue tracker to see if there were already some discussions regarding that feature. If not, feel free to open a new discussion to see what others think about it.

So you found something you want to work on? That's great! If you run into any problems or are not entirely sure how to tackle the problem, feel free to post your question to the [issue tracker](https://github.com/logic-arts-official/java-object-diff/issues).

## Before Submitting Your PR

Please make sure to:

* __Write at least one fully integrated test__ (no mocks and comparison done via public API) to show 
that the fix or feature works as promised - from a user perspective. What you are doing here is 
basically saying: "In case of X you can expect the library to behave like Y". You shouldn't cover 
every possible execution path this way but rather focus on proving that the feature works and under 
which circumstances it will take effect. Doing this will help others to keep your feature intact, 
when the library evolves.	
* __Write unit tests__! Lots of them! Keep them small and readable and try to cover as much of your logic as possible. But don't go overboard: focus on actual logic and avoid testing simple getters and setters just to reach the magical 100% test coverage.
* __Write your tests with Groovy and [Spock](https://spockframework.org/)!__ 
Spock is an amazing testing framework that makes many things much, much easier to accomplish. 
It's not hard to learn and a lot of fun to use.

When you've done that, nothing should hold you back from sending us a pull request. :wink:

Thanks for your support and happy coding!
