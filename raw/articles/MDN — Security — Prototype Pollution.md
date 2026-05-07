# JavaScript Prototype Pollution

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/Prototype_pollution

## Overview

**Prototype pollution** is a vulnerability where an attacker can add or modify properties on an object's prototype. This causes malicious values to unexpectedly appear on objects in your application, often leading to logic errors or additional attacks like cross-site scripting (XSS).

## How Prototypes Work in JavaScript

JavaScript uses prototypes for inheritance. Each object has a reference to a prototype, which itself has a prototype, continuing until reaching `Object.prototype` (whose prototype is `null`).

When accessing a property or method, JavaScript looks up the prototype chain if the property isn't found on the object itself:

```javascript
const mySet = new Set([1, 2, 3]);
// prototype chain: mySet -> Set.prototype -> Object.prototype -> null

mySet.size; // 3 (defined on Set.prototype)
mySet.propertyIsEnumerable("size"); // false (defined on Object.prototype)
```

## Anatomy of Prototype Pollution

### Two Phases

1. **Pollution**: Attacker adds or modifies properties on an object's prototype
2. **Exploitation**: Application code accesses polluted properties, causing unexpected behavior

### Pollution Sources

The key attack vector is the `__proto__` property or `.constructor.prototype`. The dangerous pattern is:

```javascript
obj[key1][key2] = value;
```

If `key1` is `"__proto__"`, this modifies `Object.prototype`.

**Example vulnerable code:**

```javascript
function getUsers(request) {
  const result = {};
  const userNames = new URL(request.url).searchParams.getAll("names");
  const fields = new URL(request.url).searchParams.getAll("fields");
  for (const name of userNames) {
    const userInfo = database.lookup(name);
    result[name] ??= {};
    for (const field of fields) {
      // Pollution source
      result[name][field] = userInfo[field];
    }
  }
  return result;
}
```

Calling with `https://example.com/api?names=__proto__&fields=age` pollutes `Object.prototype.age`.

## Defenses Against Prototype Pollution

### 1. Validate User Input

Use schema validators like [ajv](https://ajv.js.org) or [Zod](https://zod.dev/):

- Set `additionalProperties` to `false`
- Reject `__proto__`, `constructor`, and `prototype` as keys
- Set default values for missing properties

### 2. Node.js `--disable-proto` Flag

```bash
node --disable-proto=delete app.js
# or
node --disable-proto=throw app.js
```

For non-Node environments:
```javascript
delete Object.prototype.__proto__;
```

### 3. Lock Down Built-in Objects

Use `Object.freeze()`:

```javascript
Object.freeze(Object.prototype);
const obj = {};
obj.__proto__.a = 1; // fails silently in non-strict mode
obj.a; // undefined
```

### 4. Use `Object.hasOwn()` When Accessing Properties

```javascript
// Bad
if (!user.isAdmin) {
  return new Response("Access denied", { status: 403 });
}

// Good
if (!Object.hasOwn(user, "isAdmin") || !user.isAdmin) {
  return new Response("Access denied", { status: 403 });
}
```

### 5. Use Null-Prototype Objects

```javascript
// Create with Object.create(null) or { __proto__: null }
Object.prototype.method = "POST";

fetch("https://example.com", {
  __proto__: null,
  mode: "cors",
});
// Still sends GET request because object has no prototype
```

### 6. Use `Map` and `Set` Instead

```javascript
Object.prototype.admin = true;

const config = new Map();
config.set("admin", false);

config.admin; // true (prototype lookup)
config.get("admin"); // false (Map method, avoids prototype)
```

### 7. Prefer `for...of` and `Object.keys()` Over `for...in`

```javascript
// Looks up prototype
for (const key in payload) {
  doSomething(payload[key]);
}

// Only visits own keys
for (const key of Object.keys(payload)) {
  doSomething(payload[key]);
}
```

### 8. Set Explicit Default Parameters

```javascript
// Bad - lookups on prototype
function doDangerousAction(options = {}) {
  if (!options.enableDangerousAction) {
    return;
  }
}

// Good - explicit defaults
function doDangerousAction(options = { enableDangerousAction: false }) {
  if (!options.enableDangerousAction) {
    return;
  }
}
```

## Defense Summary Checklist

**When creating objects:**
- Evaluate if a `Map` or `Set` would be better
- Use null-prototype objects when passing to other functions or dynamically modifying
- Ensure all keys are defined

**When accepting user input:**
- Always validate with a schema validator
- Reject unrecognized properties
- Check if keys exist on the object itself before accessing
- Use `for...of` and `Object.keys()` instead of `for...in`

**For built-in objects:**
- Consider freezing with SES shim

**Runtime defenses:**
- Use `--disable-proto` in Node.js
- Use `delete Object.prototype.__proto__` in browsers
