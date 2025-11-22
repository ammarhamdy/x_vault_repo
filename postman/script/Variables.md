![[Screencast from 2025-03-08 14-40-08.webm]]


## Global var in script:
![[Pasted image 20250308145410.png]]

## Collection var in script:
```js
pm.collectionVariables.set("myVariable", "myValue");

console.log(
	"Collection Variable:", 
	pm.collectionVariables.get("myVariable")
);
```

## Environment variable 
```js
pm.environment.set(
	"TOKEN",
	pm.response.json().data.verification_token
);
```
