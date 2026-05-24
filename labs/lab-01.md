## First Exercise - Getting Comfortable with Common Commands
Checking out the system setup. Using ls and ls -l to view folder structures and permissions, alongside identity commands like whoami, pwd, and uname to verify the host environment.

![Screenshot](/assets/lab-01-1.png)

---

Exploring shell behavior. Testing command history, checking environment variables ($PATH, $HISTSIZE), and using which and type to see the difference between built-in shell features (cd) and standalone programs (date).

![Screenshot](/assets/lab-01-2.png)

---

Working with shortcuts and paths. Viewing system shortcuts using alias, searching for files inside /bin, and using backticks (`...`) to quickly pull the current system date into an echo statement.

![Screenshot](/assets/lab-01-3.png)

---

Testing how different quotes change shell outputs. Comparing how backticks (`...`) and $() successfully run the date command inside a string, while single quotes (') and backslashes (\) treat the command as plain text.

![Screenshot](/assets/lab-01-4.png)

---

Testing wildcards and execution logic. Showing how * expands to match folder names, followed by a breakdown of chain commands using semicolons (;), logical AND (&& runs next only if the last one succeeds), and logical OR (|| runs next only if the last one fails).

![Screenshot](/assets/lab-01-5.png)
