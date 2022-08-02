We need to save our token in the device storage, and to do that, we will use a package called `shared_preferences`.

30. Install `shared_preferences` package into your project:

```shell
flutter pub add shared_preferences
```

31. Import it in the auth provider:

```dart
import 'package:shared_preferences/shared_preferences.dart';
```

The way this package works is simple, it stores a string and we can assign it a key to be able to retrieve it later.

In our case, we will store a string named 'token', and assign it our `token` as shown in the code below:

```dart
  void signup({required User user}) async {
    token = await AuthServices().signup(user: user);
    SharedPreferences prefs = await SharedPreferences.getInstance();
    prefs.setString('token', token);
    notifyListeners();
  }
```

32. Use the same package to store the token in the signin function:

```dart
  void signin({required User user}) async {
    token = await AuthServices().signin(user: user);
    SharedPreferences prefs = await SharedPreferences.getInstance();
    prefs.setString('token', token);
    notifyListeners();
  }
```

Repeated code! Let's create a separate function for this:

```dart
  void setToken(String token) async {
    SharedPreferences prefs = await SharedPreferences.getInstance();
    prefs.setString('token', token);
  }
```

33. Use the `setToken` in both `signin` & `signup` functions:

```dart
  void signup({required User user}) async {
    token = await AuthServices().signup(user: user);
    setToken(token);
    notifyListeners();
  }

  void signin({required User user}) async {
    token = await AuthServices().signin(user: user);
    setToken(token);
    notifyListeners();
  }
```

We successfully stored the token. Let's create a function to retrieve it:

```dart
  void getToken() async {
    SharedPreferences prefs = await SharedPreferences.getInstance();
    token = prefs.getString('token') ?? "";
    notifyListeners();
  }
```

34. Call this function in the `isAuth` getter:

```dart
  bool get isAuth {
    getToken();
    if (token.isNotEmpty && Jwt.getExpiryDate(token)!.isAfter(DateTime.now())) {
      user = User.fromJson(Jwt.parseJwt(token));
      return true;
    }
    return false;
  }
```

Try to sign in and restart your app!

One more thing to do, try to sign out and then restart your app, you are signed in again!

In the `signout` function, we need to clear the token from our storage:

```dart
  void logout() async {
    SharedPreferences prefs = await SharedPreferences.getInstance();
    prefs.remove('token');
    token = "";
    notifyListeners();
  }
```

And we also need to clear it if the token is expired:

```dart
  bool get isAuth {
    getToken();
    if (token.isNotEmpty && Jwt.getExpiryDate(token)!.isAfter(DateTime.now())) {
      user = User.fromJson(Jwt.parseJwt(token));
      return true;
    }
    logout();
    return false;
  }
```
