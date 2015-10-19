

## Bash

Delete files from a certain age

```bash
find . -mtime +20 -type f -delete
```

When directories _and_ files need to be deleted, use this instead:

```bash
find . -mtime +20 -type d -type f -delete
```

