# RScout

This is the base for FRC team 3824's scouting app. Each year a fork of this repository is made to create an Android application that is customized for that specific year's competition. Any framework upgrades or additions that would be useful for multiple years should be added to this repository in between seasons.

## Getting Started as a Developer

This guide will help you get started with RScout codebase.

### Getting the tools
You will need a few things before you begin development on the project:

- A Git client
  - [Sourcetree](https://www.sourcetreeapp.com/)
  - [Gitkraken](https://www.gitkraken.com/)
  - [Github Desktop](https://desktop.github.com/)
  - Command Line
    - Git Bash for Windows
    - Terminal on Linux or Mac
- [Android Studio](https://developer.android.com/studio/)

There are a few other optional tools that may be useful:

- A Diff tool
  - [Beyond Compare](https://www.scootersoftware.com/)
  - [Meld](http://meldmerge.org/)

### Understanding Git
If you are familiar with how to fully use git then you may skip to the next section. Git is a version control system, which means that it tracks the history of the changes made to files as people collaborate on a project together. As the code changes and the project evolves, any previous version can be recovered. For more specifics on what Git is and how it works, it is recommended that you read through tutorials such as [this one from Atlassian](https://www.atlassian.com/git/tutorials) or [this one from Github](https://try.github.io/). Once you feel that you are comfortable with Git then move on to the next section.

### Understanding Git Flow
Now that you have an idea of what Git is and why it is useful, it is time to discuss the specific way we use Git this project.

The Gitflow Workflow defines a strict branching model designed around project releases (which for our case is the code for the being of a season on the base repository and for an event for any year specific repository) and clearly separated tasks. This provides a robust framework for managing larger projects. The core idea behind the Feature Branch Workflow is that all feature development should take place in a branch dedicated to that feature instead of the `master` or `dev` branches. This encapsulation makes it easy for multiple developers to work on a particular feature without disturbing the work of other developers on potentially different tasks. It also means that the master branch should __always__ contain a working set of code.

Encapsulating feature development also makes it possible to leverage pull requests, which are a way to initiate discussions around a set of changes or code edits. They give other developers the opportunity to review and give feedback on a feature before it gets merged into the main code base. Also, if you get stuck in the middle of a feature, you can open a pull request asking for suggestions from your colleaguesi/teammates. The point: pull requests make it incredibly easy for your team to comment on each other's work.

#### How it works
##### Dev and Master Branches
Instead of a single `master` branch, this workflow uses two branches to record the history of the project. The `master` branch stores the official release history, and `dev` serves as an integration branch for features. It is also convenient to tag all commits in the `master` branch with a version number/event name.

##### Feature and Bugfix Branches
Each new feature should reside in its own branch, which can be pushed to the central repository for backup/collaboration. `feature` branches use `dev` as their parent branch. *Features should never interact directly with `master`*. When a feature is complete, it gets merged back into `dev` through a pull request.

Bugfix branches work just like features, but they avoid adding in lots of new code or changing functionality of the project. They should be short-lived and small, specific sets of fixes.

##### Pull Requests
Upon finishing a feature a pull request should be created via github. This starts a review process. The code will automatically be checked if it compiles through continuous integration. A merged version of `dev` and the feature branch will also be checked if it compiles. If these both compile then they will need to be reviewed by a human. The human reviewer(s) can request changes and fixes such as logic errors or bad assumptions. Upon completing all the requested changes (or not having any), the feature branch will be merged into `dev` and then pruned.

##### Hot Branches
Maintenances or `hotfix` branches are used to quickly patch releases. `hotfix` branches are based on `master`. *This is the only brnach that should fork off of `master`*. As soon as the fix is complete, it should be merged into both `master` and `dev`, and `master` should be tagged with an updated version number.

Having a dedicated line of development for critical bug fixes lets the team address the issues without interrupting the rest of the workflow.

Keep in mind that a `hotfix` should only be used when the bug is critical or is deemed of high / timely importance. Other normal fixes or low-importance bugs should be managed as `bugfix` or `feature` branches.

For a visualization of the workflow look at [the Git-Flow cheatsheet](https://danielkummer.github.io/git-flow-cheatsheet/).

### Understanding Android

TODO


### Documentation
Comments are one critical part of readability and maintainability. Everyone knows they should comment their code, and so should you. When writing comments, write them as English prose, which means they should use proper capitalization, punctuation, etc. Aim to describe what the code is trying to do and why, not how it does it at a micro level. Remember you and other are going to spend significantly more time reading through the code than actually writing it, so good comments and documentation will speed that part up.

#### Class
Classes are one fundamental part of any good object oriented design. As such, a class definition should have a comment block that explains what the class is used for and how it works. Every non-trivial class is expected to have a Javadoc comment block.

#### Function
All functions should have a comment block. A quick note about what it does and a description of the borderline behavior is all that is necessary here (unless something particularly tricky or insidious is going on). The hope is that people can figure out how to use your interfaces (the inputs and output) without reading the code itself.

Good things to talk about here are what happens when something unexpected happens: does the function return null? Abort? Format your hard disk? Eat your cat?

#### Comment Formatting
Comment are to be formatted as proper Javadoc comments. Include descriptive paragraphs for all public interfaces (public classes, member and non-member functions). Don't just restate the information that can be inferred from the API name. The first sentence (or paragraph beginning with `@brief`) is used as an abstract. Put detailed discussion into separate paragraphs.

To refer to parameter names inside a paragraph, use the `@p` name command.

Wrap non-inline code examples in `@code ... @endcode`. To document a function parameter, start a new paragraph with the `@param` name command. If the parameter is used as an out or an in/out parameter, use the `@param [out] name` or `@param [in,out] name` command, respectively.

To describe a function return value, start a new paragraph with the `@returns` command.

A minimal documentation comment:

```
// Sets the xyzzzy property to @p baz
void setXyzzy(bool baz);
```

A documentation comment that uses all Doxygen features in a preferred way:

```
/**
 * @brief Does foo and bar.
 *
 * Does not do foo the usual way if @p bax is true.
 *
 * Typical usage:
 * @code
 *   foobar(false, "quux", res);
 * @endcode
 *
 * @param bax Whether foo should be done the bax way or the normal way
 * @param quux The kind of foo to do.
 * @param [out] result Filled with bar sequence on foo success.
 *
 * @returns True on success.
 */
 bool fooBar(bool bax, String quux, ArrayList<Integer> result);
```

Functions can include additional comment (not necessarily in Javadoc markup) to explain implementation details as needed.
