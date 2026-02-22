# 🟢 Exercise 07: r_dwssap

## 📝 Objective
A complex formatting of `/etc/passwd`. Remove comments, keep every other line starting from the second, reverse logins, sort reverse alphabetical, extract a range between `$FT_LINE1` and `$FT_LINE2`, format with commas, and end with a period.

## 💡 The Logic
This is the ultimate pipeline challenge. You must link multiple small tools together.
* `cat /etc/passwd`: Get the file.
* `grep -v '^#'`: Remove comments.
* `awk 'NR % 2 == 0'`: Keep even lines.
* `cut -d: -f1`: Get the login names (column 1).
* `rev`: Reverse the strings.
* `sort -r`: Sort reverse alphabetically.
* `sed -n "$FT_LINE1,$FT_LINE2 p"`: Extract the specific line range.
* `paste -sd, -`: Join with commas.
* `sed 's/$/./'`: Add the period at the end.

## 🛠️ Step-by-Step Solution

1. **Create the shell script:**
   Use `echo` to redirect the giant pipeline into the file. Using single quotes on the outside allows the inner `$FT_LINE` variables to remain intact until the script is executed.
   ```bash
   echo 'cat /etc/passwd | grep -v "^#" | awk "NR % 2 == 0" | cut -d: -f1 | rev | sort -r | sed -n "$FT_LINE1,$FT_LINE2 p" | paste -sd, - | sed "s/,/, /g" | sed "s/$/./" | tr -d "\n"' > r_dwssap.sh
   ```

2. **Test it:**
   ```bash
   export FT_LINE1=7
   export FT_LINE2=15
   bash r_dwssap.sh
   ```
