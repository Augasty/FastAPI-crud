<!-- uvicorn sql_app.main:app --reload -->
FastAPI works with any database and any style of library to talk to the database.

A common pattern is to use an "ORM": an "object-relational mapping" library.
Here, in this example we are using SQLAlchemy ORM.

An ORM has tools to convert ("map") between objects in code and database tables ("relations").
With an ORM, you normally create a class that represents a table in a SQL database, each attribute of the class represents a column, with a name and a type.


#__init__.py
The file __init__.py is just an empty file, but it tells Python that sql_app with all its modules (Python files) is a package.

