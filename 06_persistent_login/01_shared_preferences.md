We need to save our token in the device storage, for that we will use a package called `shared_preferences`.

Install `shared_preferences` package into your project:

```shell
flutter pub add shared_preferences
```

Then import it in your provider:

```dart
import 'package:shared_preferences/shared_preferences.dart';
```

The way this works is simple, we store a string and then assign it a key to be able to retrieve it later, so let's use it in our signup function and store the token:

```dart
  void signup({required User user}) async {
    token = await AuthServices().signup(user: user);
    SharedPreferences prefs = await SharedPreferences.getInstance();
    prefs.setString('token', token);
    notifyListeners();
  }
```

And we do the same in our signin function:

```dart
  void signin({required User user}) async {
    token = await AuthServices().signin(user: user);
    SharedPreferences prefs = await SharedPreferences.getInstance();
    prefs.setString('token', token);
    notifyListeners();
  }
```

Repeated code!, let's create a separate function for this:

```dart
  void setToken(String token) async {
    SharedPreferences prefs = await SharedPreferences.getInstance();
    prefs.setString('token', token);
  }
```

Then use it in both functions:

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

We successfully stored the token, let's create a function to retrieve the token:

```dart
  void getToken() async {
    SharedPreferences prefs = await SharedPreferences.getInstance();
    token = prefs.getString('token') ?? "";
    notifyListeners();
  }
```

And we will call this function in our `isAuth` getter:

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

Try to signin then restart your app!

One more thing, try to signout and then restart your app, you are signed in again!

In our signout function, we need to clear the token from our storage:

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
