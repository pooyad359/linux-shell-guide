# User Management

## Get List of Users

Users information is stored in `/etc/passwd`. You can see a list of the users by running `cat /etc/passwd`. Alternatively, you could use `getent passwd` to get a list of users.

### Normal Users

The list above contains system users. To only get a list of normal users you could filter them by UID. A normal user UID is from 1000 to 60000.

```bash
getent passwd {1000..60000}
```

_Note that root account has UID of 0._

## Switch User

Command `su` can be used to switch between users.

```bash
su <username>
```

### Flags

- `-l` or `-`: Provide an environment similar to what the user would expect had the user logged in directly. For instance, it moves to users home directory.

## Change Password

To change password you can use `passwd` command. To change password of current user just enter `passwd`. Then you will be asked to enter the current password, and then the new password, twice.
To switch another user's password add username after the command, e.g., `passwd user_name`

### Flags

- `-d`: Set the password of the user as blank (i.e., no password).

## TODO

- [ ] `adduser`
- [ ] `passwd`
- [ ] `userdel`
- [ ] `usermod`
- [ ] `deluser`
- [ ] `finger`
