[Home](./README.md)

# Simple Encryption

A simple non secure encryption that only allows writable ASCII characters used to obfuscate files.

## Writable ASCII characters:

|Decimal| Character |Dec|Char|Dec|Char|Dec|Char|Dec|Char|Dec|Char|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 32 |  space  |33 |    !    |34 |    "    |35 |    #    |36 |    $    |37 |    %    |
| 38 |    &    |39 |    '    |40 |    (    |41 |    )    |42 |    *    |43 |    +    |
| 44 |    ,    |45 |    -    |46 |    .    |47 |    /    |48 |    0    |49 |    1    |
| 50 |    2    |51 |    3    |52 |    4    |53 |    5    |54 |    6    |55 |    7    |
| 56 |    8    |57 |    9    |58 |    :    |59 |    ;    |60 |    <    |61 |    =    |
| 62 |    >    |63 |    ?    |64 |    @    |65 |    A    |66 |    B    |67 |    C    |
| 68 |    D    |69 |    E    |70 |    F    |71 |    G    |72 |    H    |73 |    I    |
| 74 |    J    |75 |    K    |76 |    L    |77 |    M    |78 |    N    |79 |    O    | 
| 80 |    P    |81 |    Q    |82 |    R    |83 |    S    |84 |    T    |85 |    U    |
| 86 |    V    |87 |    W    |88 |    X    |89 |    Y    |90 |    Z    |91 |    [    |
| 92 |    \    |93 |    ]    |94 |    ^    |95 |    _    |96 |    `    |97 |    a    |
| 98 |    b    |99 |    c    |100 |   d    |101 |   e    |102 |   f    |103 |   g    |
| 104 |   h    |105 |   i    |106 |   j    |107 |   k    |108 |   l    |109 |   m    |
| 110 |   n    |111 |   o    |112 |   p    |113 |   q    |114 |   r    |115 |   s    |
| 116 |   t    |117 |   u    |118 |   v    |119 |   w    |120 |   x    |121 |   y    |
| 122 |   z    |123 |   {    |124 |  \|    |125 |   }    |126 |   ~    |
| 9 | tab | 10 | new line |

## Steps:
1. Get input character
1. If the input character is a tab or new line then print it out and go to next character
1. Get password character
    - If the password is shorter than the input then the password wraps around to its beginning
1. Subtract 32 from input and password character
1. If encrypt
    - Add (input - 32) and (password - 32)
1. If decrypt
    - Subtract (input - 32) and (password - 32)
    - Add (127 - 32) to the result
1. Mod the result by (127 - 32)
1. Add 32 to the result
1. Print out the output character

## Example:

| | |
|:-|:-:|
|Input:| This |
|Password:| abc |


|Encrypt| | | |
|-|-|-|-|
| T: 84 - 32 = 52 | h: 104 - 32 = 72 | i: 105 - 32 = 73 | s: 115 - 32 = 83 |
| a: 97 - 32 = 65 | b: 98  - 32 = 66 | c: 99  - 32 = 67 | a: 97  - 32 = 65 | 
| 52 + 65 = 117   | 72 + 66 = 138    | 73 + 67 = 140    | 83 + 65 = 148    |
|117 % (127-32) = 22|138 % (127-32) = 43 |140 % (127-32) = 45 |148 % (127-32) = 53|
| 22 + 32 = 54 | 43 + 32 = 75 | 45 + 32 = 77 | 53 + 32 = 85 |
| 6 | K | M | U |


|Decrypt| | | |
|-|-|-|-|
| 6: 54 - 32 = 22 | K: 75 - 32 = 43 | M: 77 - 32 = 45 | U: 85 - 32 = 53 |
| a: 97 - 32 = 65 | b: 98  - 32 = 66 | c: 99  - 32 = 67 | a: 97  - 32 = 65 | 
| 22 - 65 = -43   | 43 - 66 = -23    | 45 - 67 = -22    | 53 - 65 = -12    |
| -43 + (127-32) = 52 | -23 + (127-32) = 72 | -22 + (127-32) = 73 | -12 + (127-32) = 83 |
|52 % (127-32) = 52|72 % (127-32) = 72 |73 % (127-32) = 73 |83 % (127-32) = 83|
| 52 + 32 = 84 | 72 + 32 = 104 | 73 + 32 = 105 | 83 + 32 = 115 |
| T | h | i | s |
