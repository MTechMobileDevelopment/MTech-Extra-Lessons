# Git

Git is a version control system for tracking changes in files, and being able to collaborate with others to work on the same files together. This lesson will teach students how to use Git and how it is used in order to collaborate with others. It is critical in a work environment to be competent with Git. It is the primary mode in which you will submit and recieve code to craft into mobile applications.

# Learing Outcomes #

- Be able to create a new repository and commit to it.
- Be able to clone a repository and contribute to it
- Be able to use XCode as a GUI for their repositories.
- Be able to successfully work with a partner to work on a project.

# Vocabulary #

- Repositories
- Commit
- Branches
- Pull
- Push
- Fetch
- Clone
- Fork
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

 ![GitHub Create Repo](https://github.com/MTechMobileDevelopment/MTech-Extra-Lessons/blob/master/Git/Resources/CreateRepo.png)

Typically you keep the repository name to be the same as your project. So for a Journal App your repository could be Journal, or the name of your app.

You get the option to make the repository public or private. A public repository means that anyone on the internet would be able to open and look at your code. A private repository only lets you and your collaborators access the repository. Students can qualify for Github for free! Check out the Student Developer Pack in Additional Resources.

In addition your repository can include a README. When possible you should create a README for all of your repositories. Consider this as an introduction to what your repository is all about. Take a look at how we use README's in this Repository.

The last two options you get are to add a .gitignore and a license. The Git Ignore is way to hide files in your repository. A good example is .DS_Store. That type of file type is a nuisance as it is created whenever you create new files and folders. Adding .DS_Store to your .gitignore is common practice. Licenses are there to protect you. For example, if you had a code base that other people are using. You will want to be acknowleged for your work, an Apache License will require anyone using your code to provide attibution to you.

Apple has recently made a push to incorporate XCode with Github. You will find many helpful tools along the way that integrate XCode with Github. One instance would be if you are on a repository on Github and want to see the project in XCode there is a Open in Xcode button.

![Github- Open in XCode](https://github.com/MTechMobileDevelopment/MTech-Extra-Lessons/blob/master/Git/Resources/OpenInXCode.png)

There are millions of repositories on GitHub. The public repositories you can access and learn from. If you just want to open the project then you can download the ZIP or Open in Xcode as you can see from above. However, you have other options depending on what you want to do.

Your first option would be to Clone. Cloning a Repository gives you a copy of the code that is in the repository. Another option is to Fork. When you fork a repository you create a new repository that is identical to the original, but it is now on your Github account. Remember if you ever decide to use code from other people they probably have a license so you will need to attribute them in your project.

__Link Project to GitHub__

First thing you need to do is to get your Github account linked up to XCode. If you don't have a Github account _now_ is a good time to do so. In XCode in the top bar go to XCode -> Preferences -> Accounts -> + (In the bottom left) -> Choose GitHub -> Sign in.

Now that XCode knows about your GitHub account we can link your created repo on Github to the XCode project. Open XCode and go to the source control tab for your project.

![Source Control Tab](https://github.com/MTechMobileDevelopment/MTech-Extra-Lessons/blob/master/Git/Resources/SourceControlTab.png)

Right click on your the folder with your project name on it. Mid way down in your options you should see:

![AddRemoteRepo](https://github.com/MTechMobileDevelopment/MTech-Extra-Lessons/blob/master/Git/Resources/AddRemoteRepo.png)

Here you have two options. The first option "Create "Project Name" Remote on GitHub..." When you select this option XCode will open a new dialog box for you and you will be able to create a GitHub repository right inside of XCode.

The second option is "Add Existing Remote". Use this option when you already have a repo in GitHub. You will need to get the link from your repository. This link is right about the Open in XCode button on Github. When adding the existing remote the Location it is asking for is the link that you get from GitHub.

Nice work, you now have created your repositories. Next you will learn how to save your code to them and how to work effectively with the repositories.

## Commits and Branches ##

A commit is the bread and butter of Git. Think of committing as saving your code. These saves can be referenced and you can see the progress of the code.

In order to create a commit you need two things. A change in a file and a commit message.

While working on a project you are constantly changing code and writing new code. Anytime a file is created or adjusted it is added into a section called Unstaged Changes. When you are ready to commit you can move the files from Unstaged to Staged. When a file is in Staged Changes it is ready to be commited to the repository.

The second thing you need is a commit message. These messages should be descriptive of what is reflected in the staged changes files. For example if you just made a change in your project to fix a bug. Your commit message could say something like "Keyboard bug fixed"

You know what files you are ready to commit and you have a message so how do you do it? Conveniently Xcode has this built in for you.

![Commit](https://github.com/MTechMobileDevelopment/MTech-Extra-Lessons/blob/master/Git/Resources/Commit.png)

By going to Source Control -> Commit this will open up a new window. In this window you will see your changed files and the ability to add a message. Make sure the right files are checked, write your message and press commit.

__Branches__

By default you are given a branch called "master". Branches are a great resource for you to organize your code and to more easily collaborate with others on your project. Branches are essentially a place to hold commits. A good seperation of commits are with features. You can start a new branch when you start working on a new feature. To create a branch go to the source control navigator in XCode. Right click on the master branch and select Branch from "master" option. You can create a branch from any other branch.

![Create Branch](https://github.com/MTechMobileDevelopment/MTech-Extra-Lessons/blob/master/Git/Resources/CreateBranch.png)

It is good practice to have multiple branches. For an app that is on the App Store it is common to have the master branch have the code that is in live on the App Store. A develop branch is commonly created to seperate what you are working on with what is in production. This enables developers to work in an environment where they do not need to worry about breaking code that is in production. Once code is tested on the develop branch it is merged into the master branch and put into production.

Another benefit to having branches is for collaboration. Later in the lesson you will learn about merge conflicts. When you and another person are working on the same project, you don't want to be changing the same lines of code. To do this it is best to create seperate branches to work on your features.

## How Git interacts with Github ##

Git and Github are not the same. Although they work hand in hand making each other better.

__Git__

So what is Git? Git is a version control system. It tracks versions of your projects and allows you to revert back in time to a previous commit. Git allows you to code away and not worry about breaking something. If something goes awry you know that you have a commit that you can go back to at anytime.

__Github__

What is Github? Github is a place for you to store your repositories. Instead of keeping everything local on your machine, Github gives you a place to store your code online. This allows for other people to see your code, or just a save haven for you to feel comfortable knowing your code is safe.

## Pull, Push, Fetch ##

These are functions to help you have the right code on your computer. They help you interact with your GitHub Repository.

__Pull__ is taking commits that are on the GitHub Repository and bringing them down onto your computer. For example, if Bill made a new commit and Jane wanted to see that commit she would need to _pull_ down the code to see it on her computer.

__Push__ is taking commits that are on your computer and _pushing_ the commits to the GitHub repository. Until you _push_, your code is only stored on your computer. After a _push_ then your commited code is both on your computer and on a GitHub Repository.

__Fetch__ is telling XCode to go look at the repository in GitHub to see if there are any changes. If there are changes XCode will suggest that you _pull_ down the changes.

## Merge Conflicts ##

A __Merge Conflict__ is when you pull down code that someone else has changed and it interferes with code that you have changed. For example, if Bill changed line 24. Jane pulls down Bill's code and Jane had also changed line 24. This results in a Merge Conflict. It is always best to _pull_ before you push. That way any merge conclicts that you may enounter are handled locally.

To solve a _Merge Conflict_ you choose what lines of code you want to keep. Essentially going line by line determining who's code to take. You also have the option to always take Bill's code or always take Jane's.

This becomes a problem in interface builder. There is no good way to solve a merge conflict in interface builder. Avoid working in a storyboard file if someone else is also working in the same file. For this reason use Storyboard References to seperate your storyboards so that different people can work on their own features.

## Conclusion ##

Git is crucial for every developer. Committing often and having meaningful commit messages can really aide your development. Rarely will you work on a project by yourself. Being able to utilize Git to work with others will set you apart as a developer. One of the biggest headaches is working through Merge Conflicts and how to get the right code. Being able to master Git is critical for a successful developer career.


