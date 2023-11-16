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
        return self.__session
        ```
        
      * **2. Find user**  
      
