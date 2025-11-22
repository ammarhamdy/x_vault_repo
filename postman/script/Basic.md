

## `pm.expect` function 
The `pm.expect()` function in Postman is based on the `Chai` assertion library, specifically `Chai's BDD` style assertions.
`pm.expect()` **does not return a value**.
It is used to perform **assertions** (checks) and **throws an error** if the assertion **fails**.
If the assertion **passes**, the test **continues** without returning anything.

```ls
pm.test("Check name field in response", function () {
    var jsonData = pm.response.json();
    /*If name is not "Alice", test fails*/
    pm.expect(jsonData.name).to.equal("Alice");
});
```



---
## **Commonly Used Assertions**

1. **Equality & Comparison**
    - `.equal(value)` / `.eql(value)` → Checks if values are equal.
    - `.not.equal(value)` → Checks if values are not equal.
    - `.above(value)` / `.greaterThan(value)` → Checks if a number is greater.
    - `.below(value)` / `.lessThan(value)` → Checks if a number is smaller.
    - `.within(start, end)` → Checks if a number is within a range.

2. **Type Checking**
    - `.a(type)` → Checks if value is of a specific type (`'string'`, `'number'`, etc.).
    - `.an(type)` → Same as `.a(type)`.

3. **Existence & Emptiness**
    - `.exist` → Checks if value is not `null` or `undefined`.
    - `.not.exist` → Checks if value is `null` or `undefined`.
    - `.empty` → Checks if an array, object, or string is empty.
    - `.not.empty` → Checks if an array, object, or string is not empty.

4. **String & Array Assertions**
    - `.include(value)` / `.contain(value)` → Checks if a string/array contains a value.
    - `.match(regex)` → Checks if a string matches a regular expression.
    - `.lengthOf(number)` → Checks the length of a string or array.

5. **Object Property Assertions**
    - `.have.property(key[, value])` → Checks if an object has a specific property.
    - `.have.keys([keys])` → Checks if an object has specific keys.

6. **Boolean Assertions**
    - `.true` / `.false` → Checks if value is `true` or `false`.


```ls
pm.expect(jsonData.name).to.equal("Alice");    /*Check exact match*/
pm.expect(jsonData.name).to.include("Ali");   /*Check substring*/
pm.expect(jsonData.age).to.be.above(18);      /*Check greater than*/
pm.expect(jsonData.isActive).to.be.true;      /*Check boolean*/
pm.expect(jsonData).to.have.property("email"); /*Check property exists*/
pm.expect(jsonData.tags).to.have.lengthOf(3); /*Check array length*/
```



## More about `.to.have`


### Object Property Assertions

Checks if an object has a property (with optional value)
```js
pm.expect(user).to.have.property("name", "Alice");
```

Checks if an object has an own property (not inherited)
```js
pm.expect(user).to.have.ownProperty("id");
```

Checks if an object has a specific property descriptor
```js
pm.expect(obj).to.have.ownPropertyDescriptor("prop");
```

### Object Keys Assertions 

Checks if an object contains exact keys
```js
pm.expect(user).to.have.keys(["name", "age"]);
```

Same as `.keys()`, ensures all provided keys exist
```js
pm.expect(user).to.have.all.keys("name", "email");
```

Checks if an object has at least one of the keys
```js
pm.expect(user).to.have.any.keys(["name", "email"]);
```




---
# Assertion Styles in `Chai`

`Chai` provides three assertion styles:
1. BDD (Behavior-Driven Development) Style – `expect` / `should`
2. TDD (Test-Driven Development) Style – `assert`

Example using `expect`:
```js
const chai = require("chai");
const expect = chai.expect;

expect(5).to.equal(5);
expect("hello").to.have.lengthOf(5);
expect([1, 2, 3]).to.include(2);
```

Example using `should`:
```js
const chai = require("chai");
chai.should();

(5).should.equal(5);
"hello".should.have.lengthOf(5);
[1, 2, 3].should.include(2);
```

### TDD Style (`assert`)
- Uses classic assertion functions
- Less readable but useful for strict comparisons
```js
const chai = require("chai");
const assert = chai.assert;

assert.equal(5, 5);
assert.lengthOf("hello", 5);
assert.include([1, 2, 3], 2);
```