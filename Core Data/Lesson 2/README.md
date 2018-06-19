# Core Data
# Lesson 2: Start from the Finish Line... Manually #

## Intro ##

In this lesson we will go over how to add Core Data manually to a project for scenarios when you wish to add it to an existing app.
We will also learn how to implement a Relationship in our `.xcDataModeld` file. We will finish off by learning how to subclass `NSManagedObject` manually in code and remove the magic class declaration that Xcode offers.


## Learing Outcomes ##

- Know how to add Core Data to any app
- Know how to setup an NSPersistentContainer
- Know how to create a Relationship on an Entity
- Know how to create a subclass of `NSManagedObject`

## Vocabulary ##

- Core Data Stack: A set of Core Data objects that you must set up before you can use Core Data. (things like what kind of file to use, which NSManagedObjectContext you want to use, etc.)
- NSPersistentContainer: A class that encapsulates setting up the Core Data Stack.
- Delete Rule: The rule for how to handle object related to an object that you delete.
- Data Model File: The `.xcDataModeld` file where you define Entities, Attributes, and Relationships.

## Additional Resources ##

- Apple's docs:
  - [Creating Managed Object Relationships](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreData/HowManagedObjectsarerelated.html)
  - [Initializing the Core Data Stack](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreData/InitializingtheCoreDataStack.html#//apple_ref/doc/uid/TP40001075-CH4-SW1)
  - [Creating and Modifying Custom Managed Objects](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreData/LifeofaManagedObject.html#//apple_ref/doc/uid/TP40001075-CH16-SW1)
- A great Pluralsight video: [Core Data Fundamentals with Swift](https://app.pluralsight.com/library/courses/swift-core-data-fundamentals/table-of-contents)

## Lesson ##

### Core Data Setup ###
When you select the fancy little check box for "Use Core Data", Xcode does two things for you:
1. It adds a Data Model file of type `.xcDataModeld`.
2. It adds a basic setup to your App Delegate for interacting with Core Data.
Implementing these two steps on your own to an existing project is actually quite easy to do -- as we will see in this lesson. All you need to do is add a specific type of file to the project and then add a few lines of code to setup the `NSPersistentContainer` so you can interact with the Data Model file. Then you are caught up to the _use core data check box_ state.

#### .xcDataModeld ####
From [Apple's docs](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreDataVersioning/Articles/vmModelFormat.html) "A managed object model that supports versioning is represented in the filesystem by a .xcdatamodeld document. An .xcdatamodeld document is a file package (see [Document Package](https://developer.apple.com/library/archive/documentation/CoreFoundation/Conceptual/CFBundles/DocumentPackages/DocumentPackages.html#//apple_ref/doc/uid/10000123i-CH106)) that groups versions of the model, each represented by an individual .xcdatamodel file, and an Info.plist file that contains the version information."
Really the only thing you need to do to add Core Data to your app is to add a `.xcDataModeld` file. To do this, you select *File -> New -> File*, and then search for the file type called "Data Model" under the _Core Data_ section. Once you choose a location and file name for your Data Model file, you will see that the `.xcDataModeld` file is added to your project. Once the Data Model file has been added to your project, you can start using Core Data with a little bit of setup code! It's that simple.

Take Away:
`File -> New -> File -> "Data Model"`

#### NSPersistentContainer ####
The second step is to initialize an `NSPersistentContainer`. Doing so is extremely easy. What previously was referred to as "setting up the Core Data Stack", which was a 6 step process and about 20 lines of code, is now initializing the Persistent Container, which can be as short as one line of code, with a few more for error handling.

##### What is NSPersistentContainer? #####
The `NSPersistentContainer` class is the class Apple came out with to encapsulate the Core Data Stack. It contains a property called `viewContext` that is of type `NSManagedObjectContext`. This variable is the means by which you will query the database, add/delete items from the database, and save changes made to the database. Most interactions you make with the Persistent Container at this stage will simply be through the `viewContext` variable.

##### The Core Data Stack #####
The Core Data Stack is a good thing to understand. Before `NSPersistentContainer`, the developer had to manually _configure the Stack_ (as they would say). Manually configuring the stack consisted of:
1. Setting up an instance of `NSManagedObjectModel` by referencing the URL for your Data Model file.
1. Creating an `NSPersistentStoreCoordinator` by passing in the newly created `NSManagedObjectModel` object.
1. Creating a _Store_ file using `FileManager`(the term used for the type of file system you wanted your data saved to. i.e. SQLite file, an XML file, a Binary file, or an In-Memory file type.)
1. Adding your Store file to your StoreCoordinator object.
1. Creating an `NSManagedObjectContext` object
1. Adding the Store Coordinator to your new context object.
1. And finally your stack is configured and you have an `NSManagedObjectContext` object to use.

##### Goodbye Core Data Stack, Hello NSPersistentContainer! #####
As of iOS 10.0, `NSPersistentContainer` is now available and encapsulates the Core Data Stack to make an easy and automated means of setting up Core Data in your app.
To setup the stack using `NSPersistentContainer`, we simply:
1. Create an instance of `NSPersistentContainer`
  - i.e. `let container = NSPersistentContainer(name: "name_for_your_container")`
1. Tell the Persistent Container to load its Persisten Stores
  - i.e. `container.loadPersistentStores(completionHandler: { (storeDescription, error) in .... }`

Note: If there are any issues loading the stores, you will see that error in the completion handler of `.loadPersistentStores`. The most common error you will likely run into is a _migration error_. Migrating data (i.e. changing an attribute/relationship name, adding more attributes/relationships, etc.) must be handled correctly or else it will error out in this call. We will go over Migrating Data in Lesson 4, but **be aware that if you run your app on a simulator/device, any subsequent changes to your Data Model file will result in the need for a migration before you can run your app on that simulator/device again.**
And with that, you have your Core Data Stack configured and ready to use.

#### Relationships ####
We've already addressed Entities and Attributes in the last lesson and we have now implemented them in a simple _Remember App_, but we haven't really gone over Relationships at all yet. We learned in the last lesson that a Relationship is really just a variable that is of a type of one of your other Entities. That is where it gets its name, you create a relationship between two entities. We also learned that there are two types of relationships: _to One_ and _to Many_. We also learned that there is such a thing as an _inverse relationship_ and specifying that the relationship has an inverse relationship, both entities will know about each other. This means that we really have 4 types of relationships:
- _One to One_
  Each entity has a reference to a single instance of the other entity.
- _One to Many_ / _Many to One_
  The first entity has a reference to an array of the second entity, while the second entity only has a reference to one of the first entities. A good example of this would be a Department of People. The department will have a reference to several people, but each person will have a reference to only one department.
  _Many to One_ is simply the inverse of this. Person would have a _Many to One_ relationship with Department.
- _Many to Many_
  Both entities reference an array of the other entity. An example of this might be with a music app and playlists. Each `Playlist` would have an array of subscribers, and each `Subscriber` would have an array of playlists that they subscribe to.

##### Delete Options #####
When you create a relationship between two Entities you will also be presented with the option to select a _Delete Rule_ that determines what happens to the related objects when an instance of this object is deleted. For example, if we have a Department full of Employees, the _Delete Rule_ would determine what happens to the Employees when the Department is deleted. The four options are:
1. _No Action_: Do nothing to the objects related to this object. If I delete a Department with a list of employees, nothing happens to the Employees and they still think that the department exists (dangerous).
1. _Nullify_: Do not delete the other object, but simply remove the relationship between them. If I delete a Department, then each Employee's Department variable would be set to nil.
1. _Cascade_: Delete all objects associated with this relationship. If I delete the department, then it would go through and delete all of the employees related to it.
1. _Deny_: Do not allow the deletion to take place as long as a relationship exists. If I try and delete a Department that still has Employees in it, deny that request. Only when a Department has no employees associated with it will I be able to delete the Department.
The most popular relationships are the _Nullify_ and the _Cascade_. But each rule has its place and which rule you use will depend upon the situation.


### Subclassing NSManagedObject ###
So far we have been using Xcode's magically generated class definitions of our Entities, and it has worked fine. Since writing less code means up-keeping less code and an overall lower cost of implementation/maintenance, we will continue with this approach.
Remember, we can always add functionality to our entities through means of an extension!

#### Custom Subclass ####
If you wish to implement your own, programmer-defined implementation of your entity, doing so is not very difficult. You simply follow these steps:
1. Create a new Swift file and declare a public class exactly after your Entity.
  - Note: To be specific, your class should be named after the `Name` textField under the `Class` section specified in the _Data Model Inspector_ for that entity. It is possible to have separate names for the Entity and the Class, but that will only happen if you manually change this value; Xcode defaults to using the Entity name as the Class name.
    - To open the Data Model Inspector, select an Entity in the Data Model file(`.xcDataModeld` file) and open the right pane. Then select the icon that looks like a square inside a square.
1. Specify that your class is a subclass of `NSManagedObject`.
1. Add variables to your class to mimic the Entity. Again make sure you name them exactly the same as the Entity attributes/relationships and make the type (including whether it is optional or not) the same as is specified by the Entity.
1. Before Each variable declaration, add the descriptor `@NSManaged`. For example: `@NSManaged var middleName: String?`.
1. The GOTCHA: Navigate to the Data Model file and select the Entity you added a class for. In the _Data Model Inspector_ pane under the _Class_ section, change `Codegen` from `Class Definition` to `Manual/None`.
1. The GOTCHA #2: In the drop down directly above the `Codegen` selector you will see a place to specify the `Module`. Tap the drop down arrow on the right, and select `Current Product Module`.
1. Build the app, and watch it work!


## Quiz ##

1. What are the 4 delete rules for a relationship? (mark all that apply)
  1. Conditional
  1. No Action
  1. Transfer
  1. Nullify
  1. Cascade
  1. Deny

1. Relationships can only be one way.
  1. true
  1. false

1. What class encapsulates setting up the Network Stack?
  1. NSManagedObject
  1. NSNetworkStackConfigure
  1. NSPersistentContainer
  1. NSManagedObjectContext

1. What is the file extension of the Data Model file?
  1. .xcDataModeld
  1. .strings
  1. .lproj
  1. .alan
  1. .dataModel

1. In order to use Core Data in a project, you *must* select the check box to "Use Core Data" when creating the project.
  1. true
  1. false
  1. sometimes

1. How do you save data from a NSPersistentContainer object called `container`? (i.e. `var container = NSPersistentContainer(...)`)
  1. You're supposed to save on a different object.
  1. `try container.viewContext.save()`
  1. `try container.save()`
  1. `try container.sendSaveNotification()`
  1. Ask Alan to come write the code for you.

1. You can always add a class extension for each Entity you create in your Data Model file.
  1. true
  1. false

1. The class created by Xcode for your Entity is always named exactly the same as your Entity name.
  1. true
  1. false

1. You cannot programmatically subclass NSManagedObject, but must use the Xcode generated class provided for each Entity.
  1. true
  1. false

1. If you build your app and then change the Data Model file (by changing an entity name or adding attributes to it for instance), you will get a migration error.
  1. true
  1. false


## Project 2: `Cool As` part 1 -- Relationships ##
Create an app that allows you to assign emojis to fellow students to keep track of how much you like them day to day.
  - A TableViewController that has a plus button at the top
    - Plus button takes you to a new screen where you can add the person's name and an emoji to them
    - Tapping on a row takes you to the same add screen with all the data populated but it says "save" in the top right, rather than "add"
      - Removing the person's name from the screen will delete the person when you tap save.
