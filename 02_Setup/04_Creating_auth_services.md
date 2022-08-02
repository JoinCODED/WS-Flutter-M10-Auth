Our endpoints are:

```
Post /signin
Post /signup
```

We need to send a username and password to those endpoints.

8. In your `services` folder, create a new file called `auth_services.dart` and initialize a `dio` instance like we did before:

```dart
class AuthServices {
  final Dio _dio = Dio();

  final _baseUrl = 'https://coded-books-api-auth.herokuapp.com/';
}
```

The response will look like this:

```json
"token": "xxxx.yyyy.zzzz"
```

And what we need from that is the token value.

9. Create the `signup` request as follows:

```dart
  Future<String> signup({required User user}) async {
    late String token;
    try {
      Response response =
          await _dio.post(_baseUrl + '/signup', data: user.toJson());
      token = response.data["token"];
    } on DioError catch (error) {
      print(error);
    }
    return token;
  }
```

We created a function that takes a `User` object as an argument, then we passed it to our `post` request. We used the `toJson` constructor to convert the data to the `json` format that we agreed to use previously.

Then, from the `response` object, we selected the `token` property which is a `string`, this is why our function return is of type `String`.

10. Create the `signup` function in the `auth` provider as follows:

```dart
  void signup({required User user}) async {
    token = await AuthServices().signup(user: user);
    print(token);
  }
```
