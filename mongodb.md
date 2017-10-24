# MongoDB

## Sort the results
```js
db.collection.find().sort( { age: -1 } )
```

## Show only specific fields
```js
db.collection.find({}, { name: true, _id: false } )
```

## Finding documents using operators
```js
db.collection.find({ count: { $gt: 10 } })
db.collection.find({ count: { $lte: 10 } }) 
db.collection.find({ type: { $exists: true } }) 
db.collection.find({ name: { $regex: '^U' } }) 
```

## Update document
```js
db.collection.update({ name: 'Something'}, { $set : { operator: 'Starfleet', class: 'Prometheus' } })
```

## Insert document
```js
db.collection.insert({ name: 'card', age: 21 })
```
