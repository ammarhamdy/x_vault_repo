
Defines a test case:
```js
pm.test("Test Name", function () {...})
```

Assertion for values:
```js
pm.expect(actual).to.equal(expected);
```

## Response time
```js
pm.test("Response time below 200", function () {
    pm.expect(pm.response.responseTime).to.be.below(200);
});
```


## Response code
```js
let statusCode = pm.response.code;
console.log("Status Code:", statusCode);
```

```js
pm.test("Status code is 202", function () {
    pm.response.to.have.status(202);
});
```


