[Home](./README.md)

# Vim commands
- This will only cover the commands I use the most

## Table of Contents

<!-- TOC -->

- [Vim commands](#vim-commands)
  - [Table of Contents](#table-of-contents)
  - [Movement](#movement)
  - [Save/Quit](#savequit)
  - [Comment/Uncomment](#commentuncomment)
  - [Increment numbers](#increment-numbers)
  - [Modes](#modes)
  - [Delete](#delete)
  - [Change](#change)
  - [Undo and redo](#undo-and-redo)
  - [Copy, Paste, and Cut](#copy-paste-and-cut)
  - [Find on page/Search](#find-on-pagesearch)
  - [Macros](#macros)
  - [Swp files](#swp-files)

<!-- /TOC -->

## [Movement](#table-of-contents)

|            |                                           |
|------------|-------------------------------------------|
| h          | left                                      |
| j          | down                                      |
| k          | up                                        |
| l          | left                                      |
| gg         | go to top                                 |
| G          | go to bottom                              |
| w          | next word                                 |
| b          | back a word                               |
| : + number | go to line number                         |
| 0          | Move to beginning of line                 |
| $          | Move to end of line                       |
| zz         | Center cursor                             |
| <          | Remove indent                             |
| >          | Indent                                    |
| g + j      | Move down one line without the line break |
| g + k      | Move up one line without the line break   |
| g + 0      | Beginning of line without the line break  |
| g + $      | End of line without the line break        |
| e          | Move to the end of a word                 |

## [Save/Quit](#table-of-contents)

|      |                       |
|------|-----------------------|
| :w   | save                  |
| :q   | quit                  |
| :wq  | save and quit         |
| :wq! | force a save and quit |

## [Comment/Uncomment](#table-of-contents)

|           |              |
|-----------|--------------|
| ctrl + v  | select lines |
| shift + i | comment      |
| esc       |              |

## [Increment numbers](#table-of-contents)

|                 |                                       |
|-----------------|---------------------------------------|
| ctrl + v        | select lines                          |
| ctrl + a        | increment number by 1                 |
| ctrl + x        | decrement number by 1                 |
| g then ctrl + a | progressively increment. 1 2 3 4 etc. |
| g then ctrl + x | progressively decrement. 4 3 2 1 etc. |

## [Modes](#table-of-contents)

|     |                              |
|-----|------------------------------|
| i   | insert mode                  |
| o   | insert line below and i mode |
| O   | insert line above and i mode |
| a   | insert to the right          |
| esc | back to command/normal mode  |
| v   | visual mode                  |

## [Delete](#table-of-contents)

|    |                                               |
|----|-----------------------------------------------|
| dd | delete line and copy line to default register |
| x  | delete where your cursor is at                |

## [Change](#table-of-contents)

|           |                |
|-----------|----------------|
| c         | change         |
| c + i + w | change in word |
| r         | replace letter |

## [Undo and redo](#table-of-contents)

|          |                    |
|----------|--------------------|
| u        | undo               |
| ctrl + r | redo               |
| .        | redo command again |

## [Copy, Paste, and Cut](#table-of-contents)

|              |                               |
|--------------|-------------------------------|
| yy           | copy line to default register |
| p            | paste below default register  |
| P            | paste above default register  |
| " + char + y | copy to char register         |
| " + char + p | paste from char register      |
| " + +        | clipboard register            |

## [Find on page/Search](#table-of-contents)

|                       |                                                                      |
|-----------------------|----------------------------------------------------------------------|
| / + regex + enter     | Search forward on page                                               |
| ? + regex + enter     | Search backward on page                                              |
| n                     | got to next                                                          |
| N                     | go back one                                                          |
| :noh                  | remove highlight                                                     |
| :s/regex/replace/g    | search and replace. You can also do this for selected text.          |
| f + character         | Go to the next occurrence of that character in the current line.     |
| shift + f + character | Go to the previous occurrence of that character in the current line. |

## [Macros](#table-of-contents)

|                      |                                 |
|----------------------|---------------------------------|
| q + macro + keys + q | record keys and put it in macro |
| @ + macro            | play macro                      |

## [Swp files](#table-of-contents)

|           |                                                                                                                     |
|-----------|---------------------------------------------------------------------------------------------------------------------|
| (O)pen    | Read only mode                                                                                                      |
| (E)dit    | The last save                                                                                                       |
| (R)ecover | Read in all data. Need to delete .swp file after. Use when .swp file contains changes you know you want to restore. |
| (Q)uit    | Quits the 1st command for vim. Same as abort if only opening 1 file                                                 |
| (A)bort   | Go back to terminal                                                                                                 |
