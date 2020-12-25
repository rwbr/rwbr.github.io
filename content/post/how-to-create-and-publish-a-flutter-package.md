---
title: "How to Create and Publish a Flutter Package"
date: 2020-12-25T15:43:45+01:00
tags: [flutter, programming]
draft: true
---
You can extend the functionality of your project by adding Flutter packages as a dependency. These packages can be found on [pub.dev](https://pub.dev). There you find packages for any purpose. If you want to develop a functionality and share it with the community, this article will show you how it works.

 <!--more-->

![pub.dev](/img/pub_dev.png)

## Create a new project

To create a new Flutter package you need to generate a new project. Creating a project for a package has a slightly different syntax. Navigate to your projects folder and type:

```
flutter create --template=package my_new_package
```

(Of course you exchage the term *my_new_package* with a more sophisticated name).

This creates the following output in the terminal:

```
❯ flutter create --template=package my_new_package                                                           [20:53:57]
Creating project my_new_package...
  my_new_package/LICENSE (created)
  my_new_package/test/my_new_package_test.dart (created)
  my_new_package/my_new_package.iml (created)
  my_new_package/.gitignore (created)
  my_new_package/.metadata (created)
  my_new_package/pubspec.yaml (created)
  my_new_package/README.md (created)
  my_new_package/lib/my_new_package.dart (created)
  my_new_package/.idea/libraries/Dart_SDK.xml (created)
  my_new_package/.idea/modules.xml (created)
  my_new_package/.idea/workspace.xml (created)
  my_new_package/CHANGELOG.md (created)
Running "flutter pub get" in my_new_package...                      1,1s
Wrote 12 files.

All done!
Your package code is in my_new_package/lib/my_new_package.dart
```

Take a look at the created folder structure. You probably notice, that it shows some difefrences to a normal Flutter project:

![Finder window](/img/finder_window_package.png)

* Files **CHANGELOG.md** and **LICENSE** generated
* There are **no Android and iOS** folders
* pubspec.yaml has lines for **author** and **homepage** added
* There are a **test** and **lib** folder with a pre-generated Dart file in it

## Editing pubspec.yaml

Now you need to edit the pubspec.yaml in order to describe the package and add your name (as the author) and a homepage for the package. This can be your private or your company hoempage or the URL of the GitHub project.

![pubspec.yaml](/img/pubspec_yaml.png)

## Write the code for the package

Of course you need to write the source code of your package. If you need to strucure the code of your package, create a sub-folder called ```src``` under the ```lib``` folder and put every source file there. Because the users of you package will only import the one main source file, you need to create entry points there for the other files in the ```src```folder.

```dart
library my_new_package;

export 'src/part1.dart';
export 'src/part2.dart';
```

## Create a public repository on GitHub

Create a public repository to hold all the code, the commits and version history of your project. Upload your local repository to GutHub. On the page of your package on [pub.dev](https://pub.dev) there will be a refernce to that repository. Users can file you issues there, if they find bugs or pull-requests, if the wish to contribute to your code.

## Write documentation

Writing documentation should be normal practice for you as a developer. Here documentation gets extra importance, because the users of the package need guidance, how to use it. 

### Exxample code

It's common practice to create a folder ```example``` under the project root folder and place the code of a sample app there, that uses your packaage. Doing so you can demonstrate the basi usage of the package. 

### README.md

Write a README.md file. This file's content will serve as the start page for your GitHub repository as well as the packages's page on [pub.dev](https://pub.dev). Here you give a brief introduction into your package. It's fine to present the users some code snippets, maybe some screen shots also and examples. Your README.md should be as comprehemsive as neccessary to understand, how the package works.

### CHANGELOG.md

The content of CHANGELOG.md wille be taken to list all the updates of you package code.

```md
## [0.0.1+1] - 23 December 2020
* Fixed issue
```

The content of this file will be displayed under the *Changelog* tab on your [pub.dev](https://pub.dev) package page. 

### LICENSE

Your package must have a LICENSE file. Write your own license or check the license files available on [Github](https://docs.github.com/en/free-pro-team@latest/github/creating-cloning-and-archiving-repositories/licensing-a-repository) to selct one.

### Write tests

