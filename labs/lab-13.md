# Groups, Permissions, Directories
In this lab exercise, I learned how to modify group permissions for directories, and files within directories.

---

### Navigation to the /tmp directory is followed by the creation of priv-dir and pub-dir, each containing a respective text file. The command chmod o-rx priv-dir/ is then applied to revoke read and execute permissions from other users, which is verified using ls -ld.
![Screenshot](/assets/lab-13-1.png)

### Universal write permissions are granted to pub-dir using chmod o+w, and access to priv-dir/priv-file is restricted to the owner only via chmod g-rw,o-r. A shell script named test.sh is then created using an echo redirect, though initial execution attempts trigger a "Permission denied" error.
![Screenshot](/assets/lab-13-2.png)

### User execute rights are added to test.sh with chmod u+x to successfully run the script and display system metadata via stat. The file's permissions are subsequently updated to octal 775, followed by a switch to the root user account to access the /tmp directory.
![Screenshot](/assets/lab-13-3.png)

### Operating under the root account, chown is used to change the ownership of pub-dir to root:root and the owner of pub-dir/pub-file to bin. The session concludes by executing chgrp -R users priv-dir, which recursively updates the group ownership of the private directory and its contents to users.
![Screenshot](/assets/lab-13-4.png)
