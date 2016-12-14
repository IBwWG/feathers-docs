# Token Authentication

The JSON web token (JWT) auth strategy is enabled by default with Feathers authentication. Currently it cannot be disabled because right now session or cookie based authentication is not supported and [token based auth is better](https://auth0.com/blog/2014/01/07/angularjs-authentication-with-cookies-vs-token/).

## Usage

### Server Side

This is what a typical server setup looks like:

```js
app.configure(authentication({
  token: {
    secret: 'my-secret'
  }
}));
```

Normally the only option you might want to pass when registering the `feathers-authentication` module in server side is your token `secret`. That's all.

> **ProTip:** If you don't pass a token `secret` a secure one will be randomly generated for you each time your app starts.

#### Token Service Specific Options

All of the top level authentication options are passed to the token authentication service. If you need to customize your token specific configuration further you can use these options:

- `secret` (**required**) (default: a strong auto generated one) - Your secret used to sign JWT's. If this gets compromised you need to rotate it immediately!
- `payload` (default: '[]') [optional] - An array of fields from your user object that should be included in the JWT payload.
- `passwordField` (default: 'password') [optional] - The database field containing the password on the user service.
- `issuer` (default: 'feathers') [optional] - The JWT issuer field
- `algorithm` (default: 'HS256') [optional] - The accepted JWT hash algorithm
- `expiresIn` (default: '1d') [optional] - The time a token is valid for

You can view additional available JWT signing options in the [node-jsonwebtoken](https://github.com/auth0/node-jsonwebtoken) repo.

> **ProTip:** JWT payloads can be decoded on the client. Do not store sensitive information in the JWT payload. If you must then it should be encrypted before the JWT is signed in the token service using your secret.

### Client Side

#### Using Feathers Client

The Feathers authentication module has a client side component that makes it very easy for you to add authentication to your app. It can be used in the browser, NodeJS and React Native. Refer to the [feathers client authentication section](./client.md) for more detail.

#### Other Clients

Of course, if you don't want to use the feathers authentication client you can also just use vanilla sockets or ajax. It's a bit more work but honestly, not much more. We have some examples [here](https://github.com/feathersjs/feathers-demos/tree/master/examples).
