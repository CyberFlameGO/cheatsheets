# Python Cheatsheet

> And now for something completely different.

## Table of Contents

- [File Operations](#file-operations)
- [Iteration](#iteration)
- [Network Connections](#network-connections)
- [Type Casting](#type-casting)

## File Operations

* `x` creates new file, returns error when it exists.
* `a` appends to file, creates it when it does not exist.
* `w` overwrites file, creates it when it does not exist.

```py
f = open("file.txt", "a")
f.write("More content.")
f.close()
```

## Iteration

### Range
```py
for i in range(10):
    print(i)
```

## Network Connections

### HTTP

#### JSON
```py
import json, urllib.request
req = urllib.request.Request("https://httpbin.org/get")
req.add_header("Accept", "application/json")
r = urllib.request.urlopen(req)
data = json.loads(r.read())
print(json.dumps(data))
```

#### Plain
```py
import urllib.request
req = urllib.request.Request("https://httpbin.org/get")
r = urllib.request.urlopen(req)
data = r.read().decode("utf-8")
print(data)
```

## Type Casting

```py
integer = 42
string = "42"

# To Integer
int(string)

# To String
str(integer)
```
