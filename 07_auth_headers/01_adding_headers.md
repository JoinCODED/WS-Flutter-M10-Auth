As we agreed, a user can't create a book unless he's authenticated.

Signin and try to create a book, you will get `401` error, but we are signed in :(

If we imagined the token as our key, and shared preferences as our pocket, that means the key is in our pocket, to use it we need to get it out from our pocket and send it to the lock right?

In your `providers/auth_provider.dart` locate the `isAuth` getter:

```dart
  bool get isAuth {
    getToken();
    if (token.isNotEmpty && Jwt.getExpiryDate(token)!.isAfter(DateTime.now())) {
      user = User.fromJson(Jwt.parseJwt(token));
      Client.dio.options.headers = {
        HttpHeaders.authorizationHeader: 'Bearer $token',
      };
      return true;
    }
    logout();
    return false;
  }
```

That's it!
