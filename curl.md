# curl Cheatsheet

> Request anything.

## Table of Contents

- [Headers](#headers)
- [Behavior](#behavior)

## Headers

### Print Response Headers
```
curl -s -D - -o /dev/null http://example.com
```

### Set User Agent String
```
curl -A "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_6) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/13.1.2 Safari/605.1.15" http://example.com
```

### Set Custom Header
```
curl -H "Content-Type: application/json" http://example.com
```

## Behavior

### Follow Redirections
```
curl -L http://example.com
```
