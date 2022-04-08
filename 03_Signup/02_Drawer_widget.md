Let's introduce a new cool widget, called the `Drawer` widget.

In your `home_page.dart` as a `Scaffold` property, add a `Drawer`:

```dart
return Scaffold(
      appBar: AppBar(
        title: const Text("Book Store"),
      ),
      drawer: Drawer()
[...]
```

The `Drawer` widget takes a `child`, and we will use a `ListView` widget and add 2 `ListTile`s inside it, one to take us to the `signin` page and one for the `signup` page.

```dart
ListView(
                    padding: EdgeInsets.zero,
                    children: [
                      ListTile(
                        title: const Text("Signin"),
                        trailing: const Icon(Icons.login),
                        onTap: () {},
                      ),
                      ListTile(
                        title: const Text("Signup"),
                        trailing: const Icon(Icons.how_to_reg),
                        onTap: () {},
                      )
                    ],
                  )
```

Let's add a `DrawerHeader` widget and link the `signup` button to our `signup` page:

```dart
const DrawerHeader(
            child: Text("Sign in please"),
            decoration: BoxDecoration(
            color: Colors.blue,
            ),
        ,
```

```dart
    ListTile(
            title: const Text("Signup"),
            trailing: const Icon(Icons.how_to_reg),
            onTap: () {
                GoRouter.of(context).push('/signup');
            },
        )
```
