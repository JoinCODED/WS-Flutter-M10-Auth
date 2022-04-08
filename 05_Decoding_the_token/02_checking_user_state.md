Now let's move to our `Drawer` widget, and have a condition there, if the user is authenticated, we will show a welcome message in the header and a logout button.

In your `home_page.dart` `Drawer` widget, wrap the `ListView` in a consumer widget:

```dart
 drawer: Drawer(
        child: Consumer<AuthProvider>(
            builder: (context, authProvider, child) => authProvider.isAuth
                ? ListView(
                    padding: EdgeInsets.zero,
                    children: [
                      DrawerHeader(
                        child: Text("Welcome ${authProvider.user.username}"),
                        decoration: const BoxDecoration(
                          color: Colors.blue,
                        ),
                      ),
                      ListTile(
                        title: const Text("Logout"),
                        trailing: const Icon(Icons.logout),
                        onTap: () {},
                      ),
                    ],
                  )
                : ListView(
                    padding: EdgeInsets.zero,
                    children: [
                      const DrawerHeader(
                        child: Text("Sign in please"),
                        decoration: BoxDecoration(
                          color: Colors.blue,
                        ),
                      ),
                      ListTile(
                        title: const Text("Signin"),
                        trailing: const Icon(Icons.login),
                        onTap: () {
                          GoRouter.of(context).push('/signin');
                        },
                      ),
                      ListTile(
                        title: const Text("Signup"),
                        trailing: const Icon(Icons.how_to_reg),
                        onTap: () {
                          GoRouter.of(context).push('/signup');
                        },
                      )
                    ],
                  ),
                ),
      ),
```
