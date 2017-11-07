# Unit Tests

Meant to be taught in two days. Just teach the basics of a unit tests. Have two assignments that should take 20-30min meant to be done in class.

Lessons:
- Unit tests
- A Plug for Automated Testing

Testing Concepts:
    - TDD
    - Dependency Injection
        - Protocol Oriented Programming

# Lesson Outline #

## Intro ##

"Unit testing is a software development process in which the smallest testable parts of an application, called units, are individually and independently scrutinized for proper operation."
Unit Testing is the vital process of writing code to validate or test your production code. It may seem trivial or "not worth it", but having Unit Tests in your code allow a confidence and quality of code that is not otherwise possible.
Unit Tests are usually written as methods, which test a single _unit_ of the production code. A unit could be a method, a specific use case of a method, or even a class. When unit tests are written, it gives you a quick way to test your code. This enables confidence that any change you make to your code in the future will not break the existing/expected functionality or introduce new bugs.
When written using the process of Test Driven Development (TDD), which we will cover in the next lesson, you will usually have around two times the amount of testing code as you will production code.

# Learing Outcomes #

- What is a Unit Test?
- How do I add unit tests to my project?
- How do I create a good unit test?
- What should I test in my project?
- When should I add tests to my project?

# Vocabulary #

- Unit Test
- Automated Test Suite
-

# Additional Resources #

[A great little document that goes over what Unit Tests are and why to use them.](http://www.extremeprogramming.org/rules/unittests.html)
[Apple's documentation on adding and using Unit Tests. Not very nice to read, but a great resource!](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/testing_with_xcode/chapters/04-writing_tests.html)

# Lesson #

## Unit Test ##

Simply put, a unit test is a function containing at least one assertion. The purpose of a unit test is to exercise your production code and assert expected functionality. A "unit" is usually a function, but is technically defined as _"the smallest testable parts of an application."_ (Unit Testing definition)[http://softwaretestingfundamentals.com/unit-testing/] With proper unit testing, there will be a _one to many_ relationship between class methods and unit tests (many tests per method to assert specific allowed and unallowed behavior).
Unit tests will follow  the __AAA__ pattern:
1. __Arrange__: Prepare the state/input
2. __Act__: Call the method to be tested
3. __Assert__: Verify the correct output/state

For example, lets use the simple method `increment` as the production code we wish to test. We expect this method to return our input plus one.
```
func increment(_ value: Int) -> Int { ... }
```

We begin by __arranging__ the input:
`let inputNumber = 3`
Then we __act__ by calling the production code we wish to test:
`let result = increment(inputNumber)`
Finally, we __assert__ the expected functionality/result:
```
let expectedResult = 4
AssertEqual(result, expectedResult)
```
The result is a proper unit test, which verifies an expected behavior of production code:
```
func testIncrementAddsOne() {
    let inputNumber = 3
    let result = increment(inputNumber)
    let expectedResult = 4
    AssertEqual(result, expectedResult)
}
```

_*Often times the arrange step is the most difficult as the units (or functions) you wish to test are not merely floating functions (as the above example), but they usually live on a class, which must be initialized and setup before executing the desired unit. Structuring your code to be testable through Dependency Injection/Procedural Oriented Programming (see next lesson) is often essential to enable proper testing of class units._

## XCTest ##

 Unit tests are usually based upon a framework of some kind that allows you to run your complete suite (or collection) of tests and view which tests passed and which failed. This allows you to build up a testing suite as you add more and more unit tests to your project.
 
 
 
 Unit tests live inside of a class that inherits from the class `XCTestCase`. Unit tests are written like any normal method (usually without any parameters) but must begin with the word "test".
 For example:
 ```class CounterTests: XCTestCase {
     func testIncrementMethod_AddsOneWhenCalled() { ... }\
 }
```



## Assignment ##

20-30 minute assignment for them to work on during class. Wraps up the lesson and has the student implement what they learned. An assignment that brings in all of the learning outcomes for the lesson.

## Quiz ##

10 questions to cover the unit. Easy. We want the students to be able to get 100% on the quiz with ease.

## Project ##

This project is meant to be done solely in class. A list of instructions with no solution code. Students should struggle to work through these. Help from their fellow students and the teacher should be necessary in order to finish the project. A project can take a whole week. A week of lesson then the next week project is fine.





QUOTES:
"The biggest resistance to dedicating this amount of time to unit tests is a fast approaching deadline. But during the life of a project an automated test can save you a hundred times the cost to create it by finding and guarding against bugs."
"When you create unit tests you guard your functionality from being accidentally harmed. "
"Unit tests enable refactoring as well. After each small change the unit tests can verify that a change in structure did not introduce a change in functionality."
"Unit Tests provide a safety net of regression tests and validation tests so that you can refactor and integrate effectively."
-  http://www.extremeprogramming.org/rules/unittests.html

"It’s as close to a religious matter as programmers get, aside from the tabs-versus-spaces debate."
- http://nshipster.com/unit-testing/ (Great website!)

"Unit testing is a software development process in which the smallest testable parts of an application, called units, are individually and independently scrutinized for proper operation."
- http://searchsoftwarequality.techtarget.com/definition/unit-testing
