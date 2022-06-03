# ForgeGradle Multiproject Template

This repository provides a template for multiproject development environments using ForgeGradle.

## Project structure
This template builds upon the [runenv template](https://github.com/amadornes/fg-multiproject-runenv) repo to provide the
binding logic that makes the multiproject environment work.

The built-in `examplelib` and `examplemod` projects are standard Forge MDK projects, heavily trimmed down for the sake
of simplicity, and are unaware that they exist within a multiproject environment.

## Setup
To set up a multiproject development environment, just clone this repository.  
Optionally, you may delete the `.git` directory and initialize your own git repo in its place.  
It is advised to keep the *runenv template* as a submodule, which allows you to easily pull new versions down the line.

## Customization
The most basic form of customization comes in the form of adding new projects to `settings.gradle`.  
Just add new `include 'YourProjectName'` lines in the same place you find the predefined ones.

If you are authoring several mods that depend on each other, but you still want to be able to compile them on their own,
this template also allows it.  
For example, if one of your projects depends on `fg.deobf("com.example:examplelib:1.2.3")`, you can define a
substitution in the root level buildscript: `substitute module("com.example:examplelib") using project(":examplelib")`.  
This will make it so whatever depended on that artifact will now depend on the project in your dev environment instead.  
Make sure to also define an exclusion for the same module in the `if` statement above it. That will ensure that
ForgeGradle doesn't try to unnecessarily resolve the artifact.

Further customization can be done by either modifying the *runenv template*, or the `project('runenv')` closure in the
root level buildscript.

## Generating runs
The run configurations for your multiproject environment should point to the *runenv template*.  
You must run that project's `gen<IDE>Runs` task and use its classpath at runtime for all the projects to load.

For datagen, you may still use each project's individual runs.

## Known issues
Please check the [runenv template](https://github.com/amadornes/fg-multiproject-runenv) repository, as that will contain
the latest information regarding compatibility.

## Contributions
Pull requests adding extended feature support and bugfixes are welcome.  
Please keep them simple if possible.
