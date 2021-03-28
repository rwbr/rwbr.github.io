---
title: "How to Set Default Window Size"
date: 2021-03-28T11:45:53+02:00
tags: [flutter, desktop]
---

Flutter for Desktop has been released as beta yet. Now you can develop desktop applications with your knowledge stack. 

 <!--more-->

However, it's still in beta. Some features are still missing like setting the default size of the window. Here I will show, how you can solve that puzzle.

# Desktop support for Flutter

While the support for desktop in Flutter is still in beta state, the Flutter team ships a snapshot of desktop support in the stable channel. So to try out the desktop support **you don't neccessarily have to switch channels**. 

For additional information about it and how to activate it please follow the [link to the official web site](https://flutter.dev/desktop). 

## Controlling the window size of the application

If you develop a desktop application, there is no preset canvas size like on the mobile platforms  Usually you don't start your application in full-screen-mode on the desktop. Rather your application starts with a preset default window size. 

At the moment of writing this, there is no integrated way in the SDK to set the window size. Currently the only way to control the initial size is using native code. You can set it manually in `macos/Runner/MainFlutterWindow.swift`.
(See [issue #30736](https://github.com/flutter/flutter/issues/30736)).

## Using a plugin to set the initial size

There is a plugin for this. This plugin will be of temporary nature, as this feature will sooner or later get included in the SDK. But for now it solves this problem. I suggest using this plugin, if you struggle with this problem. It is probably the **better way than hard-coding** directly modifying the native code, especially if you have multiple platforms you want to work on.

First add to the pubspec.yaml something like:

```yaml
dependencies:
...
  window_size:
    git:
      url: git://github.com/google/flutter-desktop-embedding.git
      path: plugins/window_size
      ref: 927f8cbc09b35d85245c095f2db8df9b186f6618
```

Using the specific Git reference  gives you full control over when you choose to pull updated code and make any changes this might entail. The plugin offers setting minimal and maximal window sizes as well as querying screen parameters  

```dart
import 'dart:io'
import 'package:window_size/window_size.dart';
...
void main() {
  WidgetsFlutterBinding.ensureInitialized();
  if (Platform.isWindows || Platform.isLinux || Platform.isMacOS) {
    setWindowTitle("My App");
    setWindowMinSize(Size(800, 600));
    setWindowMaxSize(Size(1024, 800));
    setWindowSize(Size(1024, 800));
  }
  runApp(MyApp());
}
```