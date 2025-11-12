# Linux

Linux orignally a name used for Linux kernal made by Linus Torvalds, it's not an OS. When you combine linux kernal with GNU like tools and desktop enviornment then you have linux distribution, which you can say a Linux based OS.

## Root Directory

It’s the home directory for the root (superuser). Owned by the root user (administrator). Used to store configuration files or data for the root account.

It's denoted by forward slash `/`, if you write this command it will takes you to root directory if you are a superuser.

```shell
cd /
```

## Home Directory

Home directory is what contians files and folders for each individual user on the system. At this time we have only one user `asif` so to keep his files and folders seprated from the root and also other users we have a directory asif.

![](C:\Users\mrasi\AppData\Roaming\marktext\images\2025-10-30-08-52-07-image.png)

It's denoted by tilda symbol `~`. You can run this command and it will take you to the home directory and then you can see your current path is `~`

```shell
$ cd ~
```

![](C:\Users\mrasi\AppData\Roaming\marktext\images\2025-10-30-09-03-22-image.png) 

## Linux Command Structure

Every Linux command has three parts:-

```shell
$ command option argument
```

For example the cat command is used to display the content of any file in terminal:-

```shell
$ cat --numbre file.txt
```

Now here the `cat` is command, `--number` is an option which tels the cat to display line number, and`file.txt` is an argument. 

There is always a short way to specify an argument:-

```shell
$ cat -n file.txt
```

**Output:_**

```shell
> 1 I love code
> 2 I love coffe.
```

## Manual Pages

Every command in Linux has a manual page which servers as a documentation for a command, you can access manual page for any command using:-

```shell
$ man command
```

Let say you want to look at manual page for `cp` command:-

```shell
$ man cp
```

When you look throug the manual pages of different commands you can see something like this, in the terminal

```shell
$ cp [OPTION]... SOURCE... DIRECTORY 
```

The `[OPTION]` enclosed in brackets that mean it's optional, and three dots means you can pass more then one options same as with `SOURCE`

## Print Working Directory

If you want to know the path of current working directory you can use:-

```shell
$ pwd #print working directory
```

## List Command

It's used to list the content of a directory, if you run this command it will list down all files and folder present in the current working directory:-

```shell
$ ls
```

### Options in List Command

**-a**

Shows all files, including hidden ones (those starting with `.`)

```shell
$ ls -a
```

When you list with all you can see there are directories with the name of:

```shell
> . ..
```

The single `.` refers to the current working directory and the double dot `..` refers to the parent directory, you can even say:-

```shell
$ cd ..
```

and it will take you one directory back in hirarchy.

**-l**

Long format, shows details like permissions, owner, size, and date

```shell
$ ls -l
```

**Output:_**

```powershell
> drwxr-xr-x 2 mr asif      4096 Oct 29 21:52  windows
```

**-lh**

It work same as `l` the only difference is it shows the file size in human readable formate such as KBs, MBs etc.

**-lht**

The t options is refering to the time this command will sort the file and folders by time, and the newest files comes first in sorting.

**-lhtr**

The `r` stands for reverse it works same as `t` but oldest files comes first in sorting.

## File Timestamps

### Modification Time

Whenever you make any changes in the content in any of the file, Linux will record a modification time stamp, that you can see by running

```shell
$ ls -l
```

### Access Time

This is when the file was last read or accessed:-

```shell
$ ls -lu
```

**Output:_**

![](C:\Users\mrasi\AppData\Roaming\marktext\images\2025-10-30-12-06-56-image.png)

### Change Time

It records time stamp when  you move, file or change owner or permissions, in order to look at time stample change in the metadata of file you can use

```shell
$ ls -lc
```

## Creating Directories

The `mkdir` command which stands for make directory is used to create a new directory. The code snippet given below will create a new directory with the name `src`.

```shell
$ mkdir src
```

You can also create multiple directories by passing the name of multiple directories as an argument to `mkdir` command

```shell
$ mkdir src fonts
```

You can also create nested directories but it will show you an error if the parent folder not alread exists in this case `src` 

```shell
mkdir src/models
```

**Output:_**

```shell
mkdir: cannot create directory ‘src/models’: No such file or directory
```

It's because the `src`  does not exist but if you want that parent folder also get created then you can pass `-p` options and it will also create the `src` folder and inside it the `models`.

```shell
$ mkdir -p src/models
```

## Creating Files

You can use touch command to create new file/files. Touch will change the access and modifiation time once you touch any file using touch command.

```shell
$ touch index.js config.json
```

It will create two files `index.js` and `config.json`

## Checking File Type

To check the file type of any file you can `file` command and pass the file name as an argument as given below

```shell
$ file food.txt
```

Obviously it's a text file but sometime when the file type is'nt know then this command will helpfull to know the correct file type.

## Stats of Files

```bash
stat script.sh
```

It will show you: File Name, File Size (bytes), Access Time, Modification Time, Change Time, Birth Time.

## Renaming File & Directories

```bash
mv oldname newname
```

## Word Count

The `wc` command is used to count the number of lines, word and character in a file.

```bash
wc script.sh
```

**Output:_**

![](C:\Users\mrasi\AppData\Roaming\marktext\images\2025-11-02-16-44-30-image.png)

`1` - Number of lines

`3` - Number of words

`21` - Number of characters

**-l**

The `-l` is an option in `wc` command that when passed the wc only return you back the number of total lines.

```bash
$ wc -l file_name 
```

**-w**

Returns the totla number or words in file

```bash
$ wc -w file_name
```

**-m**

```bash
$ wc -m file_name
```
