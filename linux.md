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
  - [Find Commands](#find-commands)
  - [Computer commands](#computer-commands)
    - [Mount and Unmount drive](#mount-and-unmount-drive)
  - [Compression](#compression)
  - [sed](#sed)
  - [Recursive size of folders in a directory](#recursive-size-of-folders-in-a-directory)
  - [Curl](#curl)
  - [System Info](#system-info)
  - [Networking](#networking)

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

## [Installation](#table-of-contents)

| Command                 | Description        |
|-------------------------|--------------------|
| sudo dpkg -i ./file.deb | Install .deb files |

How to install other files

## [Package Manager](#table-of-contents)
- apt
- Flatpak
- AppImage
- Pacman
- Snap

| Command | Description                 |
|---------|-----------------------------|
| dpkg -l | List all installed packages |

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

## [Find Commands](#table-of-contents)

| Command                        | Description                                              |
|--------------------------------|----------------------------------------------------------|
| find filePath -iname fileName* | Finds files under filepath                               |

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

## [Curl](#table-of-contents)

Used to see the return from an api calls. Makes a get request form a URL.

```
curl https://api.github.com/users
```



## [System Info](#table-of-contents)
- df
- free

## [Networking](#table-of-contents)
- ping
- traceroute/tracepath