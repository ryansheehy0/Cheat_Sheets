# Linux

- ls
    - lists the contents of a directory
- mv
    - Moves/Cuts a file/Directory
- cp
    - Copies a file/Directory
- pwd
    - present working directory
- rm
    - rm file
    - rm -rf Directory
- mkdir
    - Make directory/folder
- touch
    - Make file
- cat
    - displays contents of a file
- grep
    - Searches for patterns in a file or input stream
- sed
    - text transformations on a file or input stream
- awk
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


### stream editor(sed)
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

#### Examples

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
