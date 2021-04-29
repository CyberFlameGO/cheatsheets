# GPG Cheatsheet

> Shhhhhh. If you whisper, it will be gone.

## Key Management

------------------------- | -------------------------
`gpg --gen-key`           | Generate
`gpg --export <uid>`      | Export
`gpg --import <filename>` | Import
`gpg --gen-revoke`        | Revoke
`gpg --list-keys`         | List All
`gpg --list-sigs`         | List All and Signatures
`gpg --fingerprint`       | List All and Fingerprints
`gpg --list-secret-keys`  | List Secret
`gpg --delete-key <uid>`  | Delete
`gpg --delete-secret-key` | Delete Secret
`gpg --edit-key <uid>`    | Edit
