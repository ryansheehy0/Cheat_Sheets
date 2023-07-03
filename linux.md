[Home](./README.md)

# Linux

## Table of Contents
- [Most Common](#most-common)
    - [ls](#ls)
    - [cd](#cd)
    - [mv](#mv)
    - [cp](#cp)
    - [rm](#rm)
    - [mkdir](#mkdir)
    - [touch](#touch)


## Most Common
### ls
List information about a directory. The current directory is default.

|    |                           |
|----|---------------------------|
| -a | show hidden files/folders |
| -l | long listing format       |
| 

```
ls -ltc --time-style=+"%B-%d-%Y %I:%M %p"
    list files by time of last modifications and gives the last time of modification.
```

### cd
### mv
### cp
### rm
- rm file
- rm -rf Directory
### mkdir
### touch

## echo
## cat
- displays contents of a file

### grep
- Searches for patterns in a file or input stream
### sed
- text transformations on a file or input stream
### awk
- analyzes text files or input streams


- chmod
- chown
- find
- head
- tail
- tar
- gzip
- sort
- uniq
- wc
- gnu Parallel
- | << >>
    - pipes, appending text into file or re-writing text into file


## sed
Stream editor

sed {options} {script} {optional file}

| Options   | Description                                           |
|-----------|-------------------------------------------------------|
| -n        | Prints lines that match that pattern.                                        |
| -e        | Allows multiple find and replaces to a file. `sed -e 's/find/replace/' -e 's/find/replace/' filename` |
| -i        | Allows modifying the files directly.                  |
| -i.backup | Creates backup before modifying the file.             |

| Scripts                       | Description                                                                          |
|-------------------------------|--------------------------------------------------------------------------------------|
| s/ {regex} / {replacement} /  | Substitutes the first occurrence of the regex with the replacement text.             |
| s/ {regex} / {replacement} /g | Allows for more than one replacement on a line.                                    |
| / {regex} / {command}         | Runs the command only to the lines matching the regex.                               |
| / {regex} /d                  | Deletes the line that has the regex in it.                                           |
| {number}q                     | Prints the first number of lines of a file                                           |

- `#`s can also be used instead of the `/`s

```
sed -i.backup 's/foo/bar/g' file.txt
    Creates a backup called file.txt.backup and then replaces all occurrences of foo in file.txt to bar.

cat file.txt | sed 's/apple/orange/g' 
    Replaces all occurrences of apple with orange and outputs it to the terminal. Doesn't change file.txt at all.

sed 's/o/O/g' <file1.txt >file2.txt
    Reads in file1.txt, replaces o for O, and outputs that into file2.txt. Doesn't change file1.txt

man sed | sed '/replace/s/the/The/g'
    The lines that have "replace" on them have the "the"s changed to "The"s.
```

## Recursive size of folders in a directory
I want ls, but with recursively calculated sizes. Not just folders, but also files.

`du --max-depth=1 -h ./`
