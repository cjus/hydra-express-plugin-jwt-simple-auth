# hydra-express-plugin-jwt-simple-auth

## Prior work

This Repo is based the excellent work of Eric Adum on [https://github.com/flywheelsports/hydra-express-plugin-jwt-auth](https://github.com/flywheelsports/hydra-express-plugin-jwt-auth). That plugin is currently tightly coupled with the use of [https://github.com/flywheelsports/fwsp-jwt-auth](https://github.com/flywheelsports/fwsp-jwt-auth) which is why this repo exists. It's also envisioned that the fwsp-jwt-auth repo may grow to be Flywheel Sports specific. The use of jwt-simple-auth is designed to remain neutral and community driven.

## Summary

Uses the [jwt-simple-auth](http://github.com/flywheelsports/jwt-simple-auth) module to decode and validate JWT tokens.

There should be a root-level `jwtPublicCert` entry in the service config with the path to the public key file.

This plugin does not require a config entry in the `hydra.plugins` section.

Express middleware `hydraExpress.validateJwtToken()` decodes valid, unexpired auth tokens into `req.authToken`, or returns a 401 response otherwise.

These tokens should be in the `authorization` header of the request, as described [here](https://jwt.io/introduction/).

## Usage

```javascript
const hydraExpress = require('hydra-express');
const JWTAuthPlugin = require('hydra-express-plugin-jwt-simple-auth');
hydraExpress.use(new JWTAuthPlugin());

api.get('/needsLogin', hydraExpress.validateJwtToken(), (req, res) => {
  res.json({decodedToken: req.authToken});
});
```
