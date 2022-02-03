# berbix_flutter_demo

Demonstrates how to use the berbix_flutter plugin.
# Building

## Android

`flutter build appbundle`

## iOS

`flutter build ios --release --no-codesign`

# Add Dependency
To begin we'll need to add `berbix_flutter` as a dependency to our project. You can accomplish this by executing:

```Bash
flutter pub add berbix_flutter
```

from your project directory. That should update your **pubspec.yml** like so:

```yaml
# Other Settings
# ...
dependencies:
  flutter:
    sdk: flutter
  berbix_flutter: ^1.0.0
```

After we've updated our configuration, we can fetch the new packages by running:

```Bash
flutter pub get
```

# Integrating
Once the dependencies have been fetched, we're ready to make use of the new package. First we'll import the package in the **.dart** file we'd like to start the Berbix flow from.

```dart
import 'package:berbix_flutter/berbix_flutter.dart';
```

## Setting a client token
Like any other Berbix SDK, the Flutter SDK requires a **Client Token*** to perform a transaction on behalf of a user. You can review our Server Side Documentation for help on generating a client token.

Once you have a valid client token, you can pass that to the SDK like so:

```dart
// Replace with a valid token!
BerbixFlutter.setClientToken("client_token_for_session"); 
```

## Completing a transaction
Once the client token is in place, you can perform a transaction simply by calling

```dart
BerbixFlutter.startFlow();
```

At this point, the SDK will handle navigation until the user either completes or cancels the verification flow.

## Handling Errors / Exceptions

When setting a client token, you may encounter a `BerbixMissingClientTokenError` if the client token is omitted. If the token was present, but there was a problem with it, you'll see `BerbixInvalidClientTokenException` instead.

```dart
try {
  var result = await BerbixFlutter.setClientToken("your-client-token-here");
} on BerbixMissingClientTokenError catch (error) {
  // We forgot to add the client token
} catch (error) {
  // Something went wrong else where
  FlutterError.presentError(error);
}
```

While presenting a flow, you may encounter other exceptions, which can be caught like so:

```dart
try {
  var result = await BerbixFlutter.startFlow();
} catch (error) {
  // Something went wrong while completing the flow
  FlutterError.presentError(error);
  // The area of the error is in error.code ("user", "api", "camera", "state", "berbix")
  // A detailed error message is available in error.details
}
```


