---
id: NO-Q20240218234754772
aliases: []
---
Use MOV for registers that need exact values, LEA for offset ones

Always MOV the function number to AH

Template:
```
cseg segment para 'code'
assume cs:cseg, ds:cseg, es:cseg, ss:cseg
org 100h

; data declaration
; =======================

; =======================

start:
; assembly codes here

exit:
; exit/return codes here
int 20h

; subroutines
; =======================

; =======================

cseg ends
end start
```
# Interrupt 21h - characters, strings or any text

ASCII control characters:

| Hex | Dec | Description                                       |
| --- | --- | ------------------------------------------------- |
| 08h | 8   | Backspace (moves one column to the left)          |
| 09h | 9   | Horizontal tab (skips forward n columns)          |
| 0Ah | 10  | Line feed (moves to next output line)             |
| 0Ch | 12  | Form feed (moves to next printer page)            |
| 0Dh | 13  | Carriage return (moves to leftmost output column) |
| 1Bh | 27  | Escape character                                  |
## Function 1 - wait for key press

(no register)
## Function 2 - write character to STDOUT

DL = character to be printed
## Function 9 - write a $-terminated string to STDOUT

(DX) = offset of string to be printed
# Interrupt 10h - graphics mode

Attribute bits:

| BL | R | G | B | INT | R | G | B |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 0 | 0 | 0 | 1 | 1 | 0 | 0 | 0 |
| BACKGROUND | ===<br> | === | === | FOREGROUND | === | === | === |

| Dec | Hex | Binary | Color |
| ---- | ---- | ---- | ---- |
| 0 | 0 | 0000 | Black |
| 1 | 1 | 0001 | Blue |
| 2 | 2 | 0010 | Green |
| 3 | 3 | 0011 | Cyan |
| 4 | 4 | 0100 | Red |
| 5 | 5 | 0101 | Magenta |
| 6 | 6 | 0110 | Brown |
| 7 | 7 | 0111 | Light Gray |
| 8 | 8 | 1000 | Dark Gray |
| 9 | 9 | 1001 | Light Blue |
| 10 | A | 1010 | Light Green |
| 11 | B | 1011 | Light Cyan |
| 12 | C | 1100 | Light Red |
| 13 | D | 1101 | Light Magenta |
| 14 | E | 1110 | Yellow |
| 15 | F | 1111 | White |
## Function 0 - set video mode

AL = video mode

| Mode | Text/Graphics | Color | Size |
| ---- | ---- | ---- | ---- |
| 00h | Text | Greyscale | 40x25 |
| 01h | Text | Color | 40x25 |
| 02h | Text | Greyscale | 80x25 |
| 03h | Text | Color | 80x25 |

Shorthand for clearing the screen:
```
mov ah, 0
mov al, 03h
int 10h
```
or
```
mov ax, 0003h
int 10h
```
## Function 2 – set cursor position

BH = page number

DH = row

DL = column
## Function 9 – write character with attribute and repetition

AL = character to write

BH = page number

BL = attribute

CX = number of times to print character
## Function 0Ah – write character with repetition

AL = character to write

BH = page number

CX = number of times to print character
## Function 13h – write string with attribute

AL = write mode (default is 01h)

BH = page number

BL = attribute

CX = number of characters in string

DH = row

DL = column

(ES:BP) = offset of string
# Interrupt 20h - terminate program

Terminates execution of the program without returning status code.