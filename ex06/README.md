# 🟢 Exercise 06: Skip

## 📝 Objective
Execute `ls -l` but display only every other line, starting from the first.

## 💡 The Logic
We need a tool that can read lines by their line number. `awk` is perfect for this. It keeps an internal variable `NR` (Number of Records/Lines). We can tell `awk` to print only when `NR % 2 == 1` (i.e., odd-numbered lines).

## 🛠️ Step-by-Step Solution

1. **Create the shell script:**
   Use `echo` to redirect the command pipeline into the file.
   ```bash
   echo "ls -l | awk 'NR % 2 == 1'" > skip.sh
   ```

2. **Test it:**
   Run the script in a directory with multiple files.
   ```bash
   bash skip.sh
   ```
