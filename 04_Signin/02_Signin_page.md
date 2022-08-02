20. In your `pages` folder, create a signin page:

```dart
class SigninPage extends StatelessWidget {
  SigninPage({Key? key}) : super(key: key);
  final usernameController = TextEditingController();
  final passwordController = TextEditingController();
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Sign in"),
      ),
      resizeToAvoidBottomInset: false,
      body: Padding(
        padding: const EdgeInsets.all(20.0),
        child: Column(
          children: [
            const Text("Sign In"),
            TextField(
              decoration: const InputDecoration(hintText: 'Username'),
              controller: usernameController,
            ),
            TextField(
              decoration: const InputDecoration(hintText: 'Password'),
              controller: passwordController,
              obscureText: true,
            ),
            ElevatedButton(
              onPressed: () {},
              child: const Text("Sign In"),
            )
          ],
        ),
      ),
    );
  }
}
```

21. Pass the `signin` function to the `Sign In` button:

```dart
    ElevatedButton(
        onPressed: () {
            Provider.of<AuthProvider>(context, listen: false).signin(
                user: User(
                username: usernameController.text,
                password: passwordController.text));
        },
        child: const Text("Sign In"),
    )
```

22. Include `SigninPage` page in the routes in `main.dart`:

```dart
      GoRoute(
        path: '/signin',
        builder: (context, state) => SigninPage(),
      ),
```

23. Navigate the user to the `/signin` page when he/she clicks the `signin` button in the drawer:

```dart
ListTile(
    title: const Text("Signin"),
    trailing: const Icon(Icons.login),
        onTap: () {
            GoRouter.of(context).push('/signin');
            },
    ),
```

Test your page, do you see the token printed in the console?
