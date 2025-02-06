# MongoDB $inc operator with String Value

This repository demonstrates an uncommon error in MongoDB when using the `$inc` operator with a string value instead of a numeric value.  The expected behavior would be an error; however, MongoDB unexpectedly appends the string instead of incrementing the numeric value.

## Bug Description
The `$inc` operator is designed to increment a numeric field in a MongoDB document. However, if you pass a string to the `$inc` operator, it will append the string value instead of throwing an error.

## How to Reproduce
1. Create a MongoDB collection (e.g., `myCollection`).
2. Insert a document with a numeric field (e.g., `counter`).
3. Run the following update operation:
   ```javascript
   db.myCollection.updateOne({"_id": 1}, {"$inc": {"counter": "1"}})
   ```
4. Observe that the `counter` field is updated by appending "1" to its existing value instead of incrementing it numerically.

## Solution
Ensure that the value provided to the `$inc` operator is a number. Using a string will lead to unexpected behavior.

```javascript
db.collection.updateOne({"_id":1},{"$inc":{"counter":1}})
```