# 0x03. User authentication service

## Tasks :page_with_curl:
* **0. User Model**
* [user.py](./user.py): In this task you will create a SQLAlchemy model named User for a database table named users (by using the mapping declaration of SQLAlchemy).
The model will have the following attributes:
id, the integer primary key
email, a non-nullable string
hashed_password, a non-nullable string
session_id, a nullable string
reset_token, a nullable string

* **1. create user**
* [db.py](./db.py): In this task, you will complete the DB class provided below to implement the add_user method.
  
  ```
"""DB module
"""
from sqlalchemy import create_engine
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker
from sqlalchemy.orm.session import Session

from user import Base
class DB:
    """DB class
    """
    def __init__(self) -> None:
        """Initialize a new DB instance
        """
        self._engine = create_engine("sqlite:///a.db", echo=True)
        Base.metadata.drop_all(self._engine)
        Base.metadata.create_all(self._engine)
        self.__session = None
    @property
    def _session(self) -> Session:
        """Memoized session object
        """
        if self.__session is None:
            DBSession = sessionmaker(bind=self._engine)
            self.__session = DBSession()
        return self.__session'
      ```
      * **2. Find user**
      * [db.py](./db.py): In this task you will implement the DB.find_user_by method. This method takes in arbitrary keyword arguments and returns the first row found in the users table as filtered by the method’s input arguments. No validation of input arguments required at this point.

Make sure that SQLAlchemy’s NoResultFound and InvalidRequestError are raised when no results are found, or when wrong query arguments are passed, respectively.

Warning:

NoResultFound has been moved from sqlalchemy.orm.exc to sqlalchemy.exc between the version 1.3.x and 1.4.x of SQLAchemy - please make sure you are importing it from sqlalchemy.orm.exc

* **4. Hash password**
*  [auth.py](./auth.py): In this task you will define a _hash_password method that takes in a password string arguments and returns bytes.

The returned bytes is a salted hash of the input password, hashed with bcrypt.hashpw.

* **5. Register user**
* [auth.py](./auth.py): In this task, you will implement the Auth.register_user in the Auth class provided below:

```
from db import DB
class Auth:
    """Auth class to interact with the authentication database.
    """
    def __init__(self):
        self._db = DB()
```
* **6. Basic Flask app**
* [app.py](./app.py): In this task, you will set up a basic Flask app.

Create a Flask app that has a single GET route ("/") and use flask.jsonify to return a JSON payload of the form:

* **10. Get session ID**
* [auth.py](./auth.py): In this task, you will implement the Auth.create_session method. It takes an email string argument and returns the session ID as a string.

The method should find the user corresponding to the email, generate a new UUID and store it in the database as the user’s session_id, then return the session ID.

Remember that only public methods of self._db can be used.

      
        
        
     
      
