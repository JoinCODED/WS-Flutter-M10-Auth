The remaining function to do is the signout function.

27. In the auth provider, add the following function:

```dart
  void logout() {
    token = "";
    notifyListeners();
  }
```

28. Call the `logout` function in the `Drawer` button:

```dart
ListTile(
        title: const Text("Logout"),
        trailing: const Icon(Icons.logout),
        onTap: () {
                Provider.of<AuthProvider>(context, listen: false).logout();
                },
    ),
```

29. Call the `notifyListeners` in the `signin` and `signup` functions:

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

Test your code. It works, we can signup, in, and out.

Try to refresh your app, you will be signed out 😁. We do not want to force the user to sign in each time the app reloads, it would be nice if we can save the token somewhere in order to keep him/her signed in.
