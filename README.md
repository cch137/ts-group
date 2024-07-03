# @cch137/group

The `@cch137/group` package provides a `Group` class that extends the functionality of arrays, along with `Collection` and `WeakCollection` classes for managing groups of items with added convenience methods. This package works in both the browser and Node.js environments.

## Installation

```bash
npm install @cch137/group
```

## Usage

### Group

The `Group` class extends the native `Array` class, providing additional methods for managing items.

#### Example

```typescript
import Group from "@cch137/group";

const group = new Group<number>();

// Add items to the group
group.add(1, 2, 3);
console.log(group); // Output: [1, 2, 3]

// Check if an item exists
console.log(group.has(2)); // Output: true
console.log(group.has(4)); // Output: false

// Delete an item
group.delete(2);
console.log(group); // Output: [1, 3]

// Delete the last occurrence of an item
group.add(3, 3, 3);
group.deleteLast(3);
console.log(group); // Output: [1, 3, 3]

// Delete one occurrence of an item
group.deleteOne(3);
console.log(group); // Output: [1, 3]

// Clear the group
group.clear();
console.log(group); // Output: []
```

### Collection

The `Collection` class extends `Map` and provides methods for managing groups of items associated with keys.

#### Example

```typescript
import { Collection } from "@cch137/group";

const collection = new Collection<string, number>();

// Add items to a group in the collection
collection.group("group1").add(1, 2, 3);
console.log(collection.get("group1")); // Output: [1, 2, 3]

// Retrieve and delete a group
const group1 = collection.once("group1");
console.log(group1); // Output: [1, 2, 3]
console.log(collection.get("group1")); // Output: undefined

// Add items and trim empty groups
collection.group("group2").add(4, 5);
collection.group("group2").delete(4);
collection.trim();
console.log(collection.get("group2")); // Output: [5]
```

### WeakCollection

The `WeakCollection` class extends `WeakMap` and provides similar functionality to `Collection`, but for weakly-referenced keys.

#### Example

```typescript
import { WeakCollection } from "@cch137/group";

const weakCollection = new WeakCollection<object, number>();
const key = {};

weakCollection.group(key).add(1, 2, 3);
console.log(weakCollection.get(key)); // Output: [1, 2, 3]

const weakGroup = weakCollection.once(key);
console.log(weakGroup); // Output: [1, 2, 3]
console.log(weakCollection.get(key)); // Output: undefined
```
