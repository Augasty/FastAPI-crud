<!-- uvicorn sql_app.main:app --reload -->
# Packages to install
pip install fastapi
pip install uvicorn
pip install sqlalchemy


FastAPI works with any database and any style of library to talk to the database.

A common pattern is to use an "ORM": an "object-relational mapping" library.
Here, in this example we are using SQLAlchemy ORM.

An ORM has tools to convert ("map") between objects in code and database tables ("relations").
With an ORM, you normally create a class that represents a table in a SQL database, each attribute of the class represents a column, with a name and a type.


# __init__.py
The file __init__.py is just an empty file, but it tells Python that sql_app with all its modules (Python files) is a package.



# database.py
SQLALCHEMY_DATABASE_URL = "sqlite:///./sql_app.db"
We are "connecting" to a SQLite database (opening a file with the SQLite database).

Then we create a SQLAlchemy engine.

Then we create a SessionLocal class, each instance of the SessionLocal class will be a database session. The class itself is not a database session yet.
But once we create an instance of the SessionLocal class, this instance will be the actual database session.
(To create the SessionLocal class, use the function sessionmaker)

Now we create a Base class.
Now we will use the function declarative_base() that returns a class.
Later we will inherit from this class to create each of the database models or classes (the ORM models).



# models.py
We will use this Base class we created before to create the SQLAlchemy models.
We are creating User and Item classes which inherit from the Base class, these classes are the SQLAlchemy models.

The __tablename__ attribute tells SQLAlchemy the name of the table to use in the database for each of these models.
Each of these attributes in  the model (class) represents a column in its corresponding database table.

Now create the relationships.
For this, we use relationship provided by SQLAlchemy ORM.
This will become, more or less, a "magic" attribute that will contain the values from other tables related to this one.



# schemas.py
We will create the pydantic models here.

Create an ItemBase and UserBase Pydantic models (or let's say "schemas") to have common attributes while creating or reading data.
And create an ItemCreate and UserCreate that inherit from them (so they will have the same attributes), plus any additional data (attributes) needed for creation.
So, the user will also have a password when creating it.
But for security, the password won't be in other Pydantic models, for example, it won't be sent from the API when reading a user.

Now create Pydantic models (schemas) that will be used when reading data, when returning it from the API.
For example, before creating an item, we don't know what will be the ID assigned to it, but when reading it (when returning it from the API) we will already know its ID.
The same way, when reading a user, we can now declare that items will contain the items that belong to this user.

Now, in the Pydantic models for reading, Item and User, add an internal Config class.
This Config class is used to provide configurations to Pydantic.
In the Config class, set the attribute orm_mode = True.

Pydantic's orm_mode will tell the Pydantic model to read the data even if it is not a dict, but an ORM model (or any other arbitrary object with attributes).

This way, instead of only trying to get the id value from a dict, as in:
This way, instead of only trying to get the id value from a dict, as in:
<div>id = data["id"]</div>

it will also try to get it from an attribute, as in:
<div> id = data.id </div>