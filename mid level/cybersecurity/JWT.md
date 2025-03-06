#todo

## Access token vs refresh token
son para el refresh de las sesiones, el de acceso dura 10 minutos, y el de refresh dura mas


## Why they are not secure
problems with libraries and vulnerabilities, as every type of signing is allowed some of them are vulnerable, but jwt still allows them, also is you use a asymetric encryption like [[RSA]] some atacks change the header, saying that they use a symetric algorithm and sign it with the public RSA key, that way overiding the jwt security

in short. jwt is not bad, but there is a lack of regularized implementations
[[paseto]]
# finish session
you can have something like redis that will store all the tokens that the user has logged out from, And the expiration date of the redis field will be the same as the token, so if a user send a request, you first check if the token is on the redis DB, if not you let it pass