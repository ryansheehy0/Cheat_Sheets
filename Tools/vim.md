[Home](../README.md)

# Vim commands
- This will only cover the commands I use the most

<!-- TOC -->

- [Movement](#movement)
- [Save/Quit](#savequit)
- [Comment/Uncomment](#commentuncomment)
- [Increment numbers](#increment-numbers)
- [Uppercase and Lowercase](#uppercase-and-lowercase)
- [Modes](#modes)
- [Delete](#delete)
- [Change](#change)
- [Undo and redo](#undo-and-redo)
- [Copy, Paste, and Cut](#copy-paste-and-cut)
- [Find on page/Search](#find-on-pagesearch)
	- [Special characters in replace](#special-characters-in-replace)
- [Macros](#macros)
- [Swp files](#swp-files)

<!-- /TOC -->

## [Movement](#vim-commands)

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
| zt         | Put cursor at the top                     |
| <          | Remove indent                             |
| >          | Indent                                    |
| g + j      | Move down one line without the line break |
| g + k      | Move up one line without the line break   |
| g + 0      | Beginning of line without the line break  |
| g + $      | End of line without the line break        |
| e          | Move to the end of a word                 |

## [Save/Quit](#vim-commands)

|      |                       |
|------|-----------------------|
| :w   | save                  |
| :q   | quit                  |
| :wq  | save and quit         |
| :wq! | force a save and quit |

## [Comment/Uncomment](#vim-commands)

|           |              |
|-----------|--------------|
| ctrl + v  | select lines |
| shift + i | comment      |
| esc       |              |

## [Increment numbers](#vim-commands)

|                                     |                                            |
|-------------------------------------|--------------------------------------------|
| ctrl + v                            | select lines                               |
| ctrl + v then shift + I             | Insert in front of the lines you selected. |
| select numbers then ctrl + a        | increment number by 1                      |
| select numbers then ctrl + x        | decrement number by 1                      |
| select numbers then g then ctrl + a | progressively increment. 1 2 3 4 etc.      |
| select number then g then ctrl + x  | progressively decrement. 4 3 2 1 etc.      |

## [Uppercase and Lowercase](#vim-commands)

|                       |           |
|-----------------------|-----------|
| select then shift + u | Uppercase |
| select then u         | Lowercase |

## [Modes](#vim-commands)

|     |                              |
|-----|------------------------------|
| i   | insert mode                  |
| o   | insert line below and i mode |
| O   | insert line above and i mode |
| a   | insert to the right          |
| esc | back to command/normal mode  |
| v   | visual mode                  |

## [Delete](#vim-commands)

|    |                                               |
|----|-----------------------------------------------|
| dd | delete line and copy line to default register |
| x  | delete where your cursor is at                |

## [Change](#vim-commands)

|           |                |
|-----------|----------------|
| c         | change         |
| c + i + w | change in word |
| r         | replace letter |

## [Undo and redo](#vim-commands)

|          |                    |
|----------|--------------------|
| u        | undo               |
| ctrl + r | redo               |
| .        | redo command again |

## [Copy, Paste, and Cut](#vim-commands)

|              |                               |
|--------------|-------------------------------|
| yy           | copy line to default register |
| p            | paste below default register  |
| P            | paste above default register  |
| " + char + y | copy to char register         |
| " + char + p | paste from char register      |
| " + +        | clipboard register            |

## [Find on page/Search](#vim-commands)

|                                     |                                                                      |
|-------------------------------------|----------------------------------------------------------------------|
| / + regex + enter                   | Search forward on page                                               |
| ? + regex + enter                   | Search backward on page                                              |
| n                                   | got to next                                                          |
| N                                   | go back one                                                          |
| :noh                                | remove highlight                                                     |
| :let @/=''                          | remove the current search                                            |
| :s/regex/replace                    | search and replace. You can also do this for selected text.          |
| f + character                       | Go to the next occurrence of that character in the current line.     |
| shift + f + character               | Go to the previous occurrence of that character in the current line. |
| s/\\(.\\)$/\1 add to end of lines/g | Add something to the end of selected lines                           |
| s/\\(^.*$\\)$/Begin \1 End/g        | Add something to beginning and  end of selected lines                |

### [Special characters in replace](#vim-commands)

|      |                                   |
|------|-----------------------------------|
| `\r` | New line                          |
| `\u` | Uppercase the following character |

## [Macros](#vim-commands)

|                      |                                 |
|----------------------|---------------------------------|
| q + macro + keys + q | record keys and put it in macro |
| @ + macro            | play macro                      |

## [Swp files](#vim-commands)

|           |                                                                                                                     |
|-----------|---------------------------------------------------------------------------------------------------------------------|
| (O)pen    | Read only mode                                                                                                      |
| (E)dit    | The last save                                                                                                       |
| (R)ecover | Read in all data. Need to delete .swp file after. Use when .swp file contains changes you know you want to restore. |
| (Q)uit    | Quits the 1st command for vim. Same as abort if only opening 1 file                                                 |
| (A)bort   | Go back to terminal                                                                                                 |
