![Ironhack Logo](https://i.imgur.com/1QgrNNw.png)

# Answers

## 1. Find all the companies that include 'Facebook' on the **name** field.

 - **`query`**: {name: 'Facebook'}
 db.companies.find({name:'Facebook'}).pretty();
 //1
 
 ## 2. Find all the companies which **category_code** is 'web'. Retrive only their `name` field:

 - **`query`**: {category_code: 'web'}
 - **`projection`**: {name: 1, _id: 0}
 db.companies.find({category_code:'web'},{name: 1, _id: 0});
 //3787

## 3. Find all the companies named "Twitter", and retrieve only their `name`, `category_code` and `founded_year` fields.
db.companies.find({name:'Twitter'},{name: 1,category_code:1,founded_year:1, _id: 0});
//1

## 4. Find all the companies who have `web` as their **category_code**, but limit the search to 50 companies.
 db.companies.find({category_code:'web'}).limit(50).pretty();
 //50

## 5. Find all the companies which **category_code** is 'enterprise' and have been founded in 2005. Retrieve only the `name`, `category_code` and `founded_year` fields.
db.companies.find({category_code: 'enterprise',founded_year:2005},{name:1,category_code:1,founded_year:1,_id:0}).pretty();
//39

## 6. Find all the companies that have been **founded** on the 2000 or have 20 **employees**. Sort them descendingly by their `number_of_employees`.
db.companies.find({$or:[{founded_year:2000},{number_of_employees:20}]}).sort({$or:[{founded_year:2000},{number_of_employees:20}]}).pretty();
//783

## 7. Find all the companies that do not include `web` nor `social` on their **category_code**. Limit the search to 20 documents and retrieve only their `name` and `category_code`.
db.companies.find({category_code: {$nin:["web", "social"]}}, {name: 1, category_code: 1, _id: 0}).limit(20)
//20;

## 8. Find all the companies that were not **founded** on 'June'. Skip the first 50 results and retrieve only the `founded_month` and `name` fields.
db.companies.find({founded_month: {$ne: 6}}, {name: 1, founded_month: 1, _id:0}).skip(50)
//1843

## 9. Find all the companies that have 50 employees, but do not correspond to the 'web' **category_code**. 
db.companies.find({category_code: {$ne: 'web'},number_of_employees:50});
//200

## 10. Find all the companies that have been founded on the 1st of the month, but does not have either 50 employees nor 'web' as their **category_code**. Retrieve only the `founded_day` and `name` and limit the search to 5 documents.
db.companies.find({founded_day:1,$nor:[{number_of_employees:50}, {category_code:"web"}]},{name:1,founded_day:1,_id:0}).limit(5);
//5

## 11. Find all the companies which the `price_amount` of the `acquisition` was **`40.000.000`**. Sort them by `name`.
db.companies.find({'acquisition.price_amount':40000000}).sort({name:1}).pretty();
//13

## 12. Find all the companies that have been acquired on January of 2014. Retrieve only the `acquisition` and `name` fields.
db.companies.find({'acquisition.acquired_year':2014,'acquisition.acquired_month':1},{acquisition:1,name:1,_id:0}).pretty()
//3
