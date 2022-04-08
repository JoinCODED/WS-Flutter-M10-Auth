The first step is to create a model for our user, just like we did with the books model.

In your `models` folder, create a new file called `user` and create the following model:

```dart
class User {
  int? id;
  String username;
  String? password;

  User({
    this.id,
    required this.username,
    this.password,
  });
```

We need to also create `fromJson` and `toJson` constructors. but this time we will utilize some amazing packages to generate all that code for us.
