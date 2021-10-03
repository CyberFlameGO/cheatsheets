# POSIX Cheatsheet

> It's Unix, not Linux.

## Table of Contents

- [Batch Operations](#batch-operations)
- [Text Processing](#text-processing)

## Batch Operations

### Rename Files
```
for j in *.bak; do mv -v -- "$j" "${j%.bak}.txt"; done
```

## Text Processing

### Skip First Line
```
sed -n '1d;p'
```
