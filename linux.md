[Home](./README.md)

# Bash/Linux

## Table of Contents

<!-- TOC -->

- [Bash/Linux](#bashlinux)
  - [Table of Contents](#table-of-contents)
  - [Navigation](#navigation)
    - [Files types](#files-types)
  - [Changing Permissions](#changing-permissions)
  - [Miscellaneous](#miscellaneous)
  - [Installation](#installation)
  - [Package Manager](#package-manager)
    - [Advanced package toolapt](#advanced-package-toolapt)
  - [File and Directory Manipulation](#file-and-directory-manipulation)
  - [Find](#find)
  - [Computer commands](#computer-commands)
    - [Mount and Unmount drive](#mount-and-unmount-drive)
  - [Compression](#compression)
  - [sed](#sed)
  - [Recursive size of folders in a directory](#recursive-size-of-folders-in-a-directory)
  - [Networking](#networking)
    - [httprobe](#httprobe)
    - [Curl](#curl)
  - [Grep](#grep)
  - [System Info](#system-info)

<!-- /TOC -->

## [Navigation](#table-of-contents)

| Command | Description                               |
|---------|-------------------------------------------|
| pwd     | List current directory                    |
| cd      | Change directory                          |
| ls      | Lists what is in the directory            |
| ls -a   | Lists with hidden files/directories shown |
| ls -l   | List in the long way                      |

```
-rwxrwxrw- 1 root ryan 9999 May 22 00:01 FileName
^[^][^][^] ^ [ ^] [^ ] [^ ] Date of creation
| |  |  |  |   |   |    |
| |  |  |  |   |   |   Size in bytes
| |  |  |  |   |   group
| |  |  |  |   user
| |  |  |  Number of links to this file
| |  |  public
| |  group
| user
File types
```

|   | Description     |
|---|-----------------|
| r | Allow reading   |
| w | Allow writing   |
| x | Allow executing |
| - | Not allowed     |

| Location | Description          |
|----------|----------------------|
| ./       | In current directory |
| ~        | Home directory       |
| ../      | One directory up     |

### [Files types](#table-of-contents)

| File type | Description                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| -         | Regular file                                                                                            |
| d         | Directory/Folder                                                                                        |
| l         | Symbolic link. A reference to another file or directory                                                 |
| c         | Character device. Device which transfers data as a steam of bytes. (Inputs can be found in /dev/input/) |
| b         | Block device. Devices which transfer data in fixed size blocks.                                         |
| p         | Named pipe. First in, First out, used for inter-process communication.                                  |
| s         | Socket. Communication endpoints for inter-process communication.                                        |
| w         | Whiteout. Used for union file systems to mark entries which should be hidden.                           |

## [Changing Permissions](#table-of-contents)

| Command                     | Description                                                              |
|-----------------------------|--------------------------------------------------------------------------|
| chown user:group fileName   | Change user and group                                                    |
| chown -R user:group dirName | Recursively change the users and groups of al the files in the directory |
| chmod ### fileName          | Change permissions. r(4) w(2) x(1) -(0)                                  |

## [Miscellaneous](#table-of-contents)

| Command              | Description                                               |
|----------------------|-----------------------------------------------------------|
| sudo                 | Run command as super user                                 |
| !!                   | Run previous command                                      |
| su user              | Switch to that user                                       |
| cat file             | Outputs contents of a file                                |
| echo text            | Outputs text                                              |
| date                 | Show current date and time                                |
| ctrl + c             | Allows you to stop running the current program            |
| command1 && command2 | Run command1 and if that was successful than run command2 |
| wc fileName          | Counts the number of lines, words, and bytes in a file    |

## [Installation](#table-of-contents)

| Command                 | Description                 |
|-------------------------|-----------------------------|
| sudo dpkg -i ./file.deb | Install .deb files          |
| dpkg -l                 | List all installed packages |

How to install other files

## [Package Manager](#table-of-contents)
- apt
- Flatpak
- AppImage
- Pacman
- Snap

### [Advanced package tool(apt)](#table-of-contents)

| Command                      | Description                                                                            |
|------------------------------|----------------------------------------------------------------------------------------|
| sudo apt install packageName | Install packageName                                                                    |
| sudo apt remove packageName  | Uninstall packageName                                                                  |
| sudo apt update              | Update source list for packages. The source list can be found at /etc/apt/sources.list |
| sudo apt upgrade             | Updates all the installed packages                                                     |
| sudo apt search packageName  | Searches for packageName                                                               |
| sudo apt purge packageName   | Uninstalls and removes files of packageName                                            |
| sudo apt autoremove          | Removes all unneeded packages                                                          |

## [File and Directory Manipulation](#table-of-contents)

| Command                     | Description                                              |
|-----------------------------|----------------------------------------------------------|
| mkdir dirName               | Make directory                                           |
| touch fileName              | Make file                                                |
| rm fileName                 | Delete file                                              |
| rm -rf dirName              | Removes directory and everything within it               |
| rm dirName/*                | Removes everything in directory, but keeps the directory |
| cp fileName ./Dir/filename2 | Copies file to dir with new name                         |
| cp fileName ./Dir/          | Copies file to dir with same name                        |
| mv fileName destinationDir  | Moves file to destination directory                      |
| mv ./* dirPath              | Move all contents of current folder to another directory |

## [Find](#table-of-contents)

Used for finding files or directories

| Command                        | Description                                                  |
|--------------------------------|--------------------------------------------------------------|
| find filePath -iname fileName* | Finds files under filepath. Case insensitive                 |
| -type f                        | Only shows files                                             |
| -type d                        | Only shows directories                                       |
| -mmin -10                      | Find files that were modified less than 10 minutes ago       |
| -mmin +10                      | Find files that were modified more than 10 minutes ago       |
| -mtime -10                     | Find files that were modified less than 10 days ago          |
| -size +5M                      | Files over 5 megabytes                                       |
| -empty                         | Empty files                                                  |
| -perm ###                      | Find files with that permission                              |
| -maxdepth #                    | Sets a max depth for recursive searching through directories |
| -exec command                  | Executes a command on all of the files                       |

Examples:
- `find . -type f -exec chown user:group {} \;` Recursively changes the own of each file in a directory.
- `find . -type f -maxdepth 1 -name "*.jpg" -exec rm {} \;` Removes all .jpg files from a directory.

## [Computer commands](#table-of-contents)

| Command              | Description         |
|----------------------|---------------------|
| sudo restart         | Restart computer    |
| sudo shutdown -h now | Shutdown's computer |
| lspci -k             | List drivers        |

### [Mount and Unmount drive](#table-of-contents)
With some linux distros this happens automatically

1. Plug in drive
1. `sudo fdisk -l` find where drive is
1. `sudo mount filePathFromFdisk filePathMountFolder` mounts the drive
1. `sudo umount filePathMountFolder` unmounts the drive

## [Compression](#table-of-contents)

| Command              | Description         |
|----------------------|---------------------|
| unzip fileName | unzips .zip files |
| tar -czvf name.tar.gz fileName | Makes .tar.gz files |

- tar
- gzip


- sed
    - text transformations on a file or input stream
- awk
    - analyzes text files or input streams
- head
- tail
- tar
- gzip
- sort
- uniq
- gnu Parallel
- | << >>
    - pipes, appending text into file or re-writing text into file


## [sed](#table-of-contents)
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

## [Recursive size of folders in a directory](#table-of-contents)
I want ls, but with recursively calculated sizes. Not just folders, but also files.

`du --max-depth=1 -h ./`

## [Networking](#table-of-contents)
- ping
- traceroute/tracepath

### [httprobe](#table-of-contents)
httprobe is used to take a list of domains and probe for working HTTP and HTTPS servers.

`cat domains.txt | httprobe > results.txt`

### [Curl](#table-of-contents)

Used to get the return information from websites/apis. Makes a get request form a URL.

`curl https://api.github.com/users`

| Flags | Description                     |
|-------|---------------------------------|
| -i    | Returns the headers and content |
| -I    | Returns just the headers        |

## [Grep](#table-of-contents)

Grep is used for searching text in a file. Grep returns the lines that match a pattern, or the files that contain the pattern.

`grep -Flags pattern fileName`

| Flags | Description                                                                    |
|-------|--------------------------------------------------------------------------------|
| -w    | Just match the word and not words which just contain the pattern               |
| -i    | Case sensitive                                                                 |
| -n    | Gives line number                                                              |
| -A #  | Shows # of lines after the line which has the pattern                          |
| -B #  | Shows # of lines before the line which has the pattern                         |
| -C #  | Shows # of lines before and after the line which has the pattern               |
| -r    | Recursively search through a directory                                         |
| -l    | Just show the files which contain the match                                    |
| -c    | Shows all files and how many matches are in that file.                         |
| -P    | Allows for Pearl compatible expressions. Allows \d and other regex expressions |
| -v    | Inverse match                                                                  |
| -h    | Don't display the file name. Just the lines                                    |
| -H    | Display the file name and the lines.                                           |

If you don't want to recursively search through a directory you can do `grep pattern dirPath/*`

Examples:
- `grep -wirn "grep" .` Searches for lines with the word "grep" recursively in the current directory
- `grep -wirl "grep" .` Searches for files that contain the word "grep"
- `grep -wirc "grep" . | grep -v :0$` Search for files that contain the word "grep" and how many matches they have to the word "grep"

## [System Info](#table-of-contents)
- df
- free