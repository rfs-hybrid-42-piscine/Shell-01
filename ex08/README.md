# 🟢 Exercise 08: add_chelou

## 📝 Objective
Take two numbers provided in custom bases (from the `$FT_NBR1` and `$FT_NBR2` environment variables), add them together, and output the result in a third custom base.

## 💡 The Logic
This is a brutal test of base conversions and string manipulation.
1. `FT_NBR1` is in base 5 (`\'?"\!`).
2. `FT_NBR2` is also in base 5 (`mrdoc`).
3. The output must be in base 13 (`gtaio luSnemf`).

We must use `tr` to translate the custom symbols of both inputs into standard numeric digits (`01234`), do the math using `bc` (basic calculator) by setting the output base (`obase=13`) and input base (`ibase=5`), and finally use `tr` again to translate the standard base-13 result into the final `gtaio luSnemf` format.

*(Note: In `bc`, it is crucial to set `obase` BEFORE `ibase`. If you set `ibase=5` first, `bc` will interpret the `13` in `obase=13` as a base 5 number!)*

## 🛠️ Step-by-Step Solution

1. **The Pipeline Structure:**
   Translate inputs -> Convert to Base 10 -> Add -> Convert to Base 13 -> Translate to custom symbols.
   
   Because this command is a nightmare of quotes and backslashes, wrapping it in an `echo` string will break the escaping. Instead, we use `cat << 'EOF'`, which tells the terminal: *"Put everything I type on the next lines into `add_chelou.sh` until I type EOF"*.

   Run this exact block in your terminal:
   ```bash
   cat << 'EOF' > add_chelou.sh
   echo "obase=13; ibase=5; $(echo $FT_NBR1 | tr "\'\\\\\"?!" "01234") + $(echo $FT_NBR2 | tr "mrdoc" "01234")" | bc | tr "0123456789ABC" "gtaio luSnemf"
   EOF
   ```

3. **How to Test (The Legendary 42 Test Cases):**
   Testing this script requires heavy escaping because characters like `\`, `"`, and `!` mean specific things to the Bash terminal. Using single quotes (`'`) around your variables is the safest way to export them.

   **Test Case 1: "Salut"**
   ```bash
   export FT_NBR1=\\\'?\"\\\"\'\\
   export FT_NBR2=rcrdmddd
   bash add_chelou.sh
   ```
   *(Expected output: `Salut`)*

   **Test Case 2: The Easter Egg**
   
   This test case famously checks if you truly mapped your bases correctly. It does not actually crash your computer; the mathematical sum of these two variables translates exactly to the string "Segmentation fault" in the custom base 13!
   ```bash
   export FT_NBR1='\"\"!\"\"!\"\"!\"\"!\"\"!\"\"'
   export FT_NBR2='dcrcmcmooododmrrrmorcmcrmomo'
   bash add_chelou.sh
   ```
   *(Expected output: `Segmentation fault`)*
