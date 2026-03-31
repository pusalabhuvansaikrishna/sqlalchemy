# sqlalchemy
Commands of SQLAlchemy


**from sqlalchemy import create_engine, Integer, Column, String, or_, and_,not_, func**  
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

### Read
session.query(User).all() -> Will retrive all the records in the DB of that mentioned table.  
session.query(User).filter_by(id=1).all() -> Will retrive the records which satisfies the condition. This will outputs in list, even if there are one output.  
session.query(User).filter_by(id=1).one_or_none() -> This will except that, there must be only one record which satisfies the condition, if there are nothing which will satisfies the condition, it will return None. If there are multiple rows which satisfies this, it will return an exception and the final output is direct object itself.  

### Update
instance=session.query(User).filter_by(id=1).one_or_none()  
print("Existing Name:",instance.name)  
instance.name="Allu Arjun"  
session.commit()  

instance=session.query(User).filter_by(id=1).one_or_none()  
print("Updated Name:", instance.name)  

### Delete
session.delete(instance)  

### Ordering Data
users=session.query(User).order_by(User.age).all() -> This will order the results from User table based on age column and provide the answer, By default the answer is Ascending.  
users=session.query(User).order_by(User.age.desc()).all() -> This will order the results and provide the answer in descending order.  
users=session.query(User).order_by(User.age, User.name).all() -> This will first order the results based on age, If there are multiple records with same values then among those values it will order it by name.  

### Filtering Data
users=session.query(User).filter(User.age>=25).all()  
users=session.query(User).filter(User.age>=25, User.name=="Ironman").all() -> This bydefault use the and condition.  
users=session.query(User).filter(and_(User.age>=30, User.name=="Ironman", User.id>4)).all()  
users=session.query(User).filter(or_(User.age>=20, User.name=="Ironman")).all() -> Same as above but not the condition is or.  
users=session.query(User).filter((User.age>=20)|(User.name=="Ironman")).all() -> Same as above but not with or_ function.  
users=session.query(User).filter_by(age=25).all() -> this filter_by will only works for equal to operation, not for others. and the parameter (eg: age) must be working, not like User.age  

### Group by
users=session.query(User).group_by(User.age).all()  
users=session.query(User.age, func.count(User.id)).group_by(User.age).all()  


### Chaining
users=session.query(User).filter(User.age>20).filter(User.age<58).all()  
