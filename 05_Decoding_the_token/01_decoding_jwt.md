We successfully got our token from signing in or signing up, the next step is to use this token to get the user info.

In your `auth_provider.dart`, we will create a getter that tells us if the user is authenticated or not:

```dart
  bool get isAuth {
    if (token.isNotEmpty) {
      return true;
    }
    return false;
  }
```

In the simplest forms, if the token exists, then we have a user, if it's not, the user has to login in our app.

But that's not always right, maybe we have a token but it's expired, in this case we need to sign the user out so he can signin again and get a new token.

To get the expiry date of the token we need to decode it first, and we will use a package for that:

```shell
flutter pub add jwt_decode
```

Import this package in your provider:

```dart
import 'package:jwt_decode/jwt_decode.dart';
```

Then let's use a cool method this package provides:

```dart
  bool get isAuth {
    if (token.isNotEmpty && Jwt.getExpiryDate(token)!.isAfter(DateTime.now())) {
      return true;
    }
    return false;
  }
```

We used `Jwt.getExpiryDate(token)!` to get the expiry time then we made sure that it `isAfter` the date of now, And if it's not, that means the token is expired.

The next step is to get data from the token and mapping them to our `User` object, and as we mentioned, `JWT` stands for `JSON` web token, so we need to use the `fromJson` constructor:

```dart
  bool get isAuth {
    if (token.isNotEmpty && Jwt.getExpiryDate(token)!.isAfter(DateTime.now())) {
      user = User.fromJson(Jwt.parseJwt(token));
      return true;
    }
    return false;
  }
```

So if the token is not expired, we will map the data to our `user` variable.
