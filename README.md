# py-mongo-cmd
cmds for pymongo
# add
db.users.insertOne({
    name:'Mike',
    age: 17
});
db.users.insertMany([
    {name:"vasya",age:28},
    {name:"petya",age:23},
    {name:"dima",age:35},
    {name:"anton",age:24},
    {name:"ulbi tv",age:42}
]);

# find
db.users.find();
db.users.find({age:42});
db.users.find({age:42, name:"ulbitv"});
db.users.find({$or:[{name:"ulbi tv"},{age:35}]})
db.users.find({age:{$lt(e):35}})
db.users.find({age:{$gt(e):35}})
db.users.find({age:{$ne:35}})

db.users.find().sort({age:1}) # прямой порядок

db.users.find().sort({age:-1}) # обратінй порядок

db.users.find({
    posts: {
        $elemMatch: {title:'js'}
    }
})


db.users.find({posts: {$exists:true}})



# update
db.users.update(
    {name:'ulbi tv'}, 
    {
        $set:{
            name: 'Anton Bilenko',
        }
    }
)
db.users.updateMany(
    {}, 
    {
        $rename:{
            name:"fullname"
        }
    }
)

#delete
db.users.deleteOne({age:24})


#
db.users.bulkWrite([
    {
        insertOne: {
            document: {
                fullname:"Alex",
                age:23
            }
        }
    },
    {
        deleteOne: {
            filter:{fullname: "petya"}
        }
    }
])

# foreign key

db.users.update(
    {fullname: "Mike"},
    {
        $set:{
            posts:[
                {
                    title:'js',
                    text:'js top'
                },
                {
                    title:'mongo',
                    text:'mongo top'
                }
            ]
        }
    }
)


# short 
import pymongo

db_client = pymongo.MongoClient("Подсоеденения к баззе данных (если не помнишь как напиши)")

# сама база данних
current_db = db_client["name_db"] # если ее нету то она создается сама автаматически

# колекцыии которые зранятся в базе (типо таблицы) если нету тоже создается само
name1 = current_db["1"]
name2 = current_db["2"]
name3 = current_db["3"]

# добавление в колекцию
name1.insert_one({"Name":"admin"})

# очиста колекции
current_db.drop_collection("1")

# поиск по колециям
name1.find({"Name":"admin"}) # находит всех с именем admin
name1.find_one({"Name":"admin"}) # находит одного с именем admin
