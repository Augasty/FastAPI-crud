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