## 📂 Folder Levels & Path Notations Explained
### 1. . (single dot) — Current directory

. means the current folder you're in.

Example:
```
./components/this
```
Means: inside the current directory, go to the components folder, then inside it to the this folder or file.

### 2. .. (double dots) — Parent directory
```
..
```
Means: go up one folder level from your current directory.

```
../
```
Means: move up to the parent folder of the current folder.
```
../assets/images
``` 

Means: go up one level, then enter assets/images.

### 3. Absolute vs Relative Paths

Absolute path: full path from root folder, e.g.
```
/home/user/project/components
```
Relative path: relative to your current folder, e.g.
```
./components or ../components
```