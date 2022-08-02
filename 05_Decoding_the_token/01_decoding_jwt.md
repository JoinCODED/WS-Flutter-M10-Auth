We successfully got our token from signing in or signing up.
The next step is to use this token to get the user info.

24. In the `auth_provider.dart` file, create a getter that tells if the user is authenticated:

```dart
  bool get isAuth {
    if (token.isNotEmpty) {
      return true;
    }
    return false;
  }
```

In the simplest forms, if the token exists, we have a user. Otherwise, the user has to login into the app.

But that is not always the case. Maybe there is a token, but it is expired. In that case, we need to sign the user out in order to make him/her sign in again and get a new token.

To get the expiry date of the token, we need to decode it first, and we will use the `jwt_decode` package for that:

```shell
flutter pub add jwt_decode
```

25. Import the `jwt_decode` package in the auth provider file:

```dart
import 'package:jwt_decode/jwt_decode.dart';
```

The `jwt_decode` package provides us with an amazing method called `getExpiryDate` that checks if the token is expired.

```dart
  bool get isAuth {
    if (token.isNotEmpty && Jwt.getExpiryDate(token)!.isAfter(DateTime.now())) {
      return true;
    }
    return false;
  }
```

We used `Jwt.getExpiryDate(token)!` to get the expiry time and we made sure that it `isAfter` the current date and time. If it is not, that means the token is expired.

The next step is to get the data from the token and map them to our `User` object. As we mentioned, `JWT` stands for `JSON` Web Token, so we need to use the `fromJson` constructor:

```dart
  bool get isAuth {
    if (token.isNotEmpty && Jwt.getExpiryDate(token)!.isAfter(DateTime.now())) {
      user = User.fromJson(Jwt.parseJwt(token));
      return true;
    }
    return false;
  }
```

If the token is not expired, we will map the data to the `user` variable.
