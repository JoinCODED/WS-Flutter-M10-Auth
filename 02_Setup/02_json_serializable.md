We will need two packages that will save us a lot of time and effort.

Install those packages:

```
flutter pub add json_serializable
flutter pub add build_runner
```

The first step is to import `json_serializable` package to our model file:

```dart
import 'package:json_annotation/json_annotation.dart';
```

Then we will add this import, and you will get the red underline that we all hate, but that's fine, it's because the file doesn't exist, it will be magically generated later!

```dart
part 'user.g.dart';
```

Notice that the `user` part should always be the name of the file you are in, for example, if we are doing this for the book model, it would be `book.g.dart`.

Just before the class definition, add this line:

```dart
@JsonSerializable()
class User {
[...]
```

Then, at the end of your class add those lines:

```dart
  factory User.fromJson(Map<String, dynamic> json) => _$UserFromJson(json);
  Map<String, dynamic> toJson() => _$UserToJson(this);
```

And like we mentioned, you will change the `User` part to be the same as your model name.

Lastly run this command:

```shell
flutter pub run build_runner build
```

A new file magically appears in your `models` folder, it's called `user.g.dart` and you can find the generated code there.

You can also do this manually, but for large models with many field, this will save you a lot of time.
