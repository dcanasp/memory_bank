#typescript 
:SiSequelize: An [[orm]] not as easy as prisma, with more control. Sequelize needs models to work (like every orm), but these models are more **strict**. is a traditional ORM which maps _tables_ to _model classes_. 

If you want a reliable ORM this is better than [[Prisma]] . But on personal opinion (currently i'm not sure on world)
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

on the `models` folder you have by default a `index.js`. this folder manages the models in which your database runs, so it always returns that type of object

on the `seeders` folder you create test data to seed your database. a starting point is `npx sequelize-cli seed:generate --name users ` and to seed you just `npx sequelize-cli db:seed:all` 

The default files use the library `path`,`process` and `fs` so (i never use the default file)

>[!Pro tip]
> You don't have to create the models by hand, create your tables in normal sql (is better this way)
> Then install `npm install -D sequelize-auto`
> and auto generate the models (the -l ts part is to generate them on typescript)
> `npx sequelize-auto -l ts -o models -d [DATABASE_NAME] -u [DATABASE_USER] -x [DATABASE_PASSWORD] -h [DATABASE_HOST] -p [DATABASE_PORT] -e [DATABSE_DIALECT]`
> **"DISCLAIMER"** this is somewhat insecure and the package is old, if you want total safety, create the tables by hand, and latter create the models by hand aswel!
> A safe alternative is to use the cli
> `npx sequelize-cli model:generate --name User --attributes firstName:string,lastName:string,email:string`




After having your models. you must setup the database. You create the connection, and **initialize the models**
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

## queries

##### select:
After this is done. you can query sequelize (first you connect to the database!!). This is simple, you just import the models and `const testData = await test.findAll();`. with this you get a weird format (the one you defined on the model). but at the end of the day, is and array of metadata and your values, to access a specific value you can `testData[0].dataValues`, Those are the values in a object. finally you just do `testData[0].dataValues.id` or whatever you want to check. If you want all of the data in a good format, you do a map. `const rowValues = testData.map(data => data.dataValues);`.
There is another way to retrieve only the values. that's doing `const testData = await test.findAll({raw:true});` .

##### insert
you do a `User.create`

##### update

this is funnier, what you need first is having an instance of the created user, it can be with a find or a insert. so for example you do a `const user = await users.findOne({where: { username: username }});` and then you modify that user object on the keys that you want to update. For example `user.email = 'new@email'` and then you **save** `await user.save();`. Sequelize automatically finds what was modified and changes only that, but you can say `user.changed('email', true);` to tell Sequelize that there was a change on that parameter. this is great but has one **MAJOR FLAW**; *silent failure* if any of the new values are `undefined`

If any of the variables (that you are going to update) are `undefined`, Sequelize will not throw an error. Instead, it will silently ignore the update for that field. This behavior can be misleading because it gives the impression that the update was successful when, in fact, some fields may not have been updated at all. To avoid this, don't trust sequelize only, and if needed do it by hand, create an object like this `const updates:Partial<typeof user.dataValues> = {};`  change the values from the updates code, and finally do `user.update(updates);`



- `User.sync()` - This creates the table if it doesn't exist (and does nothing if it already exists)
- `User.sync({ force: true })` - This creates the table, dropping it first if it already existed
- `User.sync({ alter: true })` - This checks what is the current state of the table in the database (which columns it has, what are their data types, etc), and then performs the necessary changes in the table to make it match the model.


## migrations

run `npx sequelize-cli db:migrate` after creating a .js file in your migrations in this format:
```js
'use strict';
module.exports = {
  async up (queryInterface, Sequelize) {
    await queryInterface.addColumn('videos', 'uuid', {
      type: Sequelize.UUID,
      allowNull: false,
      unique: true
    });
  },
  async down (queryInterface, Sequelize) {
    await queryInterface.removeColumn('videos', 'uuid');
  }

};
```


# Personal review
queries are fine, but that migration and model system is simply not worth it, 