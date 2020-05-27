```bash
### 1. Find and remove empty files/directories
find ./ -type f -empty	
find ./ -type d -empty

find ./ -type f -size 0 -delete
find ./ -type d -empty -delete
```
