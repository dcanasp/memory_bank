#todo

## Access token vs refresh token
son para el refresh de las sesiones, el de acceso dura 10 minutos, y el de refresh dura mas


# finish session
you can have something like redis that will store all the tokens that the user has logged out from, And the expiration date of the redis field will be the same as the token, so if a user send a request, you first check if the token is on the redis DB, if not you let it pass