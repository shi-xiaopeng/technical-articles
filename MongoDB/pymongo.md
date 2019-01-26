```
from pymongo import MongoClient
# get mongo client
client = MongoClient('localhost:27017')
or
client = MongoClient('localhost', 27017)
# get database
db = client.EmployeeData
or
db = client['EmployeeData']
# insert
db.Employees.insert_one({
        "id": employeeId,
        "name":employeeName,
        "age":employeeAge,
        "country":employeeCountry
})
# insert_many
db.Employees.insert_many([
        {
            "id": employeeId,
            "name":employeeName,
            "age":employeeAge,
            "country":employeeCountry
        },
        {
            "id": employeeId,
            "name":employeeName,
            "age":employeeAge,
            "country":employeeCountry
        }
])
# query
db.Employees.find()     #  找到Employees中的所有记录的Cursor
db.Employees.find_one({'name': 'author'})  # 查找一条name为author的记录
db.Employees.find_one({'_id': employee_id})  # query by id
# count
db.Employees.count()  #  get a count of all the document in a collection
db.Employees.find({'age': 20}).count()  # 得到所有20岁的雇员数量

# update
db.Employees.update_one(
        {'id': criteria},
        {'$set': {
                "name":name,
                "age":age,
                "country":country
        }}
)

# delete_many
db.Employees.delete_many({'id': criteria})

# sort $lt
db.Employees.find({'date': {'$lt' : d}}).sort('age')  # 找出所有字段加入日期早于特定日期的雇员，并按照年龄排序

# create unique index
db.Employees.create_index([('user_id', pymongo.ASCENDING)], unique=True)



```
