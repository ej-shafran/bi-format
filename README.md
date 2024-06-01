# bi format

Simple Structure Human-Readable Binary Format. It is used by such projects as [rere.py](https://github.com/tsoding/rere.py) and [Porth](https://gitlab.com/tsoding/porth).

The goals of the format:
- So simple you don't need a library to Parse it or Serializer into it,
- If the data stored in the blobs is Text the whole file looks like Text making any changes committed in VCS have a nice Human-Readable Diff.

## Description

A bi file consist of sequence of fields. There are only 2 kinds of fields for now: integer and blob. (We may add more kinds of fields in the future, but it's very unlikely, because these two feel pretty sufficient for now).

### Integer field

- An integer field starts with a sequence of bytes that if viewed as ASCII looks like `:i` followed by exactly ONE space.
- After that comes a sequence of arbitrary bytes (excluding newline `\n`) which denotes the name of the field. It is usually recommended to use ASCII Human-Readable names, but you do you. The name ends with exactly ONE space.
- After that comes a sequence of ASCII digits denoting the integer stored in the field. There is no upper bound for integers. Handle overflows however you want. (We don't support negative integers right now, but we may in the future if needed)
- Field ends with ASCII newline `\n`

Here is how a bunch of integer fields would look like in a bi file:

```
:i foo 69
:i bar 420
:i baz 1337
```

### Blob fields

TBD