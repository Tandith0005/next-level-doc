# Module 2: JavaScript Data Transformation and Aggregation

---

## 2-1 Objects limitations and Map Introduction

### Limitations of JavaScript Objects

- **Key types are always strings or symbols**: Even if you use numbers, boolean or objects as keys, they are automatically converted to strings.

  ```js
  const obj = {};
  obj[5] = "five";
  console.log(obj["5"]); // 'five'
  ```

- **Objects as Keys**: If you use an object as a key in another object, JavaScript converts the object key to the string `"[object Object]"`, which can lead to unexpected overwriting.

```js title="Common Variable"
const course1 = { name: "MERN" };
const course2 = { name: "Go" };
```

```js title="Using Object"
const obj = {};
obj[course1] = { id: "level 1" }; // This gets saved under "[object Object]"
obj[course2] = { id: "level 2" }; // This also gets saved under "[object Object]", overwriting the previous value

console.log(obj); // Output: { '[object Object]': {id: "level 2"} }
```

Both entries overwrite each other because the key becomes the same string, losing the association between each `course` and their `obj`.

To overcome this limitation we can use JavaScript Built-in data stricture `Map`

:::info
`Map` এ যেকোন ডাটা টাইপকে অবজেক্টের কি হিসাবে রাখা যায়। `Map` object's এর এই `‍‍key` data কে string এ convert করে না।
:::

```js title="Using Map"
const pHero = new Map();

pHero.set(course1, { id: "level 1" }); // Map allows course1 object as key
pHero.set(course2, { id: "level 2" }); // Map allows course2 object as key

console.log(pHero.get(course1)); // Output: { id: "level 1" }
console.log(pHero);
// Output: Map(2) { { name: "MERN" } => { id: "level 1" }, { name: "Go" } => { id: "level 2" } }
```

### Common Map Methods

#### 1. `set(key, value)`

Adds or updates an element with a specified key and value.

```js
pHero.set(course1, { id: "level 1" });
pHero.set(course2, { id: "level 2" });
```

#### 2. `get(key)`

Retrieves the value for a given key.

```js
console.log(pHero.get(course1));
// Output: { id: "level 1" }
```

#### 3. `has(key)`

Checks if a key exists in the Map. Return `Boolean` value

```js
console.log(pHero.has(course1)); // true
console.log(pHero.has(course5)); // false
```

#### 4. `size`

Returns the number of elements in the Map.

```js
console.log(pHero.size); // 2
```

#### 5. `delete(key)`

Removes an element by key.

```js
pHero.delete(course1);
console.log(pHero); // Map(1) { id: "level 2" }
```

#### 6. `clear()`

Removes all elements from the Map.

```js
pHero.clear();
console.log(pHero.size); // 0
```

#### 7. Iterating over a Map

we can use `forEach`, `for...of`

```js title="Using forEach Method"
pHero.forEach((value, key) => {
  console.log(key, value);
});

// Renaming key name of obj using forEach
pHero.forEach((value, key) => (key.name = "S3 " + key.name));
// {name: "S3 MERN"}, {name: "S3 Go"}
```

```js title="Using for...of loop"
for (const [key, value] of pHero) {
  console.log(key, value);
}

for (let key of pHero.keys()) {
  key.name = "S3 " + key.name;
}
// {name: "S3 MERN"}, {name: "S3 Go"}
```

#### 8. `keys()` and `values()`

They gives an iterator. By using this we can apply spread operation

```js
console.log([...pHero.keys()]); // [{ name: "MERN" }, { name: "Go" }]
console.log([...pHero.values()]); // [{ id: "level 1" }, { id: "level 2" }]
```

#### 9. `entries()`

It return a new iterator obj that contains an array of `[key, value]` pairs for each element

```js
const courses = [
  ["MERN", "l1"],
  ["Go", "l2"],
];
const pHeroMap = new Map(courses); // Map { MERN → "l1", Go → "l2" }
```

You can also use the spread operator to convert the Map entries into an array:

```js
const allEntries = [...pHero.entries()];
console.log(allEntries);
// Output: [ [ { name: "MERN" }, { id: "level 1" } ], [ { name: "Go" }, { id: "level 2" } ] ]
```
