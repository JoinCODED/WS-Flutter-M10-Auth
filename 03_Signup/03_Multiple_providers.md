At this point, we need to call our `signup` function from the `auth` provider.

To do that, we have to include this provider in the `main.dart` file and refactor some code to be able to add multiple providers to our app:

```dart
void main() {
  runApp(
    MultiProvider(
      providers: [
        ChangeNotifierProvider<BooksProvider>(create: (_) => BooksProvider()),
        ChangeNotifierProvider<AuthProvider>(create: (_) => AuthProvider()),
      ],
      child: MyApp(),
    ),
  );
}
```

In that way, you can include as much providers as you wish to your app.
