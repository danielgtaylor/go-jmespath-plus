# go-jmespath-plus - A JMESPath implementation in Go

![CI](https://github.com/danielgtaylor/go-jmespath-plus/workflows/CI/badge.svg?branch=master)

See http://jmespath.org for more info.

## Enhancements

### Recursive Descent Operator

A new `..` recursive descent operator is supported. It will recursively traverse all objects and arrays to create a new projection. For example, given:

```json
{
  "foo": {
    "bar": 1,
    "baz": [
      {
        "bar": 2
      },
      {
        "bar": 3
      }
    ]
  }
}
```

Then you can see the difference between the a wildcard and recursive descent:

```sh
# Wildcard key, selects only the first `bar`.
$ jpgo '*.bar' <input
[1]

# Recursive descent, selects *all* the `bar` entries.
$ jpgo '..bar' <input
[1, 2, 3]
```

### Multi-select Hash Shorthand

Selecting a single key from an object is now possible with a property shorthand syntax borrowed from [modern Javascript](http://es6-features.org/#PropertyShorthand). Given:

```json
{
  "foo": {
    "bar": 1,
    "baz": [true, false]
  }
}
```

Then you can select via the shorthand:

```sh
# Shorthand example.
$ jpgo 'foo.{bar}' <input
{"bar": 1}

# Mixing shorthand and long-form.
$ jpgo 'foo.{bar, first_baz: baz[0]}' <input
{"bar": 1, "first_baz": true}
```
