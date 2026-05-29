## Linux User and Group Management Summary

## Linux Groups

### Purpose of Groups
Groups are mainly used to allow multiple users to share access to files and directories.

Example:
- Developers working on the same project
- Shared project folders
- Common permissions

---

## Viewing Groups

### Using `grep`
```bash
grep groupname /etc/group
```

Example:
```bash
grep root /etc/group
```

### Using `getent`
Works for both local and network-based groups.

```bash
getent group groupname
```

Example:
```bash
getent group root
```

---

## Creating Groups

### Basic Syntax
```bash
groupadd groupname
```

Example:
```bash
groupadd development
```

### Specify a GID
```bash
groupadd -g GID groupname
```

Example:
```bash
groupadd -g 1005 research
```

### Create a System Group
Creates a group with a lower reserved GID.

```bash
groupadd -r sales
```

---

## Group Naming Rules

Recommended rules:
- Start with:
  - lowercase letter (`a-z`)
  - underscore (`_`)
- Maximum:
  - 32 characters (16 recommended for compatibility)
- Allowed characters:
  - letters
  - numbers
  - hyphen (`-`)
  - underscore (`_`)
- Do NOT end with a hyphen (`-`)

---

## Modifying Groups

### Rename a Group
```bash
groupmod -n newname oldname
```

Example:
```bash
groupmod -n clerks sales
```

### Change Group ID (GID)
```bash
groupmod -g NEW_GID groupname
```

Example:
```bash
groupmod -g 10003 clerks
```

⚠ Warning:
Changing the GID can orphan files.

---

## Orphaned Files

Files become orphaned when:
- A group is deleted
- A GID changes
- A user is deleted

### Find Orphaned Group Files
```bash
find / -nogroup
```

---

## Deleting Groups

### Delete a Group
```bash
groupdel groupname
```

Example:
```bash
groupdel clerks
```

⚠ Important:
- Primary groups cannot be deleted
- Only supplemental groups can be deleted directly

---

## Important User Files

| File | Purpose |
|---|---|
| `/etc/passwd` | User account information |
| `/etc/shadow` | Encrypted passwords |
| `/etc/group` | Group information |
| `/etc/gshadow` | Secure group information |

---

## Useradd Default Settings

### View Defaults
```bash
useradd -D
```

Important defaults:
- Default group
- Home directory location
- Default shell
- Skeleton directory
- Password inactivity period

---

## `/etc/login.defs`

Contains system-wide defaults for:
- Password aging
- UID/GID ranges
- Home directory creation
- Password rules
- Encryption settings

### View Active Settings
```bash
grep -Ev '^#|^$' /etc/login.defs
```

---

## Creating Users

### Basic User Creation
```bash
useradd username
```

Example:
```bash
useradd jane
```

---

## User Creation Options

### Specify UID
```bash
useradd -u UID username
```

Example:
```bash
useradd -u 1000 jane
```

---

### Specify Primary Group
```bash
useradd -g groupname username
```

Example:
```bash
useradd -g users jane
```

---

### Add Supplementary Groups
```bash
useradd -G group1,group2 username
```

Example:
```bash
useradd -G sales,research jane
```

---

### Create Home Directory
```bash
useradd -m username
```

Example:
```bash
useradd -m jane
```

---

### Specify Home Directory
```bash
useradd -d /path/to/home username
```

Example:
```bash
useradd -md /test/jane jane
```

---

### Specify Custom Skeleton Directory
```bash
useradd -mk /custom/skel username
```

Example:
```bash
useradd -mk /home/sysadmin jane
```

---

### Specify Shell
```bash
useradd -s /bin/bash username
```

Example:
```bash
useradd -s /bin/bash jane
```

---

### Add Comment (Full Name)
```bash
useradd -c "Full Name" username
```

Example:
```bash
useradd -c "Jane Doe" jane
```

---

## Full User Creation Example

```bash
useradd -u 1009 -g users -G sales,research -m -c "Jane Doe" jane
```

This creates:
- UID: 1009
- Primary group: users
- Supplementary groups: sales, research
- Home directory
- Comment/full name

---

## Setting Passwords

### Set or Change Password
```bash
passwd username
```

Example:
```bash
passwd jane
```

### User Changes Own Password
```bash
passwd
```

---

## Good Password Practices

A strong password should:
- Be reasonably long
- Include:
  - uppercase letters
  - lowercase letters
  - numbers
  - symbols
- Avoid:
  - names
  - birthdays
  - phone numbers
  - personal information

---

## Password Aging with `chage`

### View Password Aging Info
```bash
chage -l username
```

### Set Maximum Password Age
```bash
chage -M days username
```

Example:
```bash
chage -M 60 jane
```

---

## Checking Logged-in Users

### Show Logged-in Users
```bash
who
```

### Detailed Session Info
```bash
w
```

### Login History
```bash
last
```

---

## Modifying Users

### Basic Syntax
```bash
usermod options username
```

---

### Change Username
```bash
usermod -l newname oldname
```

---

### Change Primary Group
```bash
usermod -g group username
```

---

### Replace Supplementary Groups
```bash
usermod -G groups username
```

⚠ Warning:
Using `-G` alone replaces all supplementary groups.

---

### Append Supplementary Groups
```bash
usermod -aG group username
```

Example:
```bash
usermod -aG development jane
```

---

### Lock Account
```bash
usermod -L username
```

### Unlock Account
```bash
usermod -U username
```

---

## Deleting Users

### Delete User Only
```bash
userdel username
```

Example:
```bash
userdel jane
```

⚠ Home directory remains and files become orphaned.

---

### Delete User + Home Directory + Mail Spool
```bash
userdel -r username
```

Example:
```bash
userdel -r jane
```

⚠ Files outside the home directory are NOT deleted.

---

## Important Concepts

### UPG (User Private Group)
- Some distributions automatically create a private group for each user.
- UID and GID usually match.

---

### System Accounts
Reserved for services/daemons.

Typical ranges:
- 1–99
- 1–499
- 1–999 (modern systems)

---

### Recommended UID/GID Range
- Start normal users/groups at:
  - 1000 or higher

---

## Common Commands Summary

| Command | Purpose |
|---|---|
| `groupadd` | Create group |
| `groupmod` | Modify group |
| `groupdel` | Delete group |
| `useradd` | Create user |
| `usermod` | Modify user |
| `userdel` | Delete user |
| `passwd` | Change password |
| `chage` | Manage password aging |
| `who` | Show logged-in users |
| `w` | Detailed login info |
| `last` | Login history |
| `find / -nogroup` | Find orphaned group files |

---

## Best Practices
- Use groups for shared access
- Avoid low UID/GID values for regular users
- Use strong passwords
- Set password expiration policies
- Use `-aG` when adding supplementary groups
- Be careful when deleting users/groups
- Regularly check for orphaned files
- Lock accounts instead of deleting when possible
