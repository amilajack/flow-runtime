# Validation

Sometimes it's useful to get the full details of why a particular value does not match a type.

In addition to `t.any().accepts(value)` and `t.any().assert(value)`, the [TypeContext](./TypeContext.md) exposes a `t.validate(t.any(), value)` method which returns a `Validation` object:

```js
import t from 'flow-runtime';

const string = t.string();

const validation = t.validate(string, false);

validation.hasErrors(); // true
console.log(validation.errors); // array
```

## Error Reporting

`Validation` objects are the raw representation of the validation result, we use Error Reporters to turn them into something more useful.

```js

import t from 'flow-runtime';

const string = t.string();

const validation = t.validate(string, false);
if (validation.hasErrors()) {
  const json = t.makeJSONError(validation);
  console.log(JSON.stringify(json, null, 2));

  const error = t.makeTypeError(validation);
  throw error;
}

```