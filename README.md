# berbix_flutter_demo
Demonstrates how to use the berbix_flutter plugin.

# Fetching Dependencies
We can fetch the demo dependency packages by running:

```Bash
flutter pub get
```

# Building

## Android

`flutter build appbundle`

## iOS

`flutter build ios --release --no-codesign`

## Setting a client token
Like any other Berbix SDK, the Flutter SDK requires a **Client Token*** to perform a transaction on behalf of a user. You can review our Server Side Documentation for help on generating a client token.

Once you have a valid client token, you can pass that to the SDK like so:

```dart
// Replace with a valid token!
BerbixFlutter.setClientToken("client_token_for_session"); 
```

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

