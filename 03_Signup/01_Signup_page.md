Let's create a simple page with two fields, one for the password and one for the username:

In your `pages` folder, create a `signup_page.dart`.

```dart
class SignupPage extends StatelessWidget {
  SignupPage({Key? key}) : super(key: key);
  final usernameController = TextEditingController();
  final passwordController = TextEditingController();
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Sign up"),
      ),
      resizeToAvoidBottomInset: false,
      body: Padding(
        padding: const EdgeInsets.all(20.0),
        child: Column(
          children: [
            const Text("Sign Up"),
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
              child: const Text("Sign Up"),
            )
          ],
        ),
      ),
    );
  }
}
```

Let's add this page to our list of routes in `main.dart`:

```dart
      GoRoute(
        path: '/signup',
        builder: (context, state) => SignupPage(),
      ),
```
