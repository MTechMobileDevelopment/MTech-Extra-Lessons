# Git

Git is a version control system for tracking changes in files, and being able to collaborate with others to work on the same files together. This lesson will teach students how to use Git and how it is used in order to collaborate with others. It is critical in a work environment to be competent with Git. It is the primary mode in which you will submit and recieve code to craft into mobile applications.

# Learing Outcomes #

Bulleted list of things the student can expect to learn from the lesson
- Be able to create a new repository and commit to it.
- Be able to clone a repository and contribute to it
- Be able to use XCode as a GUI for their repositories.
- Be able to successfully work with a partner to work on a project.

# Vocabulary #

- Repositories
- GUI
- Commit
- Branches
- Pull
- Push
- Fetch
- Clone
- Fork
- Stash
- Revert
- Pull Requests
- Merge Conflicts
- Git
- GitHub
- Version Control

# Additional Resources #

[Github's Guide to Create a new repository](https://guides.github.com/activities/hello-world/)

[WWDC - Github and the New Source Controler Workflows in XCode](https://developer.apple.com/videos/play/wwdc2017/405/)

[Atlassian Gudie on Git](https://www.atlassian.com/git/tutorials/what-is-git)

[Github Student Developer Pack](https://education.github.com/pack)

[Git vs. Github](https://www.codefellows.org/blog/git-and-github-what-s-the-difference/)

[Git Source Control with XCode 9](https://www.raywenderlich.com/153084/use-git-source-control-xcode-9)

# Lesson #

## Repositories ##

A repository is the home for your code. Changes that you make in code will be reflected in your repository for that code. All folders and files in your projects can be stored in a repository. There are many services online that you can utilitize to save your repositories. For this class, and for many people in the iOS community Github will be our service that we use. So, how do we start with a repository on GitHub? All you need to start is a name, but you also will have many options to include which we will cover.

 ![GitHub Create Repo](https://github.com/MTechMobileDevelopment/MTech-Extra-Lessons/blob/GitLesson/Git/Resources/CreateRepo.png)

Typically you keep the repository name to be the same as your project. So for a Journal App your repository could be Journal, or the name of your app.

You get the option to make the repository public or private. With a free account you will only be able to create a public repositories. A public repository means that anyone on the internet would be able to open and look at your code. A private repository only lets you and your collaborators access the repository. Students can qualify for Github for free! Check out the Student Developer Pack in Additional Resources.

In addition your repository can include a README. When possible you should create a README for all of your repositories. Consider this as an introduction to what your repository is all about. Take a look at how we use README's in this Repository.

The last two options you get are to add a .gitignore and a license. The Git Ignore is way to hide files in your repository. A good example is .DS_Store. That type of file type is a nuisance as it is created whenever you create new files and folders. Adding .DS_Store to your .gitignore is common practice. Licenses are there to protect you. For example, if you had a code base that other people are using. You will want to be acknowleged for your work and so a Apache License will require anyone using your code to provide attibution to you.

Apple has recently made a push to incorporate XCode with Github. You will find many helpful tools along the way that integrate XCode with Github. One instance would be if you are on a repository on Github and want to see the project in XCode there is a Open in Xcode button.

![Github- Open in XCode](https://github.com/MTechMobileDevelopment/MTech-Extra-Lessons/blob/GitLesson/Git/Resources/OpenInXCode.png)

There are millions of repositories on GitHub. The public repositories you can access and learn from. If you just want to open the project then you can download the ZIP or Open in Xcode as you can see from above. However, you have other options depending on what you want to do.

Your first option would be to Clone. Cloning a Repository gives you a copy of the code that is in the repository. Another option is to Fork. When you fork a Repository then you create a new repository that is identical to the original, but it is now on your Github account. Remember if you ever decide to use code from other people they probably have a license so you will need to attribute them in your project.

## Commits and Branches ##

A commit is the bread and butter of Git. Think of committing as saving your code. These saves can be references and you can see the progress of the code.

In order to create a commit you need two things. A change in a file and a commit message.

First thing is you need to change a file. Working on a project you are constantly changing code and writing new code. Anytime a file is created or adjusted it is added into an Unstages Change. When you are ready to commit you can move the files from Unstaged to Staged. When a file is in Staged Changes it is ready to be commited to the repository.

The second thing you need is a commit message. These messages should be descriptive of what is reflected in the staged changes files. For example if you just made a change in your project to fix a bug. Your commit message could say something like
"Keyboard bug fixed"

You know what files you are ready to commit and you have a message so how do you do it? Conveniently Xcode has this built in for you.

![Commit](https://github.com/MTechMobileDevelopment/MTech-Extra-Lessons/blob/GitLesson/Git/Resources/Commit.png)

By going to Source Control -> Commit this will open up a new window. In this window you will see your changed files and the ability to add a message. Make sure the right files are checked, write your message and press commit.

By default you are given a branch called "master". Branches are a great resource for you to organize your code and to more easily collaborate with others on your project. Branches are essentially a place to hold commits. A good seperation of commits are with features. You can start a new branch when you start working on a new feature. To create a branch go to the source control navigator in XCode. Right click on the master branch and select Branch from "master" option. You can create a branch from any other branch.

![Create Branch](https://github.com/MTechMobileDevelopment/MTech-Extra-Lessons/blob/GitLesson/Git/Resources/CreateBranch.png)

It is good practice to have multiple branches. For an app that is on the App Store it is common to have the master branch have the code that is in development. A develop branch is commonly created to seperate what you are working on with what is in production. This enables developers to work in an environment where they do not need to worry about breaking code that is in production. Once code is tested on the develop branch it is merged into the master branch and put into production.

Another benefit to having branches is for collaboration. Later in the lesson you will learn about merge conflicts. When you and another person are working on the same project, you don't want to be changing the same lines of code. To do this it is best to create seperate branches to work on.

## Pull, Push, Fetch ##

- What is a pull
- A push?
- A Fetch?
- How often should someone do those things

## How Git interacts with Github ##

- The difference between Git and Github

## Pull Requests ##

- What is a pull request
- How to create a pull request
- How to review said pull request.

## Merge Conflicts ##

- What is a merge conflict
- What tools to use in order to solve the conflicts
- Power of developing with others.

## Conclusion ##

- Importance of Git. How it can really make you a better developer and save you time.

# Assignment #

20-30 minute assignment for them to work on during class. Wraps up the lesson and has the student implement what they learned. An assignment that brings in all of the learning outcomes for the lesson.

# Quiz #

10 questions to cover the unit. Easy. We want the students to be able to get 100% on the quiz with ease.
