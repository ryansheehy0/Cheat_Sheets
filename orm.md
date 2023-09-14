[Home](./README.md)

# Object Relational Mappings(ORMs)
ORMs are used to interact with relational databases using oop.

## Sequelize
Sequelize can work with multiple different RDBMS so you need to install `mysql2` as well if you are using mysql.

./connection.js file:

```javascript
const Sequelize = require("sequelize")

// Connection provided by JAWSDB_URL which is what Heroku uses
const sequelize = process.env.JAWSDB_URL
  ? new Sequelize(process.env.JAWSDB_URL)
  : new Sequelize(`db_name`, `username`, `password`, {
    host: `localhost`,
    port: 3306,
    dialect: `mysql`
  })


module.exports = sequelize
```

### Syncing
Syncing is connecting to your sql server with sequelize.

In your server file:

```javascript
// Express code
const sequelize = require(`./connection`)
const PORT = 3000

// Connect to the db before running server
sequelize.sync().then(() => {
  app.listen(PORT)
})
```

```javascript
// or you can force true to drop and recreate tables on every sync based upon your modals.
  // DO NOT use this when deploying an app. Your data in your db will be destroyed.
sequelize.sync({force: true}).then(() => {
  app.listen(port)
})
```

### Modals
Modals are JS classes that define a table's schema.

```javascript
const { Model, DataTypes } = require('sequelize')
const sequelize = require('./connection') // Get the connection

class Book extends Model{
  // Instance methods. Functions you can use for specific rows
  isBook() {
    if (this.numberOfPages > 0) { // Does for each row. this refers to the current row
      return true
    }
    return false
  }
}

Book.init(
  { // First object are the columns
    column1: { // If you don't set a primary key sequelize will set one automatically as "id"
      type: DataTypes.INTEGER, // SQL type
      allowNull: false,
      primaryKey: true,
      autoIncrement: true
    },
    email: {
      type: DataTypes.STRING,
      defaultValue: 'test@gmail.com',
      validate: {
        isEmail: true
      }
    },
    numberOfPages: {
      type: DataTypes.INTEGER,
      allowNull: false
    },
    foreign_id: {
      type: DataTypes.INTEGER,
      references: { // This doesn't automatically create a foreign key reference. You have to use association functions.
        modal: 'foreign_modal',
        key: 'id'
      }
    }
  },
  {
    hooks: {
      // Put your hook functions here
    },
    sequelize, // Link to db
    timestamps: false, // Don't set timeouts
    underscore: true, // Converts Camel case to snake case when putting it in the db
    modelName: `book` // table name
  }
)

module.exports = Book
```

OR

```javascript
const { DataTypes } = require('sequelize')
const sequelize = require('./connection') // Get the connection

const ModalName = sequelize.define('modal_name', {
  id: {
    type: DataTypes.INTEGER,
    allowNull: false,
    primaryKey: true,
    autoIncrement: true
  }
})
```

```javascript
// In the server code add
const Book = require(`./Book`) // This invokes the init method and thus connect to sequelize.
```

### Associations
When using references within a modal you have to use a function to define that reference. These functions define relationships between models.

Association functions create a new column(or use an already existing column) that is a foreign key reference to another table.

#### Association Functions
- Module1.hasOne(Module2)
  - Creates a foreign key `Module1Id` inside the `Module2` table that references the primary key of the `Module1` table.
  - `Module1Id` has to be unique inside the `Module2` table.
- Module1.hasMany(Module2)
  - Same as hasOne, but doesn't enforce uniqueness.
- Module1.belongsToMany(Module2)
  - Creates a junction table if it doesn't exist and adds the primary keys of both tables to it.
  - Without specifying the through command, belongsToMany creates a junction table with the default name set to `Module1` concatenated to `Module2` with the order being alphabetical.

`has` association functions create the foreign key and the reference.

`belongsTo` association functions also define the reference, but they are mainly just used to allow Sequelize to do additional queries.

Example:

```javascript
// Creating a One-to-One
User.hasOne(Profile, {
  foreignKey: 'user_id', // Optional argument. This is changing the name from 'UserId' to 'user_id'.
  onDelete: 'CASCADE' // When we delete a User, it also deletes the associated link. In this case it would be the user_id in profile
})
Profile.belongsTo(User, {
  foreignKey: 'user_id' // This has to be the same as the previous foreignKey or else you create a new foreign key
})

// Creating a One-to-Many/Many-to-One
User.hasMany(Task)
Task.belongsTo(User)

// Creating a Many-to-Many relationship
Students.belongsToMany(Courses, {
  through: 'Enrollments' // Optional argument. Sets the name of the junction table
})
Courses.belongsToMany(Students, {
  through: 'Enrollments'
})

  // If you have already created a junction table you can set it to the through argument
  const junction = require("./junction")

  Students.belongsToMany(Courses, {
    through: junction,
    foreignKey: 'student_id', // For Students
    otherKey: 'course_id', // For Courses
  })
  Courses.belongsToMany(Students, {
    through: junction,
    foreignKey: 'course_id', // For Courses
    otherKey: 'student_id', // For Students
  })
```

### Seeding data
Seeding data is putting data into the database.

```javascript
const Book = require(`./book`)

// Creating a new row
Book.create({
  column1: `column1`,
  column2: `column2`
})

// Creating multiple new rows
Book.bulkCreate([
  {
    column1: `column1`,
    column2: `column2`
  },
  {
    column1: `column1`,
    column2: `column2`
  }
])
```

### Querying data

| Function Name      | Description                                                         |
|--------------------|---------------------------------------------------------------------|
| .findAll()         | Finds all rows that match the arguments.                            |
| .findOne()         | Finds the first row that matches the argument.                      |
| .findByPk(id)      | Gets a row by its primary key                                       |
| .findOrCreate()    | Finds the first row and if it couldn't find it it creates one.      |
| .findAndCountAll() | Finds all rows and the count of all the rows found.                 |
| .count()           | Counts the number of rows that match the arguments.                 |
| .max(field)        | Finds the max value of the field in the table.                      |
| .min(field)        | Finds the min value of the field in the table.                      |
| .sum(field)        | Calculates the sum of values of the field in the table.             |
| .aggregate()       | Performs aggregate functions like SUM, COUNT, AVG, etc.             |
| .group()           | Groups rows based on the arguments.                                 |
| .distinct()        | Gets a unique rows based on the arguments.                          |
| .raw()             | Runs a raw SQL query and returns the results as a Sequelize models. |

- You can use `.get({plain: true})` to convert a sequelize object into a JS object.

Example:

```javascript
const dishData = await Dish.findAll()
cost dishes = dishData.map(dish => dish.get({plain: true}))
```

#### Arguments Querying Functions

| Argument   | Description                                                                          |
|------------|--------------------------------------------------------------------------------------|
| attributes | An array of field names to specify the columns to include.                           |
| where      | An object of conditions that rows must meet to be included.                          |
| order      | An arrays of arrays specifying the order in which to sort results.                   |
| group      | Array of arrays to group results by. `[['column to sort', ASC or DESC]]`             |
| limit      | Int specifying the max number of results that can be returned.                       |
| offset     | Int specifying the number of records to skip before starting to get the results.     |
| distinct   | Bool or array of column names and if true ensures that the result have to be unique. |
| having     | Where for using the group arg                                                        |
| raw        | Bool that allows raw SQL queries.                                                    |


Example:

```javascript
Book.findAll(
  include: [
    {
      model: linkedModel,
      through: junctionModel,
      where: {
        id: 1
      }
    },
    {model: secondLinkedModel}
  ]
)
.then(data => console.log(data))
.catch(error => console.error(error))
```

#### Create Update and Destroy

```javascript
Book.create({
  column1: "value"
})
.then(data => console.log(data.dataValues))
.catch(error => console.error(error))
```

```javascript
Book.update(
  {
    column1: "new value"
  },
  {
    where: {
      id: 10
    }
  }
)
.catch(error => console.error(error))
```

```javascript
Book.destroy({
  where: {
    id: 10
  }
})
.catch(error => console.error(error))
```

#### Hooks
Used to filter data before some modification to the database.

The hook is used when creating your schema.

```javascript
hooks: {
  beforeCreate: (data) => {
    data = data.toLowercase()
    return newData
  },
  beforeUpdate: (data) => {
    if(data.changed("attribute")){
      data.attribute = attribute.toLowercase()
    }
    return data
  }
}
```

If you are using bulk commands like `bulkCreate`, `update`, etc you have to set the property `individualHooks = true`


## Sessions
Storing sessions in a database. This is useful if you need to restart you server, but you don't want to loose your session information.

```javascript
const SequelizeStore = require("connect-session-sequelize")(session.store)

app.use(session({
  secret: 'Super secret secret',
  cookie: {
    // Stored in milliseconds
    maxAge: 24 * 60 * 60 * 1000, // expires after 1 day
  },
  resave: false,
  saveUninitialized: true,
  store: new SequelizeStore({
    db: sequelize,
  }),
}))
```