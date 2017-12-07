# Unit Tests

[//]: # (TODO: Update this once everything is finalized)
- Unit Test Definition and Composition ##
  - The Three A's ###
    - Assignment ###
- XCTest Library ##
    - Benefits ####
    - Adding XCTest to your Project ###
      - Assignment: Add a Test Target to an Existing Project ####
      - Assignment: Include Unit Tests in a New Project ####
- Using XCTest ##
  - Creating a Test Case ####
    - Assignment #####
  - XCTAssert ####
  - setUp() and tearDown() ####
    - Assignment: setup() and tearDown() ####
    - Assignment: Singletons and Member Variables ####
- Quiz ##

# Lesson Outline #

## Intro ##

"Unit testing is a software development process in which the smallest testable parts of an application, called units, are individually and independently scrutinized for proper operation."
-[searchofsoftwarequality.com](http://searchsoftwarequality.techtarget.com/definition/unit-testing)

Unit Testing is the vital process of writing code to validate or test your production code. It may seem trivial or time consuming, but having Unit Tests in your code allows a confidence and quality of code that is otherwise not possible.
Unit Tests are written as methods, which test a single _unit_ of the production code. A unit could be a method, a specific use case of a method, or even a class. When unit tests are written, they give you a quick way to test your code and validate that you haven't broken anything. This enables confidence that any change you make to your code in the future will not break the existing and expected functionality thereby introducing new bugs. That kind of confidence will let you sleep peacefully each night.


## Learing Outcomes ##

- What is a Unit Test?
- How do I create a unit test?
- How do I add unit tests to my project?
- How do I avoid cross contamination of tests?


## Vocabulary ##

- Unit Test, Test Case
- Automated Test Suite
- Arrange
- Act
- Assert
- XCTest
- XCTestCase
- XCTAssert
- Target


## Additional Resources ##

- [What Unit Tests are and why to use them.](http://www.extremeprogramming.org/rules/unittests.html)
- [Apple's documentation: Adding and Using XCTest](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/testing_with_xcode/chapters/04-writing_tests.html)
- [Overview of unit testing](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/testing_with_xcode/chapters/03-testing_basics.html)


## Quotes about Unit Testing ##

"The biggest resistance to dedicating this amount of time to unit tests is a fast approaching deadline. But during the life of a project an automated test can save you a hundred times the cost to create it by finding and guarding against bugs." http://www.extremeprogramming.org/rules/unittests.html

"When you create unit tests you guard your functionality from being accidentally harmed. " http://www.extremeprogramming.org/rules/unittests.html

"Unit tests enable refactoring as well. After each small change the unit tests can verify that a change in structure did not introduce a change in functionality." http://www.extremeprogramming.org/rules/unittests.html

"Unit Tests provide a safety net of regression tests and validation tests so that you can refactor and integrate effectively." http://www.extremeprogramming.org/rules/unittests.html

"It’s as close to a religious matter as programmers get, aside from the tabs-versus-spaces debate." http://nshipster.com/unit-testing/ _(Great resource website!!)_

"Unit testing is a software development process in which the smallest testable parts of an application, called units, are individually and independently scrutinized for proper operation." http://searchsoftwarequality.techtarget.com/definition/unit-testing



# Lesson #

## Unit Test Definition ##

Simply put, a unit test is a method revolving around at least one assertion. The purpose of a unit test is to exercise your production code and assert expected functionality. A "unit" is usually a function, but is technically [defined](http://softwaretestingfundamentals.com/unit-testing/) as _"the smallest testable parts of an application."_
With proper unit testing, there will be a _one to many_ relationship between class methods and unit tests (many tests per method to assert specific allowed and unallowed behavior).


### The Three A's ###

Unit tests will follow  the __AAA__ pattern:
1. __Arrange__: Prepare the state/input
2. __Act__: Call the method to be tested
3. __Assert__: Verify the correct output/state

For example, lets use the simple method `increment` as the production code we wish to test. We expect this method to return our input plus one.
```
func increment(_ value: Int) -> Int { ... }
```

We begin by __arranging__ the input:
```
let inputNumber = 3
```
Then we __act__ by calling the production code we wish to test:
```
let result = increment(inputNumber)
```
Finally, we __assert__ the expected functionality/result:
```
let expectedResult = 4
AssertEqual(result, expectedResult)
```
The result is a proper unit test, which verifies an expected behavior of production code:
```
func testIncrementAddsOne() {
    // Arrange
    let inputNumber = 3

    // Act
    let result = increment(inputNumber)
    let expectedResult = 4

    // Assert
    AssertEqual(result, expectedResult)
}
```

_*Often times the_ __arrange__ _step is the most difficult as the units (or functions) you wish to test are not merely floating functions (as the above example), but usually live on a class, which must be initialized and setup before executing the desired assertion. Structuring your code to be testable through Dependency Injection or Procedural Oriented Programming is often essential to enable the proper testing of a class unit._

### Assignment: Write your First Test Method! ###

Write your own function (similar to the one created above) to test the output of the method in this Playground:
-> Playground reference here.


## Adding Unit Tests to Your Project ##

Testing code is not production code, and as such it shouldn't be included in the same deliverable or __target__ as your production code. Targets are a cool concept and enable many of Apple's iOS features (iMessage apps, Widgets, Spotlight, Share, Unit Testing, etc.). Apple, with their great documentation, describes it as: "A target specifies a product to build and contains the instructions for building the product from a set of files in a project or workspace. A target defines a single product... Projects can contain one or more targets, each of which produces one product." - [Apple's documentation on Targets](https://developer.apple.com/library/content/featuredarticles/XcodeConcepts/Concept-Targets.html) In other words, a target is basically just a list of files that should be included when building and running a product, as well as some rules around how to build that product. Thus, we can create a "testing" target that will contain all of our testing code. When we build and run that target, it will _only_ run our unit tests! No waiting for simulator to launch; no asking permission to allow notifications or badging; no username and password required; and no waiting around for animations! Clean and slick. Perhaps more importantly though, this means our production code will stay clean and separate from our testing code. You don't have to worry about a unit test causing side effects that would affect user experience.

Xcode will do this part for us when you create a new Project if you select the checkbox for "Include Unit Tests".
![Unit Test Check Box](https://github.com/MTechMobileDevelopment/MTech-Extra-Lessons/Unit\ Tests/Resources/Create\ Project\ Check\ Boxes.png)

If you are working with an existing project that has no testing target, or you forgot to select that little checkbox when creating a new project, it's actually quite easy to add a testing target to a project manually.
To add a testing target to an existing project:
1. Select the blue Project file at the top of the _Project Navigator pane_ in the left side Navigator area. Tap the + button in the bottom left of the "Targets" section.
![Project Screen](https://github.com/MTechMobileDevelopment/MTech-Extra-Lessons/Unit\ Tests/Resources/Project\ Screen.png)

1. Search for "test" and select the "iOS Unit Testing Bundle" option, which will be found under the section of "Testing". Then tap "Next".
![Unit Testing Bundle](https://github.com/MTechMobileDevelopment/MTech-Extra-Lessons/Unit\ Tests/Resources/Unit\ Test\ Bundle.png)

1. Add a name for your target. By default Xcode will add "Tests" to the end of your project name.
Notice the section at the bottom labeled "Target to be Tested." You will likely only have one target, which will be your production target, and this will be the default selection. If you ever wanted to add tests to a separate target, say an iMessages target, you would select that "Target to be Tested" here.
1. Tap "Finish" to add the target to your project.
![Finish Page](https://github.com/MTechMobileDevelopment/MTech-Extra-Lessons/Unit\ Tests/Resources/Target\ to\ be\ Tested.png)

And that's it! Done! Finished! "Target"-ed!

You will now notice a shiny (not really) new folder added to your Project Navigator pane with the same name as your testing target. Within this folder you will find a sample XCTest class with bonus educational boiler-plate methods included (yay educational boiler-plate methods🎉).
![Unit Testing Folder](https://github.com/MTechMobileDevelopment/MTech-Extra-Lessons/Unit\ Tests/Resources/Unit\ Test\ Files.png)

### Assignment: Add a Test Target to an Existing Project ###
-> Project Reference Here


### Assignment: Include Unit Tests in a New Project ###
  1. Open Xcode
  1. Create a new Project
  1. Select _Single View App_ or any other iOS boiler-plate Application setup (excluding _Sticker Pack App_ and _iMessage App_) and tap __Next__.
  1. Fill in the required fields and select __Include Unit Tests__.
    - _Note the options for Include Core Data and Include UI tests. Fancy Eh? Core Data will come up in another lesson (spoiler!)._
  1. Choose a location to add this new project.
  1. Locate your testing folder conveniently added by Xcode❤️. It will be named: "<name of your project>Tests" (where <name of your project> is the name of your project...)


## Using the XCTest Framework ##

### Benefits ####

It is possible to add tests without a framework (as we did in the above Playground assignment), but doing so would cause a number of issues and would be extremely difficult. XCTest is greatest friend when it comes to unit testing. XCTest is the framework Apple has provided for testing in Xcode. Testing frameworks make adding test cases to your code quick and easy and also add additional functionality to your tests. XCTest enables the functionality of *performance measurement* (how long test take to execute etc.), *UI testing* (launches a simulator and tests the UI of the application through simulated taps and gestures), as well as *continuous integration and Xcode servers* (the ability to run the tests from the command line; in other words, you can automate the execution of your tests to happen after events such as a commit, a pull request, a 24 hour period, etc.).


### Creating a Test Case ###
Unit tests live inside of a class that inherits from `XCTestCase`. Unit tests are written like any normal method (usually without any parameters) but must begin with the word "test".
For example:
```
import XCTest

class CounterTests: XCTestCase {
    func testIncrementMethod_valueIsOneWhenCalled() { ... }
    // The method name must begin with "test"
}
```
The method name should be descriptive enough to give understanding to the error by merely seeing the method name in an error log. For instance `testMyCustomClass` is a very vague method name; seeing `Test Case 'testMyCustomClass' failed` would give no indication of what actually broke in that class. `testMyCustomClass_incrementLevelTo5_recievesAward` is a much more specific name; seeing `Test Case 'testMyCustomClass_incrementLevelTo5_recievesAward' failed` would give a very clear indication of what broke in your custom class. Since we will never be calling these test case method ourselves, such lengthiness only proves to our benefit as it provides immediate understanding in error logs.


##### Assignment: Create your First Test Method #####
// Playground referenced here.


### XCTAssert ###

Once you have _arranged_ and _acted_ in your test case, you will need to _assert_ the expected outcome. XCTest has provided many assert options for you to utilize in your test cases:

1. Basic Assertions:
  - `XCTAssert(expression: Bool)`
  - `XCTAssertTrue(expression: Bool)`
  - `XCTAssertFalse(expression: Bool)`
1. Equivalence Assertions:
  - `XCTAssertEqual(expression1: Equatable, expression2: Equatable)`
1. Comparison Assertions:
  - `XCTAssertLessThan(expression1: Comparable, expression2: Comparable)`
  - `XCTAssertLessThanOrEqual(expression1: Comparable, expression2: Comparable)`
  - `XCTAssertGreaterThan(expression1: Comparable, expression2: Comparable)`
  - `XCTAssertGreaterThanOrEqual(expression1: Comparable, expression2: Comparable)`
1. Nil Assertions:
  - `XCTAssertNotNil(expression: Any?)`
  - `XCTAssertNil(expression: Any?)`
1. Exception Throwing Assertions:
  - `XCTAssertNoThrow(expression: T)`
  - `XCTAssertThrowsError(expression: T)`

Each of these asserts will also allow an optional `, message: String` at the end of the method call.


### setUp() and tearDown() ###

_Arranging_ your data is perhaps the most difficult step in creating a unit test. Since many of your unit tests will likely revolve around a specific object, you will want to add a member variable to your XCTestCase class that you can reference in each test case, like so:
```
class CounterTests: XCTestCase {
    // convenience variable that is used in most of test cases.
    var incrementalObject: IncrementalObject

    func testIncrementMethod_valueIsOneWhenCalled() {
      incrementalObject.increment()
      XCTAssert(incrementalObject.value == 1)
    }

    func testIncrementMethod_valueIsTwoWhenCalledTwice() {
      // value == 0 because tests are executed independently of each other
      incrementalObject.increment()
      incrementalObject.increment()
      XCTAssertEqual(incrementalObject.value, 2, "Called increment twice on IncrementalObject, but value was not 2.")
    }
}
```

As a security feature, XCTestCase will actually compile each test case/method into its own class at run-time. This means that, for the most part, you don't have to worry about cross contamination between test cases (this is why `testIncrementMethod_valueIsTwoWhenCalledTwice()` will start with `value == 0` and not `1`). This safety feature can pose a problem, though, when your convenience variable requires some basic initialization and setup before it can be used by each test case. XCTestCase has provided the overridable methods `setUp()` and `tearDown()` to handle this problem. The code in these two methods will be executed before and after each test case, respectively.
However, this safety feature only protects you from the _most common_ cross contamination scenarios. It __does not__ protect you from cross contamination of singleton objects and static properties. You should be extremely cautious when handling these kinds of static variables in test cases. If you set a variable on a singleton in one test case, that value will remain altered on all subsequent test cases and will likely cause confusing, false negatives. Even method calls on singleton objects can have side effects of updating or setting a member variable on that singleton.

#### Assignment: setup() and tearDown() ####
-> Project reference here.


#### Assignment: Singletons and Member Variables ####
See if you can find out why the tests in the XCTestCase classes are failing.
-> Project reference here.


## Quiz ##

1. What string must the name of each test case begin with?
  1. "test"
  1. "XCTest"
  1. "case"
  1. There is no requirement for test case naming.
  [//]: # (Answer: 1. "test")

1. What are the three A's from the __AAA__ pattern? _Select all that apply_
  1. Act
  1. Account
  1. Assert
  1. Arrange
  1. Alive
[//]: # (Answer: 1, 3 and 4 - Arrange, Act, Assert)

1. If I change a member variable of my XCTestCase class in one test case, that member variable will remain changed for all future test cases.
  1. True
  1. False
  [//]: # (Answer: 1. False)

1. If I change a variable contained on a singleton object in one test case, that variable will remain changed for all future test cases.
  1. True
  1. False
  [//]: # (Answer: 1. True)

1. What is the name of the framework Apple has provided for unit test creation in Xcode?
  1. AppleTests
  1. XCTest
  1. NSTest
  1. Test
  [//]: # (Answer: 2. XCTest)

1. Which assert will check that `var returnValue: String` is equal to `var expectedValue: String`?
  1. `XCTAssert(returnValue == expectedValue)`
  1. `XCTAssert(returnValue == expectedValue, message: "The string value returned from myCustomStringCreatingMethod() is not correct.")`
  1. `XCTAssertTrue(returnValue == expectedValue)`
  1. `XCTAssertEqual(returnValue, expectedValue)`
  1. `XCTAssertFalse(returnValue != expectedValue)`
  1. Any of the above.
  [//]: # (Answer: 6. Any of the above)

1. You can test performance, or speed of execution using XCTest.
  1. True
  1. False
  [//]: # (Answer: 1. True)

1. The `setup()` and `teardown()` methods get called before/after each test case is executed.
  1. True
  1. False
  [//]: # (Answer: 1. True)

1. What reasoning did this lesson give to support verbose test naming (i.e. creating your test case with a name that explains what it does)? (multiple choice)
  1. YOLO
  1. You will not call these test case methods yourself, so verbose naming will not cause use-case issues.
  1. A verbose name will allow you to identify the error from an error log, rather than requiring you to dive into a specific line in a specific file to identify the error.
  1. In the culture of unit testing, all of the cool kids write verbose names.
  1. Unit tests will be read by non-programmers and should be easy to read for those with little or no programming experience.  
  [//]: # (Answer: 2 and 3 - You will not call these test case methods yourself, so verbose naming will not cause use-case issues. - A verbose name will allow you to identify the error from an error log, rather than requiring you to dive into a specific line in a specific file to identify the error.)

1. Each XCTAssert method will allow you to append an optional `message: String` to the end of the assert. (i.e. `XCTAssert(Bool)` also can be written `XCTAssert(Bool, message: String)`)
  1. True
  1. False
  [//]: # (Answer: 1. True)

1. When adding unit tests to an existing project, you must first create a _______, which will ensure separation of test code from production code. The creation of this ______ happens automatically if you select the "Include Unit Tests" checkbox in the Project creation flow.
  1. Folder
  1. Project
  1. Playground
  1. Target
  1. Workspace
  [//]: # (Answer: 3. Target)
