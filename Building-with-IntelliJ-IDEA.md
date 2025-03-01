<!-- omit in toc -->
# Table of Contents

- [Getting started](#getting-started)
  - [Importing the project](#importing-the-project)
  - [Installing Lombok](#installing-lombok)
  - [Building the project](#building-the-project)
  - [Running the project](#running-the-project)
  - [Conclusion](#conclusion)
- [Troubleshooting](#troubleshooting)
  - [Missing git](#missing-git)
  - [Missing JDK](#missing-jdk)
  - [Client failing to start](#client-failing-to-start)

# Getting started

For working with this project, [IntelliJ IDEA](https://www.jetbrains.com/idea/download) is our recommended IDE and the one used by most collaborators. The free community edition has everything you'll need to start testing and contributing real improvements to the project.

You can build RuneLite locally using [JDK 11](https://adoptium.net/temurin/releases/?version=11). We recommend installing the JDK through IntelliJ and selecting vendor `Eclipse Temurin (AdoptOpenJDK HotSpot)` version `11`. The codebase supports language features up to Java 11.

## Importing the project

You will now need to clone RuneLite repository from git. After launching IntelliJ IDEA for first time, you will see IntelliJ welcome window. click on `Get from VCS`.

![get_from_vcs.png](img%2Fbuilding-with-intellij%2Fget_from_vcs.png)

If you're presented with the editor instead of the welcome screen, click on on  `File > New > Project from Version Control…`

![new_project_from_vcs.png](img%2Fbuilding-with-intellij%2Fnew_project_from_vcs.png)

After clicking on that you will be greeted with prompt. You can either enter the RuneLite repository `https://github.com/runelite/runelite` or your own GitHub fork, if you've created one.
You can also specify a directory where you'd like to save RuneLite and press `Clone`.

![clone_runelite.png](img%2Fbuilding-with-intellij%2Fclone_runelite.png)

After cloning is done you will be presented with a `Trust and open Project ’runelite’?`

Press `Trust Project`.

**Runelite is now cloned**.

We also need to check out to a stable RuneLite version. to do that we first need to get the latest stable tag from https://github.com/runelite/runelite/tags.
At the moment of writing this is ```runelite-parent-1.10.23.2```

![check_runelite_branch.png](img%2Fbuilding-with-intellij%2Fcheck_runelite_branch.png)

Click on the branch manager at the top left corner and then click on `Checkout Tag or Revision...`.

![checkout_tag.png](img%2Fbuilding-with-intellij%2Fcheckout_tag.png)

Enter the tag name and press `OK`

![enter_tag_name.png](img%2Fbuilding-with-intellij%2Fenter_tag_name.png)

**NOTE**: If you plan to make a Pull Request, you must fork the RuneLite repository, and clone from your fork.

## Installing Lombok

When first viewing the project in IntelliJ IDEA you may come across this error:

![missing-lombok-errors](https://i.imgur.com/a1YDonV.png)

This is because you do not have the [Lombok Plugin](https://plugins.jetbrains.com/plugin/6317-lombok-plugin) installed.

Navigate to the `Plugins` tab under the `File > Settings` menu (`IntelliJ IDEA > Preferences` for Mac). Click the `Marketplace` button and search for **Lombok** to find it. Install the plugin and restart IntelliJ IDEA.

![installing_lombok.png](img%2Fbuilding-with-intellij%2Finstalling_lombok.png)

Success! You should no longer be getting ``Cannot resolve symbol`` or ``Cannot resolve method`` errors.


## Configuring the project

We need to make sure that the correct SDK is selected for RuneLite. To do that go to `File > Project Structure…`

![project_structure.png](img%2Fbuilding-with-intellij%2Fproject_structure.png)

Go to `Project Structure > Project Settings > Project` and select Java 11 as the SDK. Then press Ok to close the window.

![select_java.png](img%2Fbuilding-with-intellij%2Fselect_java.png)

If you are having issues with missing JDK see [Troubleshooting](#troubleshooting) section.

## Building the project 

RuneLite is using [Maven](https://maven.apache.org/) as build tool. It is used for dependency management, resource generation, running tests and any other tooling needed to properly build, run and deploy RuneLite.

So, to actually run RuneLite, we first need to invoke Maven.

Locate *Maven* on right-side of the screen. Press on `Reload All Maven Projects`.

![reload_maven.png](img%2Fbuilding-with-intellij%2Freload_maven.png)

Click on `Runelite > Lifecycle` and right click `install` and press `Run Maven Build`:

![run_maven_build.png](img%2Fbuilding-with-intellij%2Frun_maven_build.png)

At this point, it should start the build, which might take a while. Once the process is done, you should see a message to let you know that the build was successful:

![successful_build.png](img%2Fbuilding-with-intellij%2Fsuccessful_build.png)

Now, we need to tell IntelliJ to pick up changes based on Maven build (it should do that automatically, but sometimes it doesn't). `Generate Sources and Update folders for all projects`

![generate_sources.png](img%2Fbuilding-with-intellij%2Fgenerate_sources.png)

## Running the project

Now locate `Project` in sidebar and click that open project view, and expand the tree to `runelite/runelite-client/src/main/java/net/runelite/client`. 
And all you need to do now is right-click the `RuneLite` class and select `run ‘RuneLite.main()’`

![run_runelite.png](img%2Fbuilding-with-intellij%2Frun_runelite.png)

And you are done! RuneLite should open.

If you are having any issues with this step see [Troubleshooting](#troubleshooting) section.

## Conclusion

Success! You can now rebuild RuneLite by pressing the green play button at the top right side of the IDE.

![quick_run_runelite.png](img%2Fbuilding-with-intellij%2Fquick_run_runelite.png)

# Troubleshooting

## Missing git

If you are getting error about `git.exe` (or `git` on linux and mac) missing, you will need to first download and install Git for your OS. Git is version control software and implementation that RuneLite uses to store and track history of it's source code. To download git, just [go here and select your OS version](https://git-scm.com/downloads).

## Missing JDK

If you are getting errors about missing JDK, make sure to install JDK 11 (see start of this page) and then navigate to *File* -> *Project Structure* like this:

![missing-jdk-project-structure](https://i.imgur.com/IzAKzOH.png)

Then press *+* button and *Add JDK* and locate directory of your installed JDK:

![missing-jdk-add](https://i.imgur.com/ZRHDAk3.png)

## Client failing to start

If the client fails to boot or if the applet does not appear, try running the Maven build again with the following command:  
`clean install -DskipTests -U`
![mvn-clean-install](https://github-production-user-asset-6210df.s3.amazonaws.com/41973452/246999260-b33934e5-0969-4455-a5ee-adceeaf55f86.png)

If that also doesn't work, feel free to ask for help in the discord server. Here are few helpful tips:

<!-- omit in toc -->
#### Make sure your branch is up to date with master

To sync your fork simply run

```
git checkout master && git fetch upstream && git rebase upstream/master && git checkout - && git rebase -
```
or update the project from IntelliJ:

![update-project](https://i.imgur.com/69R580v.png) 

<!-- omit in toc -->
#### Make sure IntelliJ is picking up changes from Maven

If you are unsure, run: *Maven Projects* > *Reimport all maven projects* in IntelliJ (or *Ctrl* + *Shift* + *A* and type *Reimport all maven project*).

Happy development!

<!-- omit in toc -->
#### JDKs 16+

You have to add the following extra VM arguments in order to use these java versions:

<!-- omit in toc -->
##### Windows/Linux
```
--add-opens=java.desktop/sun.awt=ALL-UNNAMED
```

<!-- omit in toc -->
##### Mac
```
--add-opens=java.desktop/com.apple.eawt=ALL-UNNAMED --add-opens=java.desktop/sun.awt=ALL-UNNAMED
```
