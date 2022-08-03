Let's introduce a new cool widget, called the `Drawer` widget.

15. In the `home_page.dart`, add a `drawer` as a `Scaffold` widget property:

```dart
return Scaffold(
      appBar: AppBar(
        title: const Text("Book Store"),
      ),
      drawer: Drawer()
[...]
```

**Note:** A `drawer` can be any widget, but it is often best to use the `Drawer` widget from the material library, which adheres to the Material Design spec.

The `Drawer` widget takes a `child` named argument, and in our case, we will use a `ListView` widget and add two `ListTile`s inside it, one to take us to the `signin` page and the other to take us to the `signup` page.

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

16. Add a `DrawerHeader` widget and link the `signup` button to the `signup` page:

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
