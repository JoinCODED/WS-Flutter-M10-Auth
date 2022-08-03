There are many ways and flows to do authentication, we will use `JWT` tokens to authenticate our users, but what are `JWT` tokens?

`JWT`, or JSON Web Token, is an open standard used to share security information between two parties — a client and a server. Each JWT contains encoded JSON objects, including a set of claims. JWTs are signed using a cryptographic algorithm to ensure that the claims cannot be altered after the token is issued.

A `JWT` is a string made up of three parts, separated by dots (.), and serialized using base64. In the most common serialization format, compact serialization, the JWT looks something like this: xxxxx.yyyyy.zzzzz.

Once decoded, you will get those values as follows:

- Id
- Expiration Time
- Username

The expiration time is a security mechanism. If the token is expired, the server will throw a `401` error and will refuse to process the request.

Here's an example of a `JWT`:

```
eyJhbGciOiJIUzI1NiJ9.eyJpZCI6MSwidXNlcm5hbWUiOiJ0ZXN0IiwiZXhwIjoxNjQ5NDMwMDc5MzIyfQ.A33Yo9LYrVxiYT0okDnBnRWDWL-CrGCrZAl8D0-3ZRc
```

And you can use this [website](https://jwt.io/) and paste the token to decode and see the values.
