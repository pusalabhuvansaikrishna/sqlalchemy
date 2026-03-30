# sqlalchemy
Commands of SQLAlchemy


**from sqlalchemy import create_engine, Integer, Column, String**  
**from sqlalchemy.orm import sessionmaker, relationship, declarative_base**  

database_url="<db_provider_name>://<username>:<password>@localhost:5432/<db_name>"  
engine=create_engine(database_url)
Session=sessionmaker(bind=engine)
session=Session()
Base=declarative_base()

## Table Declaration
eg:  
class User(Base):  
__tablename__="users"  
column1=Column()  
column2=Column()  
column3=Column()  

Base.metadata.create_all(engin) -> This will consider the classes which you have declared above and create the tables in the mentioned DB  

user1=User(column1="", column2="")  

### Create
session.add(user1) -> Add only mentioned object into the table  
session.add_all([user1, user2, user3]) -> Add the mentioned users into the table  
