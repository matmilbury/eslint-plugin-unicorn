# Prefer ternary expressions over simple `if-else` statements

This rule enforces the use of ternary expressions over  'simple' `if-else` statements, where 'simple' means the consequent and alternate are each one line and have the same basic type and form.

Using an `if-else` statement typically results in more lines of code than a single-line ternary expression, which leads to an unnecessarily larger codebase that is more difficult to maintain.

Additionally, using an `if-else` statement can result in defining variables using `let` or `var` solely to be reassigned within the blocks. This leads to variables being unnecessarily mutable and prevents `prefer-const` from flagging the variable.

This rule is fixable.

## Fail

```js
function unicorn() {
	if (test) {
		return a;
	} else {
		return b;
	}
}
```

```js
function* unicorn() {
	if (test) {
		yield a;
	} else {
		yield b;
	}
}
```

```js
async function unicorn() {
	if (test) {
		await a();
	} else {
		await b();
	}
}
```

```js
if (test) {
	throw new Error('foo');
} else {
	throw new Error('bar');
}
```

```js
let foo;
if (test) {
	foo = 1;
} else {
	foo = 2;
}
```

## Pass

```js
function unicorn() {
	return test ? a : b;
}
```

```js
function* unicorn() {
	yield (test ? a : b);
}
```

```js
async function unicorn() {
	await (test ? a() : b());
}
```

```js
const error = test ? new Error('foo') : new Error('bar');
throw error;
```

```js
let foo;
foo = test ? 1 : 2;
```

```js
// Multiple expressions
let foo;
let bar;
if (test) {
	foo = 1;
	bar = 2;
} else{
	foo = 2;
}
```

```js
// Different expressions
function unicorn() {
	if (test) {
		return a;
	} else {
		throw new Error('error');
	}
}
```

```js
// Assign to different variable
let foo;
let bar;
if (test) {
	foo = 1;
} else{
	baz = 2;
}
```