The first step is to create a model for our user, just like we did with the books model.

1. In your `models` folder, create a new file called `user` and add the following model:

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

We also need to create `fromJson` and `toJson` constructors. But, this time we will use some amazing packages to generate all that code for us.
