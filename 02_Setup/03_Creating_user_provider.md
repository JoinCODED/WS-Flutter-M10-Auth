Now, let's create a provider for our user info.

7. In your `providers` folder, create a file called `auth_provider.dart`.

```dart
class AuthProvider extends ChangeNotifier {
  String token = "";
  late User user;
}
```

We have two properties for now: The `JWT` token, and a `User` object that is marked as `late` because we are going to initialize later.
