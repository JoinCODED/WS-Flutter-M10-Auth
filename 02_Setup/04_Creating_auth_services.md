Our endpoints are:

```
Post /signin
Post /signup
```

And we need to send a username and password to those endpoints.

In your `services` folder, create a new file `auth_services.dart` and initialize a `dio` instance like we did before:

```dart
class AuthServices {
  final Dio _dio = Dio();

  final _baseUrl = 'http://10.0.2.2:5000';
}
```

The response will look like this:

```json
"token": "xxxx.yyyy.zzzz"
```

And what we need from that is the token value.

Let's start by creating the `signup` request:

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

We created a function that takes a `User` object as an argument, then we passed it to our `post` request, but we used the `toJson` constructor to convert the data to the `json` format that we agreed to use previously.

Then from the `response` object, we selected the `token` property which is a `string`, thus why our function return is of type `String`.

Next, let's create the `signup` function in our `auth` provider:

```dart
  void signup({required User user}) async {
    token = await AuthServices().signup(user: user);
    print(token);
  }
```
