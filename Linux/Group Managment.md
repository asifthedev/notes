# Group Managment

Groups users ko aik group karney kelye use hotey heyn, or user ko group karney k peachay ki reason hey k ham permissions management ko asan bana saktey heyn

Har user k aik specific files ki permissions allow karney sya behtar hey k aik specific type k user ka group bana diya jaye or phir permission ko us group ko assigne kia jaye to is tarah jo bhi bnda us group ka member hoga uko uskey group ki permission mill jaye gi.

For example you only want to allow your software engineer to access a specific type of softwares such as Git, VS Code and not everthing on your system, you can create a seprate group for them. Each user you add in this group have permission to all those software that you are allowd for that particular group

## Primary Group

Woh group jo user k name ka hota hey jab user bnta hey to uskay name say automatically aik group create kar diya jata hey, to is group ko primary group kaha jata hey.

## Secondary Group

Aik user multiple groups ka hisa ho skta hey primary group k elway jinay bhi group ka hisa aik user hota hey unhen secondary group kehtay heyn

## How to check which group you are the part of?

```bash
groups
```

Here are the list of all those groups your are the part of.

![](C:\Users\mrasi\AppData\Roaming\marktext\images\2025-11-03-10-48-16-image.png)

## How to check the number of group a specif user is part of?

```bash
groups username
```

## /etc/group

Yeah aik file hoti hey jis traha `/etc/passwd` mey sarey user ka record hota hey usi traha `/etc/group` sarey group ka hisab rakaha jata hey

If you run this command you will see the list of all different groups on your system:

```bash
cat /etc/group
```

Let's look at on of the group present in our `group` file,

![](C:\Users\mrasi\AppData\Roaming\marktext\images\2025-11-03-10-34-19-image.png)

It has four parts:

`scanner` - group name

`x` - is the group password (x just a representation for the hash password)

`115` - Group ID

`saned` - fourth part includes all the users part of this group.

## Creating a Group

```bash
sudo groupadd groupname
```

**cat /etc/passwd**

![](C:\Users\mrasi\AppData\Roaming\marktext\images\2025-11-03-10-38-26-image.png)

### Delete a Group

```bash
sudo groupdel groupname
```

## How add a user into a group?

To add a user into a group there are multiple wasy but we are going to user `usermod` command, which is used to modify an existing user.

```bash
sudo usermod -aG groupname username
```

**-a** means append

**-G** means group

`-aG`  are combined together

Here's a practical examaple:-

```bash
sudo usermod -aG sysadmin mr
```

### Adding user in a group using `gpasswd`

```bash
sudo gpasswd -a sysadmin mr
```


