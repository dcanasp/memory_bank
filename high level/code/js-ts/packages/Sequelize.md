:SiSequelize: An [[orm]] not as easy as prisma, with more control. Sequelize needs models to work (like every orm), but these models are more **strict**. is a traditional ORM which maps _tables_ to _model classes_. 

If you want a reliable ORM this is better than [[Prisma]] . But on personal opinion, instead of sequelize i prefer raw [[sql]] with something like [[sqlx]] 
### initial config

```shell
npm i sequelize
npm i -D sequelize-cli
npx sequelize init
```

with that you created 4 folders,
`config`, `migrations`,`models`, `seeders` 

on the folder `config`, you have a file `config.json`
on `config.json` there will be 3 databases by default, **development**, **test** and **production**. give the credentials to the ones you want; "dialect" means the database that you will use

on the `models` folder you have by default a `index.js`. this folder manages the ..... ^c1b591

The default files use the library `path`,`process` and `fs` so install those

>[!Pro tip]
> You don't have to create the models by hand, create your tables in normal sql (is better this way)
> Then install `npm install -D sequelize-auto`
> and auto generate the models (the -l ts part is to generate them on typescript)
> `npx sequelize-auto -l ts -o models -d [DATABASE_NAME] -u [DATABASE_USER] -x [DATABASE_PASSWORD] -h [DATABASE_HOST] -p [DATABASE_PORT] -e [DATABSE_DIALECT]`
> **"DISCLAIMER"** this is somewhat insecure and the package is old, if you want total safety, create the tables by hand, and latter create the models by hand aswel!
> A safe alternative is to use the cli
> `npx sequelize-cli model:generate --name User --attributes firstName:string,lastName:string,email:string`




After having your models. you must setup the database. You create the connection, and initialize the models
```
Full example of configuration of sequelize on typescript
```
```typescript 
import {Sequelize} from 'sequelize';
import {test} from '../../models/test';

export class Database {
    private sequelize: Sequelize;
    constructor() {
      this.sequelize = new Sequelize({
        dialect: 'postgres',
        host: 'localhost',
        port: 5432,
        username: 'postgres',
        password: 'Colegio5',
        database: 'ytClone',
      });
    }
    public async connect() {
      try {
        await this.sequelize.authenticate();
        console.log('Connection has been established successfully.');
        //ALL MODELS GO HERE
        test.initModel(this.sequelize);
      } catch (error) {
        console.error('Unable to connect to the database:', error);
      }
    }
    public async close() {
      await this.sequelize.close();
    }
  }
```

After this is done. you can query sequelize (first you connect to the database!!). This is simple, you just import the models and `const testData = await test.findAll();`. with this you get a weird format (the one you defined on the model). but at the end of the day, is and array of metadata and your values, to access a specific value you can `testData[0].dataValues`, Those are the values in a object. finally you just do `testData[0].dataValues.id` or whatever you want to check. If you want all of the data in a good format, you do a map. `const rowValues = testData.map(data => data.dataValues);`.
There is another way to retrieve only the values. that's doing `const testData = await test.findAll({raw:true});` .

**Not sure why to use sequelize**, [[sqlx]] seems better



- `User.sync()` - This creates the table if it doesn't exist (and does nothing if it already exists)
- `User.sync({ force: true })` - This creates the table, dropping it first if it already existed
- `User.sync({ alter: true })` - This checks what is the current state of the table in the database (which columns it has, what are their data types, etc), and then performs the necessary changes in the table to make it match the model.