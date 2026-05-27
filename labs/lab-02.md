# Linux Help Commands
In this lab exercise, I used various help commands and got comfortable with exploring the CLI.

---

Printing the current system date and using man -k password to search the manual pages for any commands related to passwords.

![Screenshot](/assets/lab-02-1.png)

Using the apropos password command to perform a keyword search across manual page descriptions, returning the exact same results as man -k.

![Screenshot](/assets/lab-02-2.png)

Viewing precise man page sections using man -f and man 5, using whatis to get quick command descriptions, and displaying short flag options with date --help.

![Screenshot](/assets/lab-02-3.png)

Listing the contents of the /usr/share/doc directory to see the available system and package documentation folders.

![Screenshot](/assets/lab-02-4.png)

Using locate and locate -b to quickly find paths containing "crontab" across the system database, followed by whereis to find binary, source, and man page locations for passwd.

![Screenshot](/assets/lab-02-5.png)

Looking at the internal help screen within a man page viewer (less), displaying shortcuts for jumping to specific lines, matching brackets, and searching text.

![Screenshot](/assets/lab-02-6.png)

Viewing man 5 passwd, which documents the structure and fields (like username, UID, and home directory) of the /etc/passwd file format.

![Screenshot](/assets/lab-02-7.png)

Running info date to open the GNU hypertext documentation viewer, providing a more detailed breakdown of the date command than a standard man page.

![Screenshot](/assets/lab-02-8.png)

Viewing the help screen inside the info documentation tool to learn the keyboard shortcuts for moving between nodes, levels, and hypertext links.

![Screenshot](/assets/lab-02-9.png)
