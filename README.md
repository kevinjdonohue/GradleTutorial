# GradleTutorial
A repository for notes and example script(s) for the the basic tutorial on the Gradle website.

## Installation

The tutorial actually assumes you've already downloaded and installed Gradle -- so the first step for me was to grab Gradle.

### For Unix, MacOS, etc.  

Homebrew is your friend.  Checkout this article for hints on using Homebrew to install Gradle.

[Installing Gradle on MacOS](https://stackoverflow.com/questions/28928106/install-gradle-on-mac-os-x)

### For Windows  

Either [Chocolatey](https://chocolatey.org/), [Scoop](http://scoop.sh/) or just download the latest from the [Gradle website](https://gradle.org/releases/).

## Tutorial

The files in this repository were all created while following this tutorial on the offical Gradle website:

[Creating New Gradle Builds](https://guides.gradle.org/creating-new-gradle-builds/)

### Steps

#### Step 1:  Create a folder and build file

1. Create a folder for the tutorial, call it something like `/gradle-demo/`.

2. Inside your new folder create a Gradle build file - `build.gradle`.

#### Step 2:  Checkout the Tasks command

1. Run the `gradle tasks` command to see the default tasks available from Gradle.

#### Step 3:  Generate a Gradle Wrapper

1. Run the `gradle wrapper` command to automatically generate a Gradle wrapper file.

This is an interesting step because you are making it so that a future user/client of your project won't have to download and setup Gradle - they can simply use the generated Gradle wrapper (`gradlew` or `gradlew.bat` on Windows) on their platform of choice -- and Gradle will automagically be downloaded and configured.  See the tutorial for more details on what folders and files are generated with this command.

#### Step 4:  Checkout the Properties command

1. Run the `gradlew properties` command to see the properties that are avaiable from Gradle.

2. Add some properties to your `build.gradle` file and re-run the `gradle properties` to see that your added properties are used -- in fact the description is used at the top of the output!

#### Step 5:  Create a Grade core task

1. Create a folder inside your tutorial folder called `/src/`.

2. Create a file inside your `src` folder called something like `myfile.txt` - add some text to it just for fun -- like "Hello, World!".

3. Now, the fun part, you are going to create a `task` inside your build.gradle file that'll make use of the folder and file you just created -- to demonstrate some of the built in capabilities of Gradle (Core).

```groovy
task copy(type: Copy) {
    from 'src'
    into 'dest'
}
```

4. Now, re-run Step 2 to list out all of the Gradle tasks, including your newly created copy task.

5. Finally, execute your copy task by running `./gradlew copy` (or `gradlew copy` or Windows)

#### Step 6:  Create a Gradle core task using a plugins

1. At the top of your `build.gradle` you'll need to add a reference to a plugins

```groovy
plugins {
    id 'base'
}
```

2. Then, below your first task, create a new one that makes use of the plugin your just added.

```groovy
task zip(type: Zip) {
    from 'src'
}
```

3. Now, re-run Step 2 again so you can confirm that you see your new task.

4. Finally, run your task by running `./gradlew zip` and note that in the build/distributions/ folder there is a zip file named after your project folder.

5. Now, just so you can see some other capabilities of Gradle, you can use one of the built in tasks, called `Clean` to clean up.  `./gradlew clean`  Note, it'll remove the build folder that you just generate the zip file into.

#### Step 7:  Create a Gradle ad hoc task

1. This time you're just going to create a simple ad hoc task in the same `build.gradle` file.

```groovy
task hello {
    doLast {
        println 'Hello, World!'
    }
}
```

2. Now, to wrap up, you can run your newly created task by running `./gradlew hello`.

This is a very simple introduction to an interesting concept -- writing custom Gradle tasks.
