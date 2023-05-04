# Vim commands
- This will only cover the commands I use the most

## Movement
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

## Save/Quit
|      |                       |
|------|-----------------------|
| :w   | save                  |
| :q   | quit                  |
| :wq  | save and quit         |
| :wq! | force a save and quit |

## Comment/Uncomment
|           |              |
|-----------|--------------|
| ctrl + v  | select lines |
| shift + i | comment      |
| esc       |              |

## Increment numbers
|                 |                                       |
|-----------------|---------------------------------------|
| ctrl + v        | select lines                          |
| ctrl + a        | increment number by 1                 |
| ctrl + x        | decrement number by 1                 |
| g then ctrl + a | progressively increment. 1 2 3 4 etc. |
| g then ctrl + x | progressively decrement. 4 3 2 1 etc. |

## Modes
|     |                              |
|-----|------------------------------|
| i   | insert mode                  |
| o   | insert line below and i mode |
| O   | insert line above and i mode |
| a   | insert to the right          |
| esc | back to command/normal mode  |
| v   | visual mode                  |

## Delete
|    |                                               |
|----|-----------------------------------------------|
| dd | delete line and copy line to default register |
| x  | delete where your cursor is at                |

## Change
|           |                |
|-----------|----------------|
| c         | change         |
| c + i + w | change in word |
| r         | replace letter |

## Undo and redo
|          |                    |
|----------|--------------------|
| u        | undo               |
| ctrl + r | redo               |
| .        | redo command again |

## Copy, Paste, and Cut
|              |                               |
|--------------|-------------------------------|
| yy           | copy line to default register |
| p            | paste below default register  |
| P            | paste above default register  |
| " + char + y | copy to char register         |
| " + char + p | paste from char register      |
| " + +        | clipboard register            |

## Find on page
|                   |              |
|-------------------|--------------|
| ? + regex + enter | find on page |
| n                 | got to next  |
| N                 | go back one  |

## Macros
|                      |                                 |
|----------------------|---------------------------------|
| q + macro + keys + q | record keys and put it in macro |
| @ + macro            | play macro                      |

## Swp files
|           |                                                                                                                     |
|-----------|---------------------------------------------------------------------------------------------------------------------|
| (O)pen    | Read only mode                                                                                                      |
| (E)dit    | The last save                                                                                                       |
| (R)ecover | Read in all data. Need to delete .swp file after. Use when .swp file contains changes you know you want to restore. |
| (Q)uit    | Quits the 1st command for vim. Same as abort if only opening 1 file                                                 |
| (A)bort   | Go back to terminal                                                                                                 |