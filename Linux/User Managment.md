# User Managment

There's is a fil on linux  `/etc/passwd` where you can see all different user on your system it shows the both system generated users and user generated user accounts.

If you run this code it will display the content inside our passwd file each line in this file represents a user on the system

```bash
mr@asif:/etc$ cat passwd
```

To count the number of user on your system you use wc command and it will count for you the number of lines in your etc file.

```bash
$ wc -l /etc/passwd
```

## Creating a New User

```bash
sudo useradd username
```

It will creates a user without home directory. To confirm user is created read your `passwd` file, there's must be a line for newly create user.

**Creating a User With Home Directory**

```shell
$ sudo useradd -m username
```

**--create-home**

You also use this flag for full form and more understanding of the command.

```bash
$ sudo useradd --create-home username
```

## Removing a User

```bash
sudo userdel username
```

It will remove the user but leaves behine their home directory.

**Remove user along with his files**

To remove user with his home directory also get removed.

```bash
sudo userdel --remove username
```

**Shorthand**

```bash
sudo userdel -r username
```

## How set a password for a user?

You are a super user and you've created a user as we've seen earlier, and now you want to change the password for that user, in order to do that you can run:

```bash
sudo passwd username
```

## How to change your password?

```bash
passwd
```

It will ask you for your previous password and then new password you want to setout and then it will change the old to new one.

## Creating System User

```bash
sudo useradd --system username
```

**Shorthand**

```bash
sudo useradd -r username
```
