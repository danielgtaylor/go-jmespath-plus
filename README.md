# go-jmespath-plus - A JMESPath implementation in Go

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
