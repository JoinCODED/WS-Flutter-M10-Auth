Let's create a provider for our user info.

In your `providers` folder create a file called `auth_provider.dart`.

```dart
class AuthProvider extends ChangeNotifier {
  String token = "";
  late User user;
}
```

We will have 2 properties for now, the `JWT` token and a `User` object that we are going to initialize later so we marked it as `late`.
