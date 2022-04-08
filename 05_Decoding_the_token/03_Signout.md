The last function to do is the signout function.

In your auth provider:

```dart
  void logout() {
    token = "";
    notifyListeners();
  }
```

And let's link this function in our `Drawer` button:

```dart
ListTile(
        title: const Text("Logout"),
        trailing: const Icon(Icons.logout),
        onTap: () {
                Provider.of<AuthProvider>(context, listen: false).logout();
                },
    ),
```

Don't forget to call `notifyListeners` in the signin and signup functions:

```dart
  void signup({required User user}) async {
    token = await AuthServices().signup(user: user);
    notifyListeners();
  }

  void signin({required User user}) async {
    token = await AuthServices().signin(user: user);
    notifyListeners();
  }
```

Test your code, it works, we can signup/in and out.

But try to refresh your app, you will be signed out, we don't want the user to have to sign in each time, it would be nice if we can save the token somewhere!
