We need two packages that save us a lot of time and effort.

2. Install those packages:

```
flutter pub add json_serializable
flutter pub add build_runner
```

3. Import `json_serializable` package in the user model file:

```dart
import 'package:json_annotation/json_annotation.dart';
```

You will get the red underline that we all hate, but that is fine, it is because the file doesn't exist. It will be magically generated later on!

```dart
part 'user.g.dart';
```

Notice that the `user` part should always be the name of the file you are in. For example, if we are doing this for the book model, it would be `book.g.dart`.

4. Before the class definition, add the following line:

```dart
@JsonSerializable()
class User {
[...]
```

5. At the end of your class, add the two lines below:

```dart
  factory User.fromJson(Map<String, dynamic> json) => _$UserFromJson(json);
  Map<String, dynamic> toJson() => _$UserToJson(this);
```

As we mentioned, you have to change the `User` part to be the same as your model name.

6. Run the following command:

```shell
flutter pub run build_runner build
```

A new file magically appears in your `models` folder, it is called `user.g.dart` and you can find the generated code there.
If you faced issues running the command above, delete `book.g.dart` and try again, the command will generate them both

You can also do this manually, but for the large models with many fields, this will save you a lot of time.
