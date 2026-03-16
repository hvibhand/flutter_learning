# Flutter & Dart - The Complete Guide

## Deep Dive: Position & Named Arguments
In the previous lecture, you learned about **"positional"** and **"named"** arguments / parameters.

In general, function parameters / arguments (the term is used interchangeably here) are a **key concept**.

You use arguments to pass values into a function. The function may then use these parameter values to work with them - e.g., to display them on the screen, use them in a calculation or send them to another function.

In Dart (and therefore Flutter, since it uses Dart), you have two kinds of parameters you can accept in functions:

- **Positional:** The position of an argument determines which parameter receives the value
```dart
void add(a, b) { // a & b are positional parameters
  print(a + b); // print() is a built-in function that will be explained later
}
 
add(5, 10); // 5 is used as a value for a, because it's the first argument; 10 is used as a value for b
```

- **Named:** The name of an argument determines which parameter receives the value
```dart
void add({a, b}) { // a & b are named parameters (because of the curly braces)
  print(a + b); 
}  
 
add(b: 5, a: 10); // 5 is used as a value for b, because it's assigned to that name; 10 is used as a value for a
```

Besides the different usage, there's **one very important difference** between positional and named arguments: By default, positional parameters are required and must not be omitted - on the other hand, named arguments are optional and can be omitted.

In the example above, when using **named parameters**, you **could** call `add()` like this:
```dart
add();
```
or
```dart
add(b: 5);
```
When using **positional parameters**, calling `add()` like this would be **invalid** and hence cause an **error!**

You can change these behaviors, though. You can make positional arguments **optional** and named arguments **required**.

Positional arguments can be made optional by wrapping them with square brackets (`[]`):
```dart
void add(a, [b]) { // b is optional
  print(a + b);
}
```
Once a parameter is optional, you can also assign a default value to it - this value would be used if no value is provided for the argument:
```dart
void add(a, [b = 5]) { // b is optional, 5 will be used as a default value
  print(a + b);
}
add(10); // b would still be 5 because it's not overwritten
add(10, 6); // here, b would be 6
```
Default values can also be assigned to named parameters - which are optional by default:
```dart
void add({a, b = 5}) { // b has a default value of 5
  print(a + b); 
}  
 
add(b: 10); // for b, 10 would be used instead of 5; a has no default value and would be "null" here => a special value type you'll learn about throughout this course
```
You can also make named parameters `required` by using the built-in required keyword:
```dart
void add({required a, required b}) { // a & b are no longer optional
  print(a + b); 
}
```
You will, of course, see these different use-cases in action throughout the course.

## Flutter & Code Formatting
Dart comes with a code formatter which - for example when using VS Code - will cause your code to be auto-formatted to be more readable.

Since **Dart 3.7.0** the code formatter has changed slightly (compared to what you see in the course videos).

→ The code formatter will now remove the final comma and put code onto one line, if it fits the configured line width. This is not a significant change and does NOT affect how the code execute.

**Important: You can change this (back to what you see in the videos)!**

To do that, edit (if they file already exists) or add a new file `analysis_options.yaml` in your Flutter project.

On the outermost indentation level, add the following configuration:
```dart
# This file configures the analyzer, which statically analyzes Dart code to
# check for errors, warnings, and lints.
#
# The issues identified by the analyzer are surfaced in the UI of Dart-enabled
# IDEs (https://dart.dev/tools#ides-and-editors). The analyzer can also be
# invoked from the command line by running `flutter analyze`.

# The following line activates a set of recommended lints for Flutter apps,
# packages, and plugins designed to encourage good coding practices.
include: package:flutter_lints/flutter.yaml

formatter:
trailing_commas: preserve

linter:
# The lint rules applied to this project can be customized in the
# section below to disable rules from the `package:flutter_lints/flutter.yaml`
# included above or to enable additional rules. A list of all available lints
# and their documentation is published at https://dart.dev/lints.
#
# Instead of disabling a lint rule for the entire project in the
# section below, it can also be suppressed for a single line of code
# or a specific dart file by using the `// ignore: name_of_lint` and
# `// ignore_for_file: name_of_lint` syntax on the line or in the file
# producing the lint.
rules:
# avoid_print: false  # Uncomment to disable the `avoid_print` rule
# prefer_single_quotes: true  # Uncomment to enable the `prefer_single_quotes` rule
```
Additional information about this file can be found at https://dart.dev/guides/language/analysis-options

Also see this thread: https://www.udemy.com/course/learn-flutter-dart-to-build-ios-android-apps/learn/lecture/49997051#questions/23439803

## Deep Dive: Flutter's (Stateful) Widget Lifecycle
Every Flutter Widget has a built-in lifecycle: A collection of methods that are automatically executed by Flutter (at certain points of time).

There are three extremely important (stateful) widget lifecycle methods you should be aware of:

- `initState()`: Executed by Flutter when the StatefulWidget's State object is **initialized**
- `build()`: Executed by Flutter when the Widget is built for the **first time** AND after `setState()` was called
- `dispose()`: Executed by Flutter right before the Widget will be **deleted** (e.g., because it was displayed conditionally)

You will encounter them all multiple times throughout the course - therefore you don't have to memorize them now and you will see them in action. It's still worth learning about them right now already.

## Using "if" Statements In Lists
The `if` statement is a crucial feature of the Dart language - actually, it's a core feature of pretty much all programming languages.

In addition to what you learned in the previous lecture, in Dart, you may also use `if` inside of lists to conditionally add items to lists:
```dart
final myList = [
    1,
    2,
    if (condition)
        3
];
```
In this example, the number `3` will only be added to `myList` if `condition` was met (`condition` can be `true` or `false` or a check that yields `true` or `false` - e.g., `day == 'Sunday'`).

Please note that there are **NO curly braces** around the `if` statement body. The `if` statement body also only comprises the next line of code (i.e., you can't have multiple lines of code inside the `if` statement).

You can also specify an `else` case - an alternative value that may be inserted into the list if `condition` is not met:
```dart
final myList = [
    1,
    2,
    if (condition)
        3
    else
        4
];
```
Using this feature is optional. Alternatively, you could, for example, also work with a ternary expression:
```dart
final myList = [
    1,
    2,
    condition ? 3 : 4
];
```
Especially when inserting more complex values (e.g., a widget with multiple parameters being set) into a more complex list (e.g., a list of widgets passed to a `Column()` or `Row()`), this feature can lead to more readable code.

You will also see it being used later in the course. It will be explained again then.

You can also learn more about this feature here: https://github.com/dart-lang/language/blob/master/accepted/2.3/control-flow-collections/feature-specification.md

## if Statements & Comparison Operators
When using `if` **statements** - no matter if inside or outside of functions - as well as when using **ternary expressions**, you ultimately must provide a boolean value (true / false):
```dart
if (true) {
    // do something ...
}
// or
true ? 'this' : 'that'
```
Of course, hardcoding `true` or `false` into the code makes no sense though - you wouldn't need an `if` statement or ternary expression if a value would always be `true` or always be `false`.

Instead, `true` or `false` is typically derived by comparing values - e.g, comparing a number to an expected value:
```dart
if (randomNumber == 5) {
    // do something
}
```
The `==` operator checks for **value equality** (i.e., the values on the left and right side of the operator must be equal). It **must not be mistaken** with the **assignment operator** (which uses a single equal sign: `=`).

The assignment operator is used to assign values to variables:
```dart
var userName = 'Max'; // assignment operator used
if (userName == 'Max') { ... } // comparison operator used
```
Besides the equality operator (`==`) Dart also supports many other key comparison operators:

- `!=` to check for inequality (`randomNumber != 5` expects `randomNumber` to NOT be `5`, i.e., to be any other value)
- `>` to check for the value on the left to be greater than the value on the right (`randomNumber > 5` yields `true` if `randomNumber` is greater than `5`)
- `>=` to check for the value on the left to be greater than or equal to the value on the right (`randomNumber >= 5` yields `true` if `randomNumber` is greater than `5` or equals `5`)
- `<` to check for the value on the left to be smaller than the value on the right (`randomNumber < 5` yields `true` if `randomNumber` is smaller than `5`)
- `<=` to check for the value on the left to be smaller than or equal to the value on the right (`randomNumber <= 5` yields `true` if `randomNumber` is smaller than `5` or equals `5`)

## Using "for" Loops In Lists
Just as you can also use the `if` keyword inside of lists (to add elements conditionally), you can also use the `for` keyword to add multiple items into a list:
```dart
final numbers = [5, 6];
final myList = [
    1,
    2,
    for (final num in numbers)
        num
];
```
In this example, the numbers `5` and `6` will be added to `myList` (hence `myList` thereafter is `[1, 2, 5, 6]`).

This `for ... in` syntax is a special variation of the for loop that loops through multiple items in a list. You will see it again later in the course - both outside and inside of a list. It will also be explained again later.

The idea behind this loop is to simplify the process of performing some operation on all items in a list.

When used in a list, it's essentially an alternative to the spread operator (`...`):
```dart
final numbers = [5, 6];
final myList = [
    1,
    2,
    ...numbers
];
```
It can be useful in scenarios where values must be transformed before being added to a list - the `for ... in` loop can then be used instead of `map()` + spread operator:
```dart
final numbers = [5, 6];
final myList = [
    1,
    2,
    ...numbers.map((n) {
        return n * 2;
    }) // adds 10 and 12
];
```
can be replaced with:
```dart
final numbers = [5, 6];
final myList = [
    1,
    2,
    for (final num in numbers)
        num * 2 // adds 10 and 12
];
```
As mentioned, you will learn more about `for` later in the course.

You can also learn more about `for ... in` inside of lists here: https://github.com/dart-lang/language/blob/master/accepted/2.3/control-flow-collections/feature-specification.md#repetition

## Note: A Typo In The Next Lecture
Just a quick note: In the next lecture, in the questions_summary.dart file, there will be a typo.

Instead of writing
```dart
Text(((data['question'] as int) + 1).toString()),
```
write
```dart
Text(((data['question_index'] as int) + 1).toString()),
```

## Running the App on Real iOS or Android Devices
In this course, we mainly run the app on virtual devices - the Android emulator or iOS simulator.

For development, using these virtual devices is great because changes are reflected almost instantly, you can use your real keyboard and benefit from many other convenience features.

But, of course, you should also test your app on some real devices at some point.

Therefore, the following articles provide step-by-step instructions on how to run your Flutter app on real Android or iOS devices (whilst developing it). Always select the "Physical device" tab:

- Run on Android (when working on Windows, macOS or Linux): https://docs.flutter.dev/get-started/install/windows#set-up-your-android-device

- Run on iOS (macOS only): https://docs.flutter.dev/get-started/install/macos#deploy-to-ios-devices

Keep in mind that you can only build + run iOS apps when on a macOS device. Of course the code will be the same, no matter which platform you're using - but you can only build + run an iOS app from a Mac.

__Flutter also supports other platforms – e.g, you can also build Windows or macOS desktop programs from your Flutter source code. However, this course focuses on building mobile apps for Android & iOS. Nonetheless, you can of course use the official documentation to also try running your app on those other platforms.__

## SnackBar Durations
In the next lecture we'll use a widget called "SnackBar".

One important change with the latest version of Flutter – to have it disappear automatically, add `persist: false` to the SnackBar widget (also see [this thread](https://www.udemy.com/course/learn-flutter-dart-to-build-ios-android-apps/learn/lecture/37143184#questions/24027419) if you're running into issues).

## Flutter & Material 3
If you're working with a recent version of Flutter, it will automatically use the **"Material 3"** look and settings.

I recorded this course with Material 3, BUT at the time when I did record it, this mode had to be enabled manually by setting `useMaterial3` to `true` when working with themes.

You'll see that in the next lectures.

Since Material 3 is the default now, `useMaterial3` no longer needs to be set to `true`, hence you **can and should skip that setting**. The rest of the code shown in the lectures remains unchanged.

## Important: Adding Dark Mode
In the next lecture, we'll add **"Dark Mode"** to the app.

The code you'll see in the next lecture works as shown, with **one important exception** (that you should adjust in your code):

The `useMaterial3: true` flag is no longer needed if you're using the latest version of Flutter - because Material 3 is already the default with that.

In addition, instead of adding a dark theme like this:
```dart
ThemeData.dark(
    useMaterial3: true,
    colorScheme: kColorScheme,
    cardTheme: ...
)
```
you should add it like this (in the next lecture, when we write that code):
```dart
ThemeData.dark().copyWith( // dark() no longer takes any arguments
    useMaterial3: true,
    colorScheme: kColorScheme,
    cardTheme: ...
)
```
That's all!

## Replacing WillPopScope with PopScope
In recent versions of Flutter, the `WillPopScope` widget we're using in the next lecture has been marked as deprecated.

Therefore, in the next lecture, instead of using `WillPopScope` you **should use** `PopScope`.

The code we write in the next lecture should look like this:
```dart
PopScope(
    canPop: false,
    onPopInvokedWithResult: (bool didPop, dynamic result) {
        if(didPop) return;
        Navigator.of(context).pop({
            Filter.glutenFree: _glutenFreeFilterSet,
            Filter.lactoseFree: _lactoseFreeFilterSet,
            Filter.vegetarian: _vegetarianFilterSet,
            Filter.vegan: _veganFilterSet,
        });
    },
    child: Column(...) // same code as shown in the next lecture
),
```
NOT like this:
```dart
WillPopScope(
    onWillPop: () async {
        Navigator.of(context).pop({
            Filter.glutenFree: _glutenFreeFilterSet,
            Filter.lactoseFree: _lactoseFreeFilterSet,
            Filter.vegetarian: _vegetarianFilterSet,
            Filter.vegan: _veganFilterSet,
        });
        return false;
    },
    child: Column(...) // same code as before
),
```

## An Alternative Navigation Pattern: Using Named Routes
In this section, you learned about the **recommended navigation approach**: Pushing and popping MaterialPageRoute objects to load different screens.

There also exists an **alternative approach**, though - you can assign names to routes and load your routes via those names. However, that approach is not recommended (for most apps).

Nonetheless, you can explore this alternative approach via the official documentation: https://docs.flutter.dev/development/ui/navigation#using-named-routes

## Riverpod Versions
This course was recorded based on Riverpod versions <3.

If you're working with more recent versions in your project, you will need to import certain classes like `StateProvider` from the `legacy.dart` file like this:
```dart
import 'package:flutter_riverpod/legacy.dart';
```
Also see: https://www.udemy.com/course/learn-flutter-dart-to-build-ios-android-apps/learn/lecture/37144826#questions/24147091

## "riverpod" vs "provider" - There are many Alternatives!
Older versions of this course used the "provider" package instead of "riverpod" for app-wide state management.

riverpod is a library created by the same developer as the provider library - it's essentially a re-write of the provider package, fixing many of the flaws of that library (also see: https://github.com/rrousselGit/riverpod).

That's why this course uses riverpod.

As mentioned in the section, there generally are many other alternative packages you could use instead - for example Redux or Bloc. [This page](https://docs.flutter.dev/development/data-and-backend/state-mgmt/options) from the official documentation gives you a good overview of available packages - definitely feel free to play around with them and find the package your personally like most.

## Important: "location" Package & Android
In the next lecture, we'll add the "location" package (a third-party package) get the user's location.

In the next lectures, when running the app on Android, you might get an error though (after adding that package).

If that should be the case, try editing your `android/settings.gradle` file and make sure the following line:
```groovy
id "org.jetbrains.kotlin.android" version "1.9.21" apply false
```
reflects your current Kotlin version (you find that version in the `build.gradle` file).

Also see this Q&A thread (and the threads linked in there) for further context: https://www.udemy.com/course/learn-flutter-dart-to-build-ios-android-apps/learn/lecture/37130520#questions/21453790/

## Adding Your Own Native Code
With Flutter, when using native device features, you'll very likely use external packages most of the time - like the ImagePicker or GoogleMaps packages used in this section.

But if you need to tap into a certain native device functionality that's not exposed by any package, you can also write your own native code and connect that to your Flutter code.

It's a rarely needed feature but this page from the official documentation explains how you could add your own native code: https://docs.flutter.dev/development/platform-integration/platform-channels

## FlutterFire Configuration
In the next lecture, we'll connect our Flutter project to Firebase by running the `flutterfire configure` command.

When going through all the questions asked by this command (as shown in the next lecture), you must specify an Android application ID.

DON'T use the default (com.example.app) there! Instead, **specify the name of your package** which you find in the `android/app/build.gradle` file.

## Firebase & Image Storage
Unfortunately, Firebase now requires you to **sign up with a credit card** in order to use their storage service.

However, **you can still follow along for free** since they still provide a **generous free tier** - i.e., as long as you don't exceed that tier (which you won't, if you just follow along with this course example and you don't upload lots of images), you can use their storage for free.

## A Note About Reading Data From Firestore
In the next lectures, we'll **read data** from Firebase.

If you should be facing any **issues** with that during the next lectures, consider diving into the following **Q&A threads** which offer potential solutions. Of course, you can **ignore** those threads if you don't face any issues.

https://www.udemy.com/course/learn-flutter-dart-to-build-ios-android-apps/learn/lecture/37736704#questions/19981674

https://www.udemy.com/course/learn-flutter-dart-to-build-ios-android-apps/learn/lecture/37736700#questions/19980322

