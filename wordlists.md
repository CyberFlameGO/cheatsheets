# Wordlists

> Tools to deal with wordlists, yo.

## Cleaning

### Remove Lines Under n Characters
In this case, remove every line under 6 characters long.
```bash
sed -E '/^.{,6}$/d' /path/to/input/file > /path/to/output/file
```

## Sorting

### Sort Alphabetically and Remove Duplicates
```bash
sort -us -o /path/to/output/file /path/to/input/file
```
