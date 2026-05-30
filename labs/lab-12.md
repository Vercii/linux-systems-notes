# User, Groups, and Modifications
I learned how to create user, groups, and how to modify details about them.

---

### Managing system groups with groupadd, groupmod, and groupdel, followed by verifying group details and displaying the default user creation configurations using useradd -D.
![Screenshot](/assets/lab-12-1.png)

### Modifying the system-wide default configuration settings for new user accounts by editing the /etc/default/useradd file within the nano text editor.
![Screenshot](/assets/lab-12-2.png)

### Updating default account inactivity settings using useradd -D -f 30, verifying the changes, and creating a new user account with specified supplementary group and comment fields.
![Screenshot](/assets/lab-12-3.png)

### Modifying an existing user's supplementary group memberships with usermod -aG, verifying password and account aging profiles using getent, and updating a user's password.
![Screenshot](/assets/lab-12-4.png)

### Removing a user account along with their home directory using userdel -r, and verifying the complete deletion by checking /etc/group.
![Screenshot](/assets/lab-12-5.png)
