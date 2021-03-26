# GPG Cheatsheet

> Shhhhhh. If you whisper, it will be gone.

## Key Management

### Generate
```sh
gpg --gen-key
```

### Export
```sh
gpg --export <uid>
```

### Import
```sh
gpg --import <filename>
```

### Revoke
```sh
gpg --gen-revoke
```

### List All
```sh
gpg --list-keys
```

### List All and Signatures
```sh
gpg --list-sigs
```

### List All and Fingerprints
```sh
gpg --fingerprint
```

### List Secret
```sh
gpg --list-secret-keys
```

### Delete
```sh
gpg --delete-key <uid>
```

### Delete Secret
```sh
gpg --delete-secret-key
```

### Edit
```sh
gpg --edit-key <uid>
```
