As we agreed, a user can't create a book unless he's authenticated.

Signin and try to create a book, you will get `401` error, but we are signed in :(

If we imagined the token as our key, and shared preferences as our pocket, that means the key is in our pocket, to use it we need to get it out from our pocket and send it to the lock right?

In your `services/books.dart` locate the create book function:

```dart
  Future<Book> createBook({required Book book}) async {
    late Book retrievedBook;
    try {
      FormData data = FormData.fromMap({
        "title": book.title,
        "description": book.title,
        "price": book.price,
        "image": await MultipartFile.fromFile(
          book.image,
        ),
      });
      Response response = await _dio.post(_baseUrl + '/books', data: data);
      retrievedBook = Book.fromJson(response.data);
    } on DioError catch (error) {
      print(error);
    }
    return retrievedBook;
  }
```

In this function, get the token from shared preferences:

```dart
  Future<Book> createBook({required Book book}) async {
    SharedPreferences prefs = await SharedPreferences.getInstance();
    String token = prefs.getString('token') ?? "";
[...]
```

The last step, is to send the key to the backend, and we do this by attaching it to the headers of dio:

```dart
  Future<Book> createBook({required Book book}) async {
    SharedPreferences prefs = await SharedPreferences.getInstance();
    String token = prefs.getString('token') ?? "";

    _dio.options.headers = {
      HttpHeaders.authorizationHeader: 'Bearer $token',
    };
[...]
```

That's it!
