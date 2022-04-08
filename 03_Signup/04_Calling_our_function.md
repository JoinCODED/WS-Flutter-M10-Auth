In your `signup` page submit button, call the signup function from our `auth` provider:

```dart
    ElevatedButton(
        onPressed: () {
            Provider.of<AuthProvider>(context, listen: false).signup(
            user: User(
            username: usernameController.text,
            password: passwordController.text));
        },
        child: const Text("Sign Up"),
    )
```

We called our function and passed the controllers value, can you see the token printed in your console?
