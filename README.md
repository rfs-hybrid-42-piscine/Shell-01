*This project has been created as part of the 42 curriculum by maaugust.*

<div align="center">
  <img src="https://raw.githubusercontent.com/rfs-hybrid/42-piscine-artwork/main/assets/covers/cover-shell01.png" alt="Shell 01 Cover" width="100%" />
</div>

<div align="center">
  <h1>🐚 Shell 01: Advanced Unix Commands & Piping</h1>
  <p><i>Mastering the Unix Pipeline, environment variables, regular expressions, and advanced text processing.</i></p>

  <img src="https://img.shields.io/badge/Environment-Linux%2FUnix-blue" alt="Environment badge" />
  <img src="https://img.shields.io/badge/Grade-100%2F100-success" alt="Grade badge" />
</div>

---

## 💡 Description
**Shell 01** is the second module of the C Piscine @ 42. While Shell 00 focused on basic terminal survival, this module dives deep into data manipulation, filtering, and shell scripting.

The primary goal of this project is to master the concept of the **Unix Pipeline (`|`)**, allowing the output of one command to be seamlessly passed as the input to another. It covers environment variables, complex file searching, string translation, regular expressions, and mathematical operations across custom numerical bases.

---

## 🧠 Exercise Breakdown & Logic

*The following section explains the core concepts and commands required to solve each exercise. It is designed to help future Pisciners understand the **why** behind the commands, rather than just copying and pasting them.*

### 🔹 File & Data Manipulation
| Exercise | Concept & Logic |
| :--- | :--- |
| **[`ex01: print_groups`](ex01)** | **Environment Variables:** Displaying a comma-separated list of groups for a specific user. <br><br>**Logic:** The `id` command can list user groups. Because the user is defined by the environment variable `$FT_USER`, we pass that to `id`. Then, we use the `tr` (translate) command to replace spaces with commas and strip out the trailing newline. |
| **[`ex02: find_sh`](ex02)** | **Advanced Searching:** Finding all `.sh` files but outputting *only* their names, without the extension or the path. <br><br>**Logic:** Instead of spawning a new process for every file, use `find . -type f -name '*.sh' -printf "%f\n"` to strip the path, and pipe that into `sed 's/\.sh$//'` to erase the extension. |
| **[`ex03: count_files`](ex03)** | **Counting Outputs:** Counting the total number of files and directories in the current path. <br><br>**Logic:** Use `find .` to list everything. Pipe that massive list directly into `wc -l` (word count by lines) to get the total number, and use `tr -d ' '` to trim any padding. |
| **[`ex04: MAC`](ex04)** | **Data Parsing & Regex:** Extracting only the MAC addresses from network configuration data. <br><br>**Logic:** Run `ifconfig -a` to dump all network interface data. Pipe it into `grep -oE` using a POSIX extended regular expression (`'([[:xdigit:]]{2}:){5}..'`) to aggressively hunt and extract *only* the strings that perfectly match the mathematical format of a MAC address. |
| **[`ex05: Can you create it?`](ex05)** | **Escape Characters & Attributes:** Creating a file with a highly unconventional name full of special characters, while matching specific permissions (`614`), exact byte size (2 bytes), and a forged timestamp. <br><br>**Logic:** The terminal interprets characters like `*`, `$`, `?`, and `\` as active commands or wildcards. To create a file literally named `"\?$*'MaRViN'*$?\"`, you must use strong quotes (`'`) and carefully escape specific characters so the shell reads them purely as text. Then, use `echo -n` to write exactly two bytes without a trailing newline, `chmod` for the `-rw---xr--` permissions, and `touch -t` for the specific `Oct 2 12:21` timestamp. |

### 🚀 Advanced Processing & Base Math (Optional)
| Exercise | Concept & Logic |
| :--- | :--- |
| **[`ex06: Skip`](ex06)** | **Alternating Lines:** Printing only every second line from an `ls -l` output. <br><br>**Logic:** This requires text processing tools. You can pipe the output of `ls -l` into `sed -n 'p;n'` or `awk 'NR%2==1'` to selectively print rows based on their line numbers. *(Note: The asterisks in the subject's example output mean file sizes and dates are variable; you don't need to spoof permissions here!)* |
| **[`ex07: r_dwssap`](ex07)** | **The Ultimate Pipeline:** A massive chain of commands to filter, reverse, and format the `/etc/passwd` file based on environment variables. <br><br>**Logic:** This is a test of pipeline endurance. <br>1. `cat /etc/passwd` to get the file. <br>2. `grep -v` to remove comments. <br>3. `awk` to keep every other line. <br>4. `cut` to isolate logins. <br>5. `rev` to flip the strings. <br>6. `sort -r` for reverse alphabetical. <br>7. `sed -n` to extract between `$FT_LINE1` and `$FT_LINE2`. <br>8. `paste`, `sed`, and `tr -d` to format with comma-spaces, append a period, and strip the final newline so it outputs precisely against the shell prompt. |
| **[`ex08: add_chelou`](ex08)** | **Base Conversions:** Adding two numbers formatted in entirely different, custom symbol bases. <br><br>**Logic:** <br>1. Use `tr` to translate the custom bases of `$FT_NBR1` and `$FT_NBR2` (both are in Base 5) into standard numeric digits (`01234`). <br>2. Set the output base (`obase=13`) *before* the input base (`ibase=5`) in `bc` (basic calculator). <br>3. Add them together. <br>4. Use `tr` one last time to translate the standard base-13 result into the requested `gtaio luSnemf` custom base. |

---

## 🛠️ Instructions

### 📦 Usage & Testing
Since these are Shell scripts, there is no compilation required. They must be executed using `/bin/sh`.

1. **Clone the repository:**
   ```bash
   git clone <your_repository_link>
   cd 42-Piscine/Shell01
   ```

2. **Testing with Environment Variables:**
   Several exercises in this module depend on environment variables. You must carefully export them in your terminal before running the script. Note that exercises like `add_chelou` require heavy escaping of special characters.
   
   ```bash
   # Example for ex01
   export FT_USER=bocal
   bash ex01/print_groups.sh

   # Example for ex07
   export FT_LINE1=7
   export FT_LINE2=15
   bash ex07/r_dwssap.sh
   
   # Example for ex08 (The "Salut" Test Case)
   export FT_NBR1=\\\'?\"\\\"\'\\
   export FT_NBR2=rcrdmddd
   bash ex08/add_chelou.sh
   ```

---

## 📚 Resources & References

The commands introduced in this module are extremely powerful. Familiarizing yourself with their manual pages is highly recommended.

* `man id` - For user and group identity.
* `man find` - For advanced file system searching.
* `man ifconfig` - For viewing network interfaces.
* `man wc` - For word, line, and byte counting.
* `man grep` - For pattern matching, text filtering, and POSIX regex classes.
* `man sed` & `man awk` - Essential stream editors for heavy text manipulation.
* `man tr` - For translating or deleting characters.
* `man bc` - For arbitrary precision math and base conversions.

### 🤖 AI Usage Guidelines
* **Code:** No AI-generated code was used to solve these exercises. All shell commands, scripts, and pipelines were manually crafted and tested to ensure a deep, practical understanding of the Unix system.
* **Documentation:** AI tools were utilized to structure this `README.md` and format the logic breakdowns to create a clean, accessible educational resource for fellow 42 students.
