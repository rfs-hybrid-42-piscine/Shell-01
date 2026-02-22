# 🟢 Exercise 03: count_files

## 📝 Objective
Count the total number of regular files and directories in the current directory and all subdirectories, including the starting directory (`.`).

## 💡 The Logic
If we use `find .` without any filters, it lists everything (files and folders), one per line. We can pipe that giant list directly into `wc -l` (word count by lines). Because `wc` sometimes pads its output with blank spaces, we use `tr -d ' '` to trim it.

## 🛠️ Step-by-Step Solution

1. **Create the shell script:**
   Use `echo` to redirect the command pipeline into the file.
   ```bash
   echo "find . | wc -l | tr -d ' '" > count_files.sh
   ```

2. **Test it:**
   Run the script and compare it against manually counting a small test directory.
   ```bash
   bash count_files.sh
   ```
