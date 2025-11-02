# Module 2: JavaScript Data Transformation and Aggregation

---

## 2-1: Object Limitations and Map Introduction

### Object Limitations in JavaScript

JavaScript objects are widely used for key-value storage, but they have some limitations:

```js
const course1 = { name: "Programming Hero" };

// 1️⃣ With dot notation 2️⃣ With bracket notation

console.log(course1.name); // "Programming Hero"
console.log(course1["name"]); // "Programming Hero"

// ✅ Works for both dot and bracket notation if key is a valid identifier
```

**But what if the object is like this:**
```js
const obj = {
  "Programming Hero": { courseId: 'level1' },
};

console.log(obj.Programming Hero); // ❌ Syntax Error! 
console.log(obj["Programming Hero"]); // { courseId: 'level1' }
```
**Limitation Summary:**
- Dot notation cannot be used if property names have` `spaces, special characters `@`, or start with a number `1,2,...`
- Only strings or symbols can be object keys.
- Numeric keys are converted to strings automatically.
- Even though Dot notation is more readable and easier to use, if you have dynamic keys, it is not recommended for your code.

---

### Map — A Better Key-Value Structure
`Map` is a built-in JavaScript object designed specifically for key-value data.
Unlike normal objects, a `Map` can use any **data type as a key**, including **objects**, **arrays**, and **functions**.
**Basic Usage**
```js
// Create a new Map
const courseMap = new Map();

// Add key-value pairs
courseMap.set("name", "Next Level Web Development");
courseMap.set(1, "ID as number");
courseMap.set({ level: 1 }, "Object as key");

// Get values
console.log(courseMap.get("name"));  // "Next Level Web Development"
console.log(courseMap.size);         // 3

// Check for key existence
console.log(courseMap.has(1));       // true

// Delete a key
courseMap.delete(1);

// Map.set() returns the Map object itself
const myMap = new Map();
myMap.set("name", "Tandith");
myMap.set("age", 21);

console.log(myMap);
// Map(2) { "name" => "Tandith", "age" => 21 }
```

---
