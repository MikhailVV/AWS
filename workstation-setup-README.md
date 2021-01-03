# Mutual of Omaha CDK Getting Started

This document is intended to provide users who want to help develop CDK constructs the very basic needs for their workstation. 
This document assumes that users may have little development experience.

[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)
[![Yarn](https://img.shields.io/badge/Yarn-enabled-brightgreen)](http://yarnpkg.com)

-------------------------------------
<a name="toc"></a>
## Table of contents
1. Workstation Setup
    * [VS Code](#section1a)
    * [IntelliJ](#section1b)
1. Initial Clone, Install, and Build
    * VS Code
        * [Command line](#section2a)
    * IntelliJ
        * [Command line](#section2a)
        * [Console](#section2b)
1. [Developing a "Thing"](#section3)
1. [Issue Pull Request](#section4)

-------------------------------------
[![TOC](https://img.shields.io/badge/Navigate%20To-Table%20of%20Contents-blue)](#toc)
<a name=section1a></a>
## 1a. Workstation Setup (VS Code)
   
Each person will want to download / install several extensions within the IDE
- ESLint
- GitLens
- GitHistory
- npm Intellisense
- Prettier code formatter
- AWS Toolkit for Visual Studio Code
- CloudFormation
- npm egamma
- yaml

These are a good start but not all that developers may choose to use.

### Configure Git

```
$ git config user.name "Your Name"
$ git config user.email "YourEmail@mutualofomaha.com"
```

If you forget to configure git you will get an error later
            Error in git: You can only push your own commits in this repository

[![TOC](https://img.shields.io/badge/Navigate%20To-Table%20of%20Contents-blue)](#toc)
<a name=section1b></a>
## 1b. Workstation Setup (IntelliJ)
   
For construct development, IntelliJ should not need any additional plugins.

[![TOC](https://img.shields.io/badge/Navigate%20To-Table%20of%20Contents-blue)](#toc)
<a name="section2a"></a>
## 2a. Initial Clone, Install, and Build (Command line)

### Clone

Within the IDE, you will want to open the terminal and navigate to the directory / folder
where you want to store your local copy of code.  
```
PS C:\Users\my-user\git-repos\> 
```

Once you have that selected, you will issue a clone to pull from the moo-cdk-constructs repository
```
git clone ssh://git@bitbucket.mutualofomaha.com:7999/aws_cdk/moo-cdk-constructs.git
```

When the clone is complete you will want to change directory to the newly created moo-cdk-constructs 
```
PS C:\Users\req96164\git-repos> cd moo-cdk-constructs   
PS C:\Users\req96164\git-repos\moo-cdk-constructs> 
```

### Install

We are now ready to perform a yarn install
```
yarn install
```

### Build

Finally, you will need to perform a build to finalize the setup
```
yarn build-all
```
You are now ready to do some development.

[![TOC](https://img.shields.io/badge/Navigate%20To-Table%20of%20Contents-blue)](#toc)
<a name="section2b"></a>
## 2b. Initial Clone, Install, and Build (IntelliJ Console)

### Clone
In a web browser, navigate to the [moo-cdk-constructs](https://bitbucket.mutualofomaha.com/projects/AWS_CDK/repos/moo-cdk-constructs/browse) BitBucket project.

Select "Clone" in the left navigation bar and copy the URL.

![Bitbucket clone](img/bitbucket-clone.png)

In IntelliJ, navigate to "File" > "New" > "Project from Version Control..."

![Intellij clone](img/intellij-clone.png)

Paste the URL copied from BitBucket and ensure the "directory" is a location you wish this project to live on your computer.

![Intellij clone paste url](img/intellij-clone-paste-url.png)

Then click "Clone".
Once the clone is complete, navigate to moo-cdk-constructs/package.json.  You'll notice the values in the [devDependencies](https://classic.yarnpkg.com/en/docs/dependency-types/) object are high lighted yellow.

![Package.json missing dependencies](img/packagejson-missing-dependencies.png)

### Install

Next, run a [yarn install](https://classic.yarnpkg.com/en/docs/cli/install/).
Either hover over a high lighted dependency and click "Run yarn install"...

![Run yarn install](img/run-yarn-install.png)

Or

In terminal...
```
yarn install
```

Once that is complete, there should be a newly generated "node_modules" in moo-cdk-constructs directory.

![Node modules](img/node-modules.png)

### Build

Finally, in package.json, above the "devDependencies", you'll find the "scripts" object.  Run the "build-all" command.

![Build all](img/build-all.png)

If there are errors on imports stating "Cannot find module, or it's corresponding type declaration.".
Right click anywhere in the .ts file and select "Fix ESLint problems".  You'll find this to be a recurring step during your construct development, because of the strict ESLint configurations (```.eslintrc.js```). 
You might find it useful to create a [keyboard shortcut](https://www.jetbrains.com/help/idea/configuring-keyboard-and-mouse-shortcuts.html).

You are now ready to do some development.

[![TOC](https://img.shields.io/badge/Navigate%20To-Table%20of%20Contents-blue)](#toc)
<a name="section3"></a>
## 3. Developing a "Thing"

As part of best practices you will want to perform a git pull either at the beginning of the day or 
several times throughout the day.  This will make sure you have brought in any merged changes from the master
branch within bitbucket. 
```
git checkout master
```
```
Switched to branch 'master'
Your branch is up to date with 'origin/master'.
```
```
git pull
```
```
Already up to date.
```

Next you will want to create your branch with putting in your proper type, jira, and service info.
```
git checkout -b <type>/<jira_issue>-<service>
```
You are now in your own branch to create your code that you need.  
Once your development is complete, you will now want to do a yarn test command.  This will perform 
unit tests against your code to make sure nothing has been broken in the surround code.
```
yarn test-all
```
A successful run should look like the following:
```
Test Suites: 19 passed, 19 total
Tests:       211 passed, 211 total
Snapshots:   197 passed, 197 total
Time:        65.023s
Ran all test suites.
```
Optionally, you can also run a yarn functional-test which will validate that each test 
creates the associated AWS stacks.

Next you will want to add the file or files to git
```
git add -A
```

Commit to the branch through commitizen
```
git-cz
```
This will prompt you to provide information related to the change.  
Please see the contributing guide for more information


After doing all of this we will want to move back to master branch, perform a pull, move back 
to our branch, and perform a merge.  
```
git checkout master
git pull
git checkout docx/jiraissue-service
git merge
```
At this point in time you may have merge conflicts.  If so, resolve those conflicts
the perform `git commit` 

Finally, perform another `yarn test`

[![TOC](https://img.shields.io/badge/Navigate%20To-Table%20of%20Contents-blue)](#toc)
<a name="section4"></a>
## 4. Issue Pull Request

Lastly we are ready to generate the pull request.  Issue a `git push` to the origin
You will want to copy the link provided and paste into a browser.

[![TOC](https://img.shields.io/badge/Navigate%20To-Table%20of%20Contents-blue)](#toc)
