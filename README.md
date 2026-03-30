# sqlalchemy
Commands of SQLAlchemy


**from sqlalchemy import create_engine, Integer, Column, String**  
**from sqlalchemy.orm import sessionmaker, relationship, declarative_base**  

database_url="<db_provider_name>://<username>:<password>@localhost:5432/<db_name>"  
engine=create_engine(database_url)
Session=sessionmaker(bind=engine)
session=Session()
Base=declarative_base()

# Table Declaration
eg:  
class User(Base):
__tablename__="users"
column1=Column()
column2=Column()
column3=Column()
