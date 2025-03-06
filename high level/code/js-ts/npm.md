npm, short for Node Package Manager,  is the world's largest software registry, used primarily with the language [[Javascript]] or [[Node.js]]. It allows users to install, share, and manage package dependencies in their Node.js projects. It simplifies the process of managing dependencies by allowing you to easily install, update, and remove packages from your project. Beyond its core functionality, npm offers various functionalities that enhance the development experience.

alternatives to npm are
- yarn
- pnpm
- [[bun]]

## **Ways to Use npm:**

- **Initializing a New Project:** `npm init` steps through creating a `package.json` file for a new project, which lists metadata and dependencies.
- **Installing Packages:** 
	- Locally: `npm install <package_name>` installs a package within a project.
	- Globally: `npm install -g <package_name>` installs a package globally, making it accessible across all projects on your machine. (don't do)
	- install all: `npm i` installs all in a `package.json`
These packages are installed from the [npm registry](https://www.npmjs.com/)
- **Adding Dependencies:** Specify packages as dependencies in your `package.json` file for automatic installation and management.
- **Updating Packages**: `npm update` updates all packages in a project according to the specified version ranges in `package.json`.
- **Managing Versions:** Specify specific versions of packages in your `package.json` or use flags like `~` or `^` for semantic versioning.
- **Running Scripts:** Define custom scripts in your `package.json` and run them with `npm run <script-name>`.
- **Publishing Packages:** Share your own code with the community by publishing your package to the [npm registry](https://www.npmjs.com/)
- **execute packages:** sometimes you just want to execute a package, for this you use **npx**, an example with prisma is: `npx prisma generate`. this will execute that prisma command and do whatever it must. npx is the same as executing inside a running node (write `node` on the command line to understand) 

## **Most Common Packages:**
###### web frameworks
- **Express**: Web framework for building web applications.
- **[[Fastify]]**: Web framework, faster and more resilience
- **Koa**: Web framework with a smaller footprint and more flexibility.
- **NestJS**: uses express or fastify under the hood
- **Hapi**

which is better? [all mentioned vs each other](https://medium.com/deno-the-complete-reference/express-vs-fastify-vs-hapi-vs-koa-hello-world-performance-comparison-dd8cd6866bdd), common sentimment is that fastify is better. At the end i will append why express is somewhat bad
###### for web frameworks
- **body-parser**: if you want to use req.body (always use)
- **cors**: if you want to enable the [[CORS]] (Cross-Origin Resource Sharing)
- **jsonwebtoken**: if you are going to use a [[JWT]] token
- **helmet**: helps secure Express apps by setting various HTTP headers
- **passport**: simplifies authentication 
###### [[ORM]]s ~
- **[[Prisma]]:**  Easiest to use, used by me on [[Trunews]]
- **[[Sequelize]]** 
- **TypeORM**
- **Mongoose:** [[ORM|ODM]] (Object-Document Mapper) for MongoDB database interaction.
- **[[GraphQL]]:* Way to communicate using GrapQl
###### Really usefull
- **[[typescript]]**: read the article, the superset that should always be used
- **PM2:** make a node application always available and turned on (creates a [[daemon]])
- **Socket.io:** Enables real-time communication between clients and servers using [[WebSocket]].
- **Lodash:** Utility library with various functions for manipulating data.
-  **Moment.js:** JavaScript library for working with dates and times.
- **sharp:** To modify, resize and do anything with images
- **Argon2:** my go to library for [[hash]]ing
- **dotenv**: to load .env files into `process.env`. Since node `20.6.0` this is included on node itself
- **morgan**: for logging and creating loggers
- **winston**: for creating loggers and logging
- **nodemon**: Restarts and re runs the aplication each time you save
- **ts-node-dev**: same as nodemon but smaller and faster, i prefer it
- **ts-node**: to compile typescript without building
###### Bundlers
Want a server? bundle it. always used on front end
- **Parcel:** The easiest
- **Webpack:**
- **Vite:**
###### Testing
testing is always annoying, nothing more to add
- **Jest:** The best...
- **Mocha:** JavaScript testing framework.
- **Chai:** Assertion library for testing frameworks.

## how it works

`npm init` will create a `package.json`, that has metadata of the project, and 3 relevant parts for functioning, the **scripts**, where you set up custom scripts so you don't have to write the execute the code each time, the **dependencies**, that are the dependencies that make your project run, you can install these with `npm install --omit=dev`, these are the now ways, but you could also do it with `npm install --production`. The final part is **devDependencies**, this are the dependencies that you use when you are developing, for example, typescript, code lints, types for typescript, you install this only with `npm install --include=dev`. that is the new way, the old `npm install --dev`

Why doing this? a great example is [[docker]], you want to optimize the container, so you can create a layer where you only install the production dependencies, copying the pre transpiled code and installing only what you trully need

**The Functioning of npm Cache:**

npm caches downloaded packages locally to avoid repeated downloads. This helps to improve the speed of `npm install` commands and reduce the bandwidth usage.

**Cache Location:**

The default location of the npm cache on your system depends on your operating system:

- **Windows:** `%APPDATA%\npm-cache`
- **Mac:** `~/Library/Caches/npm`
- **Linux:** `~/.npm`

**Cache Management:**

You can manage your npm cache through various commands:

- `npm cache clean`: Clears the entire npm cache.
- `npm cache verify`: Verifies the integrity of the cached packages.
- `npm cache ls`: Lists the contents of the npm cache.

**Considerations:**

- The npm cache can become large over time, especially when installing many packages.
- You can configure the maximum size of the cache or specify a different location using the `--cache` option.
- Regularly clearing the cache can be helpful to reclaim disk space and ensure you have the latest versions of packages.


## Extra

why is express bad?

firstly look at the benchmarks, second

```markdown
Express obviously is **popular**, has lot's of stars on github, but if you work with it long enough you'll understand that actually it sucks. It's middleware approach is easy to understand, however if you look under the hood, you'll realize that **your app** written on express will **slowdown** with **every new route or middleware you add**. Express router uses regular expressions and in worst case **scans all routes to find one that needed**. So if you have more than 20-50 routes, your app will be very slow comparing to others.  
Koa is more modern framework. And it's developers learned on express mistakes, so it's better. Also it doesn't contain built-in router, so you have a choice and you may write your own router and plug it without any difficulties.  
**Fastify** - is also quiet modern. It also supports express-like middleware, but it's not recommended to use them, because it will be probably deprecated in v3. Also it has much better router then express. But the thing what I really like in it - it's schemas and validation. So it's doing validation out of the box, and it's much easier to write generate swagger docs or something similar without any additional stuff like comments, etc.
```
This is a old comment, but some of it's points still remain true. Express has terrible problems with their middleware structure, they have a infinite stack of middleware that you have to go through each time your request enters, this makes your app slow (unlike fastify plugins, that only execute on their hook)

on the benchmarks is worse than fastify


two benchmarks examples
first **time per test** 
![[FastifyTimePerTest.png]]
and then **request per second**
![[FastifyRequestPersecond.png]]