We are initializing 2 Dio instances, one in the books services, and one in the auth services.

So it would be a good idea to create a singleton for `dio` to use in both files.

In your `services` folder create a file called `client.dart`:

```dart
import 'package:dio/dio.dart';

class Client {
  static final Dio dio = Dio(BaseOptions(baseUrl: 'https://coded-books-api-auth.herokuapp.com'));
}
```

Now we can use this singleton in our `BooksServices`:

```dart
class BooksServices {
  Future<List<Book>> getBooks() async {
    List<Book> books = [];
    try {
      Response response = await Client.dio.get('/books');
      books =
          (response.data as List).map((book) => Book.fromJson(book)).toList();
    } on DioError catch (error) {
      print(error);
    }
    return books;
  }

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
      Response response = await Client.dio.post('/books', data: data);
      retrievedBook = Book.fromJson(response.data);
    } on DioError catch (error) {
      print(error);
    }
    return retrievedBook;
  }

  Future<Book> updateBook({required Book book}) async {
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
      Response response = await Client.dio.put('/books/${book.id}', data: data);
      retrievedBook = Book.fromJson(response.data);

    } on DioError catch (error) {
      print(error);
    }
    return retrievedBook;
  }

  Future<void> deleteBook({required int bookId}) async {
    try {
      await Client.dio.delete('/books/${bookId}');
    } on DioError catch (error) {
      print(error);
    }
  }
}
```

And in `AuthServices`:

```dart
class AuthServices {
  Future<String> signup({required User user}) async {
    late String token;
    try {
      Response response = await Client.dio.post('/signup', data: user.toJson());
      token = response.data["token"];
    } on DioError catch (error) {
      print(error);
    }
    return token;
  }
}
```
