# Rate Limiting API

You task is to create a service that exposes a simple REST endpoint:

```
GET /random
```

which will by default return 32 bytes of randomness.

In order to use the API, the requester must supply a `client_id` to the endpoint in a header:

``` 
X-Client-ID: <client_id>
```

Additionally the Client can request a different amount of bytes using the `len` query parameter, for instance the following 
complete request will return 64 bytes of randomness to the client `1`

```
GET /random?len=64
X-Client-ID: 1
Accept: application/json
```

The response should be a base64 encoded string of the randomness in a JSON object, for instance

```
200 OK

{
    "random": "gF1jJH8AMjJbO6PZ9pF6vde0Zc8OShrO4FLSCHeoFC9tGoU/iVu+K5ViKOoQ7HTNRlrjnxG67K/ANPb9Q5p55w=="
}
```

## Rate Limiting
The API must be rate limit by allowing only 1024 bytes of randomness per 10 seconds.

The API must return an appropriate message back to the client if the rate is spent, or if the request would exceed the remaining limit.

If the request can be served, the response must contain a header specifying the remaining rate limit in a header.

```
X-Rate-Limit: <amount left>
```

## Optional extra expansions

1. Extend the API with an Admin endpoint that can reset and change the rate limit for a client
2. Allowing the rate limit to differ between different clients. This could be done through configuration.
3. Authenticate the Client before serving the request.
4. Add a signature to the response JSON object `sig` that is signed using a public / private key pair from the server.

# Your Assignment

Implement the above API in the language you are most comfortable in, however, our preferences are (in prioritized order):

1. Go
2. C# (.NET Core)
3. Rust
4. JavaScript (Node.js)
5. Java

We ask you as a minimum to implement the basic API described above, however we encourage you to pick 1 of the optional extra expansions to do as well. Pick 
one you are comfortable with, they can be harder than they appear.

In your response, please provide:
1. The source code
2. A document descibing
    - Any assumptions or design decision you made
    - How to build, run, and test your API
    - How you are sure the API works as intended

If there is anything that is unclear - that is intentional. Please derive a suitable solution based on your knowledge and the information you have, but be sure to add 
a suitable explanation in your solution to how you handled the uncertainty.

Good luck.