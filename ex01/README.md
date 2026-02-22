# 🟢 Exercise 01: print_groups

## 📝 Objective
Write a script that displays a comma-separated list of groups the user (defined in the `$FT_USER` environment variable) belongs to, with no spaces and no trailing newline.

## 💡 The Logic
The `id` command with the `-Gn` flags prints all group names for a specific user. However, it outputs them separated by spaces and adds a newline at the end. We must use `tr` (translate) to replace the spaces with commas, and another `tr` to delete the newline.

## 🛠️ Step-by-Step Solution

1. **Create the shell script:**
   Use `echo` to redirect the correct command into the file. The `$` must be escaped so it evaluates when the script runs, not when you press enter.
   ```bash
   echo "id -Gn \$FT_USER | tr ' ' ',' | tr -d '\n'" > print_groups.sh
   ```

2. **Test it:**
   You must set the environment variable first!
   ```bash
   export FT_USER=daemon
   bash print_groups.sh
   ```
