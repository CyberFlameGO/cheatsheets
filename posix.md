# POSIX Cheatsheet

> It's Unix, not Linux.

## Table of Contents

- [Batch Operations](#batch-operations)

## Batch Operations

### Rename Files
```sh
for j in *.bak; do mv -v -- "$j" "${j%.bak}.txt"; done
```
