##### 1. Provide a query showing just the names (and nothing else) of the Italian restaurants.
  ```javascript
  db.restaurants.find({"cuisine": "Italian"})
  ```
##### 2. Provide a query showing how many Bakeries have a name that start with M.
  ```javascript
  db.restaurants.find({"cuisine": "Bakery", "name":/^[M]/})
  ```
##### 3. Provide a query showing the zip codes (and _id's) of all restaurants with the word "Ice" in their cuisine.
  ```javascript
  db.restaurants.find({"name":/ice/}, {"address.zipcode": 1})
  ```
##### 4. Provide a query showing the street and street number of Chinese restaurants in ascending order by zip code.
  ```javascript
  db.restaurants.find({"cuisine":"Chinese"},{"address.building": 1, "address.street": 1}).sort({"address.zipcode":1})
  ```
##### 5. Show only the American restaurants in Manhattan.
  ```javascript
  db.restaurants.find({"borough": "Manhattan", "cuisine": /American/})
  ```
##### 6. Provide a query showing the restaurants that have been graded exactly 4 times.
  ```javascript
  db.restaurants.find({ $where: "this.grades.length === 4" } )
  ```
##### 7. Provide a query showing only _id, name and 2 grades from each restaurant on Broadway.
  ```javascript
  db.restaurants.find({"address.street": "Broadway"}, {"name":1,"grades":{$slice: 2}})
  ```
##### 8. Provide a query showing the 5 pizza restaurants in the Bronx with the highest score on an evaluation.
  ```javascript
  db.restaurants.find({"cuisine":/Pizza/,"borough":"Bronx", "grades.score":{$gt: 45}})

  db.restaurants.find({"cuisine":/Pizza/,"borough":"Bronx"}).sort({"grades.score":1}).limit(5)
  ```
##### 9. Provide a query to find all of the restaurants in Brooklynn and list only the 51st-60th results when ordered alphabetically by name.
  ```javascript
  db.restaurants.find({"borough": /Brooklyn/}).skip(50).limit(60)
  ```

##### 10. Provide a query that returns all pizza and Italian restaurants in reverse alphabetic order.
  ```javascript
  db.restaurants.find({"cuisine" : { $in: ["Pizza", "Italian"]}}).sort({"name": -1})
  ```
