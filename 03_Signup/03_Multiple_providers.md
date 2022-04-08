At this point, we need to call our `signup` function from the `auth` provider.

So we need to include this provider in `main.dart`, we need to refactor some code to be able to add multiple providers to our app:

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

In this way you can include as much providers as you wish to your app.
