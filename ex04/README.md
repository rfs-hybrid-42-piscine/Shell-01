# 🟢 Exercise 04: MAC

## 📝 Objective
Display the machine's MAC addresses, one per line.

## 💡 The Logic
The `ifconfig` command dumps network interface configuration. A MAC address is typically identified by the keyword `ether`. We can use `grep` to filter out only the lines containing `ether`, and then use `awk` to grab the specific column where the address is located.

## 🛠️ Step-by-Step Solution

1. **Create the shell script:**
   Use `echo` to redirect the command pipeline into the file. Escape the `$` so `awk` receives the `$2` parameter correctly.
   ```bash
   echo "ifconfig | grep 'ether ' | awk '{print \$2}'" > MAC.sh
   ```

2. **Test it:**
   Run the script and verify it looks like a standard MAC address format.
   ```bash
   bash MAC.sh
   ```
