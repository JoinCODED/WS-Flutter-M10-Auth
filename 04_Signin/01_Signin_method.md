We created a user, lets test that out by signing in as that user.

In your `services/auth.dart`, create a function to the `/signin` endpoint:

```dart
  Future<String> signin({required User user}) async {
    late String token;
    try {
      Response response = await Client.dio.post('/signin', data: user.toJson());
      token = response.data["token"];
    } on DioError catch (error) {
      print(error);
    }
    return token;
  }
```

Then Let's create the function in our `auth` provider:

```dart
  void signin({required User user}) async {
    token = await AuthServices().signin(user: user);
    print(token);
  }
```
