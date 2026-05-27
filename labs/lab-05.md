# Archiving and Zipping
In this lab exercise, I learned how to zip files in various different ways through the CLI.

---

Creating a backup directory (mybackups), packaging the /etc/udev directory into an uncompressed tarball (tar -cvf), and listing its contents (tar -tvf).

![Screenshot](/assets/lab-05-1.png)

Creating a compressed gzip tarball (tar -zcvf), comparing file sizes between compressed and uncompressed archives, and demonstrating extraction via tar -xvf.

![Screenshot](/assets/lab-05-2.png)

Verifying extracted directory structures and appending an additional file (/etc/hosts) to an existing uncompressed tar archive using the tar -rvf command.

![Screenshot](/assets/lab-05-3.png)

Compressing and decompressing a single file using various standard Linux compression utilities, including gzip, bzip2, and xz.

![Screenshot](/assets/lab-05-4.png)

Archiving files and directories into the standard ZIP format using zip and zip -r, followed by inspecting the archive contents without extracting using unzip -l.

![Screenshot](/assets/lab-05-5.png)

Removing the local etc directory copy and performing a clean extraction of the udev.zip file contents using the unzip utility.

![Screenshot](/assets/lab-05-6.png)
