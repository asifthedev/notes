## GREP

The `grep` stands for Global Regular Expression Print. It's a command used to search for a text string in a file or in multiple files across different directories.

```bash
$ grep <text> <file>
```

Let say I want to search for errors in my log files:-

```bash
$ grep "error" log.txt
```

It will display all the line containing the word `error`

**-i**

Let say I want perform case insensitive search, because maybe my file has word `Error` with capital `E` and I'm searching word `error` with small `e`

```bash
$ grep -i "error" log.txt
```

**Output:_**

![](C:\Users\mrasi\AppData\Roaming\marktext\images\2025-11-02-18-15-34-image.png)

**-n**

Let say you want to know the line number on which the word `error` is in the log file. 

```bash
$ grep -in "error" log.txt
```

**Output:_**

![](C:\Users\mrasi\AppData\Roaming\marktext\images\2025-11-02-18-14-14-image.png)

**-v**

In general in Linux the `-v` option refers the verbose but in grep that means return only the entries which are not contain the given string of text.

Let say I want to search for logs that are not have the word error in them in that case I can pass the word `error` with flag `-v`.

```bash
$ grep -v "error" log.txt
```

**Output:_**

![](C:\Users\mrasi\AppData\Roaming\marktext\images\2025-11-02-18-24-05-image.png)

But you can say Asif there's still the word `Error` in ouput, yes because we've never mention that we also want to exclude the error either it's with capital letters.

 By default it's consider case senstive search to make it case insensitive you can again pass the `-i` flag.

```bash
$ grep -vi "error" log.txt
```

**Output:_**

![](C:\Users\mrasi\AppData\Roaming\marktext\images\2025-11-02-18-27-50-image.png)

**-c**

It will return you the count of how many number of matches are found.

```bash
$ grep -c "error" log.txt
```

**Output:_**

![](C:\Users\mrasi\AppData\Roaming\marktext\images\2025-11-02-18-32-02-image.png)

## Recursive Search

If you want to search in all of the files and folders in an directory what you can do is you can pass the `-r` flag and the directory name

```bash
$ grep -rn "error" app
```

**Output:_**

![](C:\Users\mrasi\AppData\Roaming\marktext\images\2025-11-02-20-11-30-image.png)


