#typescript
## why fastify?
Fastify is a modern web Framework, it's the fastest web Framework, it's the most customisable with it's plugins. it's the best on the benchmarks. (unlike express.js that is the worst on all)

The core of Fastify is (speed) their **_plugins_**, **_decorators_** and **_hooks_**. You can use their plugins, or you can create your own, some notable **plugins**, are `@fastify/mongodb`, that will help you create the whole connection to mongo fully integrated on fastify. You also have aut, [[JWT]], postgrest, ratelimiters, websockets, or anything you can think of.

Also, if you have a very specific problem, create your own *plugin*, that is your own code, that you register as a plugin, give it a *hook* (execute onSend, preParsing...), and now you have a way to solve any specific problem (eg. creating a mark of the web on each file that you return to the client). Finally and really important, you can create plugins that only apply to specific scopes, making your app as light as you want

Another important part is their schemas, you don't have to, but doing them helps with serialization and documenting. When you create a schema fastify will serialize and give your route a speed up of via a `factor of 2-3`. Also documenting makes understanding and developing easer on larger teams, these are very similar to [[swagger]] schemas. Making it that you have **complete control** over your app


## basics

to maintain code integrity, always use the *register API*, you instance the app and register the routes handlers
```typescript
import Fastify from 'fastify'
import {userRoutes} from './routes/users'
const fastify = Fastify({
  logger: true
})
fastify.register(userRoutes,{prefix:"/user"}) //this is the register
fastify.listen({ port: 3000 }, function (err, address) {
  if (err) {
    fastify.log.error(err)
    process.exit(1)
  }
})
```