We created a user. Let's test that out by signing in with the user's credentials.

18. In your `services/auth.dart`, create a function for the `/signin` endpoint:

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

19. Create a void function in the `auth` provider that prints the token:

```dart
  void signin({required User user}) async {
    token = await AuthServices().signin(user: user);
    print(token);
  }
```
