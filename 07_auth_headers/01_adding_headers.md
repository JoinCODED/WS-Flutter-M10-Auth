As we agreed, the user cannot create a book unless he/she is authenticated.

Sign in and try to create a book. You will get `401` error, although you are signed in :(.

If we imagine the token as a key, and the shared preferences as our pocket, that means the key is in our pocket, and to use it, we need to get it out from our pocket and send it to the lock, right?

36. In your `providers/auth_provider.dart` locate the `isAuth` getter:

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

That is it! 🥳
