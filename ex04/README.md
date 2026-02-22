# 🟢 Exercise 04: MAC

## 📝 Objective
Write a script that displays the machine's MAC addresses, one per line.

## 💡 The Logic
The `ifconfig` command dumps network interface configuration. A MAC address follows a very strict mathematical format: six groups of two hexadecimal digits separated by colons (e.g., `00:1A:2B:3C:4D:5E`). 

Instead of relying on column numbers, we can use `grep` with Extended Regular Expressions (`-E`) to hunt specifically for this pattern.
* `ifconfig -a`: Lists all interfaces, even those that are currently down.
* `grep -o`: The "only matching" flag. It strips away all the surrounding text on the line and outputs *only* the piece of text that matched our search.
* `[[:xdigit:]]{2}`: Matches exactly two hexadecimal characters.
* `(...:){5}`: Looks for that hex pair followed by a colon, exactly 5 times.
* `..`: Matches the final two characters of the address.

## 🛠️ Step-by-Step Solution

1. **Create the shell script:**
   Use `echo` to redirect the regex pipeline into the file.
   ```bash
   echo "ifconfig -a | grep -oE '([[:xdigit:]]{2}:){5}..'" > MAC.sh
   ```

2. **Test it:**
   Run the script and verify it correctly isolates your MAC addresses.
   ```bash
   bash MAC.sh
   ```
