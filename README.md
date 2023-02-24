# Connectulum
**Connectulum** provides advanced connectivity and session management to **Trisolian** hub infrastructure.
​
**Trisol** is a proprietary (and fictional) remote infrastructure domain providing server and application
resources on demand. 
​
## Status
Basic connectivity and cryptographic primitives for the proprietary system are available.
​
## Next Steps / Contributing
Next steps will be around session management -- connecting a user to the Trisolian 
infrastructure securely and maintaining this connection through multiple requests for
resources.
​
## Issues
### Issue 1
Add a `UserSession` type that exposes the ability to authenticate a user's password against an underlying [crypt.Authenticator](pkg/crypt/crypt.go) (line 20).
​
`UserSession` should have a method with the following signature:
​
`func (s *UserSession) Authenticate(username, password string) bool`
​
The new type should be placed in a new `session` package which will be enhanced soon with additional functionality.
​
Remember to add tests via Test-Driven Development.
​
### Issue 2
Enhance the `UserSession` to be able to connect to remote resources.
​
The `Connect` method should check for authentication and then use the [ConnectSophon](pkg/conn/conn.go) (line 17) function to retrieve and store a `SophonicConnection`. If the `UserSession` was not previously authenticated successfully, an error should be returned.
​
`func (s *UserSession) Connect() error`
​
Remember to add tests via Test-Driven Development.
​
​
### Issue 3
Each `UserSession` is expensive to create, primarily because of the cost of establishing a `SophonicConnection`. Add a `UserSessionStore` type to facilitate the reuse of established `UserSessions`.
​
A `UserSessionStore` should allow the creation, retrieval, and deletion of `UserSessions` based upon some unique identifier. We expect the `UserSessionStore` to be used in a critical path of our code, so it is important that it is performant and safe for concurrent use.
​
As always, please include tests via Test-Driven Development.
