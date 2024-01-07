#typescript
example made with express, with nest just follow the templates they give you, with koa use a simillar one
## folder structure
``` bash
├───.github
│   └───workflows
├───logs
├───[ORM Models]
├───migrations
├───src
│   ├───auth
│   ├───aws
|   ├───db
│   ├───dto
│   ├───errors
│   ├───middleware
│   ├───public
│   ├───routes
│   ├───test
│   ├───user (as many folders as this for your routes controllers and services)
│   └───utils
├───sslCertificates
```
![[FolderStructureTypescript.png]]

## Express setup
**app.ts**
```typescript
export class App  {
  private app: Express;
  constructor() {
    this.app = express();
    this.app.use(express.json({limit: '10mb'}));
    this.app.use(cors());
    this.app.use(helmet());
    this.app.use( rateLimiter );
    this.app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerDocument));
    loggerMiddleware()
    this.app.use(routes);//importa index por default
  }
  public listen(port: number) {
    this.app.listen(port, () => {
      console.log(`Server running on port ${port}`);
    });
    return this.app
  }
}
const app = new App();
const appInstance = app.listen(+process.env.PORT! || 3006);
export default appInstance;
```

**routes/index.ts**
```typescript
export const routes = Router();
routes.use('/articles', articleRouter.routes())
routes.use('/users', userRouter.routes());
routes.use('/communities', communityRouter.routes())
```
**routes/user.routes.ts**
```typescript
export class UserRouter {
    private router: Router;
    constructor(){
        this.router = Router();
    }
    public routes(){
       this.router.get('/route',(req:Request, res:Response) => Controller.function(req, res));
        //all routes here
        
		return this.router
	}

}
```

## fastify setup with JWT 

```typescript
App.fastifyInstance = Fastify({ 
	logger: false
});
//register plugins
App.fastifyInstance.register(jwt, {
	secret: jwt_secret,
	sign: {
		expiresIn: '72h'
	}
	
});
App.fastifyInstance.register(fastifyMultipart, {
	attachFieldsToBody: true,
  });	
App.fastifyInstance.decorate("authenticate", async function(request, reply) {
	try {
	  await request.jwtVerify()
	} catch (err) {
	  reply.send(err)
		}
})
```