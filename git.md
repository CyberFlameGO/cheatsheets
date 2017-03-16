# Git Cheatsheet

## Archive

``` bash
git archive --format=tar --prefix=foo_bar-1.0/ v1.0 | xz > foo_bar-1.1.tar.xz
```

## Changing Author Info

### Whole Repository
Change `OLD_EMAIL`, `CORRECT_NAME` and `CORRECT_EMAIL` to desired values, afterwards run `git push --force --tags origin 'refs/heads/*'`.
``` bash
git filter-branch --env-filter '
OLD_EMAIL="your-old-email@example.com"
CORRECT_NAME="Your Correct Name"
CORRECT_EMAIL="your-correct-email@example.com"
if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$CORRECT_NAME"
    export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags
```

### One Commit

``` bash
# Checkout the commit we are trying to modify.
git checkout 03f482d6

# Make the author change.
git commit --amend --author "New Author Name <New Author Email>"

# Replace the old commit with the new one locally.
git replace 03f482d6 42627abe

# Rewrite all future commits based on the replacement.
git filter-branch -- --all

# Remove the replacement for cleanliness.
git replace -d 03f482d6

# Push the new history (after sanity checking with git log).
git push -f
```


## Submodules

### Update all Submodules
```bash
git submodule update --recursive --remote
```


## Tags

``` bash
git tag v1.0
git push origin v1.0
```
