Lesson 1: Dive in -- Start from the finish line -- shortest path from a to c

# Core Data

# Lesson Outline #

## Intro ##

In this lesson we will create an app with Core Data and get it functioning.
We will not go in depth about the different aspects of Core Data yet, but will focus on
the bigger picture and how it works overall. In the next lessons we will dive in deeper on each
aspect of Core Data and build more complex apps, utilizing the abilities and features learned.


## Learning Outcomes ##
- What is Core Data?
- Entities
  - What is an Entity?
  - What is an Attribute?
  - What is a relationship? (overview, more to come later)
  - How do I instantiate an instance of my entity?
  - How do I Update and Delete my entity?
  - How do I save my changes to Core Data?


## Vocabulary ##

- Entity: most easily understood as an alternate name for a class.
- Attribute: A basic variable, only allowed to be of basic types like String and Int
- Relationship: A more complex type of variable that reference another Entity rather than Strings and Ints
- NSManagedObject: The basic building block of core data. Every class that is savable via Core Data will be a subclass of `NSManagedObject`.
- NSManagedObjectContext: A _context_ to save `NSManagedObject`s into. Kind of like a Word Document or a note pad. It is a place to store data.
- NSFetchRequest: A query type object that is used to retrieve data from an `NSManagedObjectContext`.
- NSPredicate: A means of clarifying and refining the NSFetchRequest to retrieve data that matches a specified condition.
- NSSortDescriptor: A means of sorting the results of an NSFetchRequest.


## Additional Resources ##

- There is a great Pluralsight course on Core Data that covers everything we cover.
  If you find the in-class lessons are not enough, feel free to watch it: [Core Data Fundamentals with Swift](https://app.pluralsight.com/library/courses/swift-core-data-fundamentals/table-of-contents)
- Of course [Apple's Programming Guide to Core Data](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreData/) is also a great reference.


## Lesson ##

Go in depth on the subject. Show code examples. Remember that teachers will be covering this material. Make it easy to follow along. Easy for the teacher to pick it up and go.

As well it will be good for the students to be able to come back to the lesson and understand without a teacher directing them.

### What is Core Data? ###
Core Data is a data persistence framework provided by and maintained by Apple. Over the last several years Apple has improved this framework and made it very easy to jump in and start using it with little or no understanding of the underlying logics -- as we will experience in this lesson!
According to Apple's Core Data [Programming Guide](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreData/), "Core Data typically decreases by 50 to 70 percent the amount of code you write to support the model layer." Using Apple provided code to make your project work means you will have less code to maintain and less code where you can accidentally introduce bugs, which equates to less money 💸 and happier product owners.
Core Data not only allows you to save data to disk, but also has a lot of features around data modeling itself. Core Data has the following useful features baked in to its framework:
  - The ability to Undo/Redo changes made
  - The ability to validate data that is set to an object. For instance, you can specify that an Integer should never be below 0 or above 100.
  - Schema (i.e. Model layout) migration tools that make migrating your database mappings (i.e. a variable name change or adding/removing a variable) easy and nearly automatic.
  - Support to easily and effectively hook up your data to a UITableView: including support for sections, rows, and adding, removing, deleting, and moving data/rows around.
  - Ability to save your data to an SQLite database file (default), an XML file, or a Binary file.
  - And much, much more.

### How does Core Data Work? ###
It is probably best to think of Core Data as a database managing tool. Saving data using Core Data is straightforward and simple -- a simple call to `save()`. Loading data however, exposes some of the inner workings of Core Data. While it is not necessarily complex, it has a database style to it that may take some getting used to. In SQLite you grab data from the database by doing a SQL query like this:
```
SELECT colum1, colum2, ...
FROM table_name
WHERE ValueName=`someValue` AND OtherValueName=42
ORDER BY column1;

```
Core Data does not require you to memorize SLQ syntax or to write SQL queries, but it does use the same method of querying the database for data. Luckily, Core Data provides a fetch request object (`NSFetchRequest`) that makes all of this very easy, but the concept of specify what you want in a query/fetchRequest may take some time to wrap your head around.

Now that we have a general understanding of what Core Data is and how it works, we can dive into some of the specifics.

### The Specifics ###
Core Data defines a few new terms that will likely be unfamiliar to you. But don't worry. While the terminology may be hard for you to remember at first, the concepts are nearly identical to concepts you will be very familiar with by now. Specifically, we will go over the following terms in this lesson: Entity, Attribute, Relationship, Fetch Request. With these terms under your belt, you will be properly prepared to begin implementing Core Data with just a few technical directions (like checking a box, or adding a file, etc.).

#### Entity ####
An entity is most easily understood as an alternate name for a class. In Core Data we create Entities and add Attributes(basic variables) and Relationships(references to other Entities) to the entity.
Instead of starting out by adding a file and defining a `class Foo {...}` in code, we start out in an `.xdatamodeld` file where we press a button to add an Entity named `Foo`.
While technically the Entity name can be unique from the associated class name, each entity will still represent only one class type and so it is safe to think of an Entity as basically being a Class.

#### Attribute ####
An attribute is essentially another name for "variable", but with one caveat -- attributes only refer to the variables that are a base type. In other words, attributes can only reference types that are: `Integer 16`, `Integer 32`, `Integer 64`, `Decimal`, `Float`, `String`, `Boolean`, `Date`, `Binary Data`, `UUID`, `URI`, `Transformable`, and `Undefined`. If you don't know what the last few types are, don't worry; you likely won't use them during these introductory courses on Core Data. They are there for specific instances, and when you reach those instances they will make sense.

#### Relationship ####
Relationship refers to variables that reference another Entity. In Core Data, instead of saying my class `PetOwner` has a variable named `dog` that is of type `Dog`, we say my class `PetOwner` has a relationship to the class `Dog`, and then we define if that relationship is a `to-One` or a `to-Many` relationship. In other words, does the variable `dog` refer to a single `Dog` or to an array `[Dog]`? When you define the type of relationship, you also can specify if there is an _inverse_ relationship. In other words, does `Dog` have a reference to his owner? Again, you will specify if that inverse relationship is a to-One or a to-Many relationship.
In Swift we often discourage this concept of _inverse relationships_ because of a memory issue called a _retain cycle_. Because of this, you may have an inherent distrust or dislike for the `inverse relationship` concept. While the issue of retain cycles is real and this inherent distrust is good, the issue of retain cycles does not apply to the database so you have nothing to distrust about inverse relationships.

#### NSManagedObject ####
`NSManagedObject` is the basic building block of Core Data. Every class that is savable via Core Data will be a subclass of `NSManagedObject`. When you create an Entity in the `.xdatamodeld` file, Xcode is actually compiling a class definition of the Entity and defining the class as a subclass of `NSManagedObject` in the background hidden from your view (i.e. `class User: NSManagedObject {...}`).

#### NSManagedObjectContext ####
The `NSManagedObjectContext` is kind of exactly how it sounds: it is a specific instantiated context that can hold or store `NSManagedObject`s. While you can have multiple NSManagedObjectContext instances in your app, for our purposes we will only ever have one. You can think of an NSManagedObjectContext as a kind of Word document. On your computer you can have multiple word documents, but when you save data to one document it does not save that data to all of your other word documents. Each NSManagedObjectContext object is like a new word document that will hold your data saved via Core Data.

#### Fetch Request ####
Because all of our data is stored in an `NSManagedObjectContext` object, we must query that context object for the data we want. The way we do that is through the `NSManagedObjectContext.fetch(<NSFetchRequest>)` method. You start by creating a fetch request, which turns out to be very simple.
If I wanted to fetch all objects that are of a type `User`, I would write a fetch request that looked like this:
```
var fetchUsers = NSFetchRequest<User>(entityName: "User")
```
That's it. Done. Then we pass that fetch request into the `context.fetch()` method, and Core Data will return all the `User` objects we have saved into Core Data. _All_ the user objects... At this point you may be recognizing that this approach is not very sustainable as your database expands, and you're right! But Core Data has provided a way to add clarifications onto your fetchRequest. While we won't be using any of these variable in this current lesson, it is good to be aware of their existence.
Specifically, `NSFetchRequest` has the following main optional variables that you can set after initializing a fetch request object:
  - `predicate: NSPredicate`: The predicate is how we specify specifics about what data we want returned. For example, `"firstName=\'Bob\'"` will return all instances of the specified type where the first name equals "Bob". We will address predicates in more detail at a later time, but just know it exists for now.
  - `sortDescriptors: [NSSortDescriptor]`: Sort Descriptors allow you to sort the data returned. The order of the array will be the order in which the sorting will happen. For example: `[lastNameSortDescriptor, firstNameSortDescriptor]` will sort the returning Users by last name and then by first name. In other words, if two people have the same last name, then they will be sorted by their first name.
  - `fetchLimit`: The max number of items to return.

#### Fetched Properties ####
We won't be using Fetched Properties, but you will see them as you add Attributes and Relationships to Entities and will likely wonder what they are. A fetched property is exactly what it sounds like, a property on the Entity that is computed or populated by executing a fetch when the item is retrieved from the database. They most closely mirror the _computed variable_ on a class and you can think of them as a computed property where the computation is merely a specified fetch. For example you may have a fetched property on a `User` class called `alterEgos` that fetches all User objects in the database with the same username.

### Instantiating an Entity Instance ###
Sadly, Core Data does not have a _swifty_ way to instantiate an object of your Entity. That being said, it is not a difficult task to perform, but it will take some getting used to as it is not intuitive in the Swift environment.
The only way to initialize a new Entity is to insert that entity into our `NSManagedObjectContext` object. So we start by inserting a new `NSManagedObject` (of a type specified by the name of that type, i.e. "User") into our `NSManagedObjectContext` object. Once it is inserted, we then have a blank object of the specified type that we can populate with data (just like we do in the `init()` method of a class). After all of this, it is best to tell the context to save the changes made to it so we don't lose anything if the app crashes.
Here is what that ends up looking like for our `User` example:
```
let user = NSEntityDescription.insertNewObject(forEntityName: "User", into: myNSManagedObjectContext) as! User // We have to cast it as a User because the method will simply return an `NSManagedObject` (the superclass of our `User` class).

// Populate the data on our new object
user.name = "Bob Builder"
user.username = "canHeFixIt_yesHeCan"
user.age = "26"

...

// save the context for good measure.
myNSManagedObjectContext.save()
```
After that, we have a new user object saved in core data and ready for use. Speaking of use, lets go ahead and use all of the knowledge we just learned by making a new app! 😎

### Deleting an Entity Instance ###
Unlike creating an Entity Instance, deleting one is much more straightforward. To delete an entity instance, you simply call the `NSManagedObjectContext.delete(:)` method and pass in the object you wish to delete.
For example, with the user variable created above, we would delete it like so:
```
myNSManagedObjectContext.delete(user)
myNSManagedObjectContext.save()
```


## Project: Remember List ##

### Getting Started ###
- Create a new app and check the "Use Core Data" box above the "Include Unit Tests" check box on the app naming page.
- Take a quick look at your App Delegate. Notice that you have a variable called `persistentContainer`. We will go over `NSPersistentContainer`s in the next lesson, but you can see from the `saveContext()` method just below this variable that your `NSManagedObjectContext` variable is inside the `persistentContainer`. Whenever you need to use the `NSManagedObjectContext` object, you will use this `persistentContainer.viewContext`.
  - Getting the `persistentContainer` variable outside of the AppDelegate file may be confusing to you. You can always access your AppDelegate by referencing `UIApplication.shared.delegate`. But be careful because this variable (`.delegate`) is of type `UIApplicationDelegate`, not the custom subclass defined in your app, `AppDelegate`. You will only be able to access the `persistentContainer` on an object of type `AppDelegate`... With this information, can you figure out how?

### Requirements ###
- A TableViewController with an Add button in the top right.
  - When you tap the Add button, present the detail view which is just a textField in a ViewController with a "save" button below the textField.
    - When they tap the "save" button create a new object and save it into your NSManagedObjectContext and dismiss the ViewController.
  - When you tap a row in the tableView, present the detail ViewController, populate the TextField with the selected item's text, and make the button say "update"
    - 🔷🔷 disable the button if there are no changes made to the text.
    - 🔷🔷 If you delete all text from the TextField, then the Save button should say "delete" for clarity.
- In ViewDidLoad, fetch all of the items from Core Data and save them into an array that will be used to populate the TableView
  - Be sure to also do this each time the view appears so your data stays up to date after adding a new item!


## Quiz ##

What is an Entity mostly resemble?
  1. A class
  1. A variable
  1. A function
  1. A ghost

What does an Attribute mostly resemble?
  1. A class
  1. A Dark hair gene
  1. A variable
  1. A function

What does a Relationship mostly resemble?
  1. A Mother
  1. A class
  1. A variable
  1. A function

How do you get data from the database?
  1. You ask nicely
  1. Using an NSFetchRequest
  1. Using a SortDescriptor
  1. Using a SQL query

How do you create a new instance of an Entity?
  1. By using the `.init()` method on the class, just like any other class
  1. By inserting it into the Database with the `NSEntityDescription.insertNewObject(forEntityName:_into:_)` method
  1. By creating an NSFetchRequest
  1. By asking Alan for help.

Every class that is savable via Core Data will be a subclass of `NSManagedObject`.
  1. True
  1. False

What are the types of Relationships you can define between two Entities? (mark all that apply)
  1. familial
  1. to-one
  1. to-zero
  1. to-many
  1. to-few

How do you save your changes to Core Data?
  1. You don't need to, it happens automatically.
  1. By calling the `.save()` method on your `NSManagedObjectContext` object.
  1. By calling `.save()` on the Entity object you wish to save.
  1. By asking Alan to save the changes for you.

Deleting an object is as simple as calling `myNSManagedObjectContext.delete(myObject)`.
  1. True
  1. False

`NSFetchRequest`s are not customizable. I can only fetch _all_ of the items saved of a specific type.
  1. True
  1. False
