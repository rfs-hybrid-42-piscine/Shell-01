# 🟢 Exercise 05: Can you create it?

## 📝 Objective
Create a file containing only the string `42` with an exact, highly specific name full of special characters: `"\?$*'MaRViN'*$?\"`. The file must also perfectly match specific permissions, file size (2 bytes), and timestamps.

## 💡 The Logic
1. **Special Characters:** Characters like `*`, `$`, and `\` are interpreted by the terminal as active commands or wildcards. To create the file safely, you must wrap the entire filename string in strong quotes (`'`) and carefully escape the inner quotes.
2. **File Size (2 Bytes):** The string "42" is two bytes. However, the standard `echo` command automatically adds a hidden newline character at the end, making it 3 bytes. We must use `echo -n` to suppress the newline.
3. **Permissions:** The target is `-rw---xr--`.
   * User: `rw-` (4 + 2 + 0 = 6)
   * Group: `--x` (0 + 0 + 1 = 1)
   * Other: `r--` (4 + 0 + 0 = 4)
   This gives the octal permission code `614`.
4. **Timestamp:** The `ls -l` output requires the date to be `Oct 2 12:21`. 

## 🛠️ Step-by-Step Solution

1. **Create the file and set its size:**
   Use `echo -n` to write exactly 2 bytes into the complex filename. 
   ```bash
   echo -n "42" > '\"?$*'\''MaRViN'\''*$?\"'
   ```
   *(Note: Escaping single quotes inside a single-quoted string in Bash requires closing the quote, adding an escaped quote `\'`, and reopening it).*

2. **Set the correct permissions:**
   ```bash
   chmod 614 '\"?$*'\''MaRViN'\''*$?\"'
   ```

3. **Set the correct timestamp:**
   Use `touch -t` to forge the exact date (Year + Month + Day + Hours + Minutes).
   ```bash
   touch -t 202510021221 '\"?$*'\''MaRViN'\''*$?\"'
   ```

4. **Verify the output:**
   Run the exact command from the subject to ensure it matches perfectly.
   ```bash
   ls -lRa *MaRV* | cat -e
   ```
   *(Expected output: `-rw---xr-- 1 [User] [Group] 2 Oct 2 12:21 "\?$*'MaRViN'*$?\"$`)*
