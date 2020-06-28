# Python Cheatsheet

> And now for something completely different.

## Table of Contents

- [Command-Line Usage](#command-line-usage)
- [Databases](#databases)
- [File Operations](#file-operations)
- [Iteration](#iteration)
- [Network Connections](#network-connections)
- [Type Casting](#type-casting)

## Command-Line Usage

### Argument Parsing
```py
import argparse

parser = argparse.ArgumentParser(description="Something useful.")
parser.add_argument("input", help="Input file", nargs='?')
parser.add_argument("output", help="Output file", nargs='?')
parser.add_argument("--flag", help="An optional flag", action='append')

args = parser.parse_args()

if args.flag is not None:
    print("The flag was provided.")

print(args.input)
print(args.output)
```

## Databases

### TinyDB

#### Install
```sh
pip install tinydb
```

#### Use
```py
from tinydb import TinyDB, Query

db = TinyDB('db.json')

# Insert
db.insert({ 'type': 'OSFY', 'count': 700 })
db.insert({ 'type': 'EFY', 'count': 800 })

# Dump
db.all()
# => [{'count': 700, 'type': 'OSFY'}, {'count': 800, 'type': 'EFY'}]

# Search and List
Magazine = Query()
db.search(Magazine.type == 'OSFY')
# => [{'count': 700, 'type': 'OSFY'}]
 
db.search(Magazine.count > 750)
# => [{'count': 800, 'type': 'EFY'}]

# Update
db.update({'count': 1000}, Magazine.type == 'OSFY')
db.all()
# => [{'count': 1000, 'type': 'OSFY'}, {'count': 800, 'type': 'EFY'}]

# Remove
db.remove(Magazine.count < 900)
db.all()
# => [{'count': 800, 'type': 'EFY'}]

# Purge
db.purge()
db.all()
# => []

# In-Memory Use
from tinydb.storages import MemoryStorage
db = TinyDB(storage=MemoryStorage)
```

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
