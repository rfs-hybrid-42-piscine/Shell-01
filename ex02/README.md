# 🟢 Exercise 02: find_sh

## 📝 Objective
Find all files ending in `.sh` in the current directory and all subdirectories, and output *only* their names without the `.sh` extension.

## 💡 The Logic
The `find` command locates the files. The `basename` command extracts just the file name from a path and strips a specified suffix. We can use the `-exec` flag in `find` to run `basename` on every file it locates.

## 🛠️ Step-by-Step Solution

1. **Create the shell script:**
   Use `echo` to redirect the command pipeline into the file.
   ```bash
   echo 'find . -type f -name "*.sh" -printf "%f\n" | sed "s/\.sh$//"' > find_sh.sh
   ```

2. **Test it:**
   Create dummy files like `test.sh` in nested directories, run your script, and verify that only `test` is printed to the terminal.
   ```bash
   bash find_sh.sh
   ```
