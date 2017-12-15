# Wordlists

> Tools to deal with wordlists, yo.

## Cleaning

### Remove Lines Under n Characters
In this case, remove every line under 6 characters long.
```bash
sed -E '/^.{,6}$/d' /path/to/input/file > /path/to/output/file
```
