# Working with Text Commands
In this lab exercise, I learned how to use commands like echo, cat, more, less, and others in order to configure txt files.

---

### Tested input/output redirection in the terminal. The log shows using echo to print text, > and >> to save or append it to a file, and find to search for files. It also demonstrates using 2> to send error messages into a separate log file.
![Screenshot](/assets/lab-06-1.png)

### Practiced modifying text case and linking commands together. The tr command converts text from lowercase to uppercase, while a pipe (|) sends a long ls file list directly into more for page-by-page scrolling.
![Screenshot](/assets/lab-06-2.png)

### Built a three-step command pipeline to clean up system data. First, usernames are isolated using cut (lab-06-3.png). Next, the names are alphabetized using sort. Finally, the list is sent into more to make it scrollable.
![Screenshot](/assets/lab-06-3.png)
![Screenshot](/assets/lab-06-4.png)
![Screenshot](/assets/lab-06-5.png)

### Compared different ways to read a file payload. Running cat dumps the entire file at once, while more pauses the screen for manual scrolling. Pressing 'h' opens the internal help guide inside the pager.
![Screenshot](/assets/lab-06-6.png)
![Screenshot](/assets/lab-06-7.png)
![Screenshot](/assets/lab-06-8.png)
![Screenshot](/assets/lab-06-9.png)

### I used head and tail to view specific chunks of text. The commands display just the very beginning or the very end of a file, using custom number flags to control exactly how many lines are shown on screen.
![Screenshot](/assets/lab-06-10.png)
![Screenshot](/assets/lab-06-11.png)

### I used grep to filter text with basic regular expressions. The examples show matching exact words, targeting patterns at the start (^) or end ($) of a line, and using the dot (.) wildcard to catch variable characters.
![Screenshot](/assets/lab-06-12.png)

### I utilized advanced grep options to find complex patterns. This shows searching for multiple words at once using an "OR" bar (|), filtering by number ranges, and matching exact blocks like three digits in a row. 

![Screenshot](/assets/lab-06-13.png)
![Screenshot](/assets/lab-06-14.png)

### Highlighted every instance of the word "bin"
![Screenshot](/assets/lab-06-15.png)
