# PieceTable
<<<<<<< HEAD
**Piece Table** is an efficent **Data Structure** that is used in **Text Editors**.<br />
=======
**Piece Table** is and efficent **Data Structure** that is used in **Text Editors**.<br />
>>>>>>> 35b0267... Update README.md
It is used for representing a series of edits on a text document. Piece Table provides an elegant solution for text buffers.
The piece table is the powerful data-structure behind many text editors, old and new. A key characteristic of the piece table is that it records all of the insertions we make to a file in an append-only manner.

Piece Table stores the text doucment as a sequence of **pieces of text** either from original buffer or add buffer. 

## Why we need PieceTable?
<<<<<<< HEAD
Basically when  the text document is represented using an array of string it creates a problem of appending in the middle of document as the document is of large size.
=======
Basically when text document is represented using an array of string it creates a problem of appending in the middle of document as the document is of large size.
>>>>>>> 35b0267... Update README.md
So elements needed to be shifted from the insertion point. There were also other problems of speeding up when files are opened and out of memory crashes. <br />
Piece Table uses two buffers:
* Original Buffer
* Add Buffer

## How Piece Table Works?
 As mentined earlier PieceTable uses two buffers-
 1. Original Buffer
 > A buffer to the original text document. This buffer is read-only. It contains the original data that is read from disk. 
 2. Add Buffer
 > A buffer to a temporary file. This buffer is append-only.It contains the data that is being added. Anything being added whether in middle, start, end or whatever postion it is added here.
 
 ##### But still how the data from two buffers are read?
 So we need information to store from which buffer data is read and how much data is to read.
 This information is stored on Piece Descriptor. It contains the three fields respectively:
 1. Source
 From which source information is to be read.
 2. Start
 from where we start reading the information in the choosen buffer.
 3. Length
 How many characters are to be read from the starting of the buffer.
 
 Let the Original text be "ABCDEF"
 The text to be added "GHI" after D. So output would be "ABCDGHIEF".
 
 Buffers | Data
------------ | -------------
Original | ABCDEF
Add | GHI

The below table describes the piece table
 
  Source | Start | Length
------------ | ------------- | -------------
Original | 0 | 4
Add | 0 | 3
Original | 4 | 2

So the Pieces are combined as 
=> ABCD
=> GHI
=> EF

This is how Insertion works.
Appending characters to the "add file" buffer, and Updating the entry in piece table (breaking an entry into two or three). <br />

Deletion works by only modifying the appropriate entry in piece table.
Suppose  we want to remove "HI" so output we need "ABCDGEF".
Since the piece table containg HI needed to modify.
Source | Start | Length
------------ | ------------- | -------------
Original | 0 | 4
Add | 0 | 1
Original | 4 | 2

So the Pieces are combined as 
=> ABCD
=> G
=> EF

However it is not removed from the Add buffer.
The text to be added or removed as part of an undo or redo is already there in one of the buffers, and we just need to update our piece descriptors to point to it once again.
<<<<<<< HEAD

=======
>>>>>>> 35b0267... Update README.md

### References
* https://darrenburns.net/posts/piece-table/
* https://code.visualstudio.com/blogs/2018/03/23/text-buffer-reimplementation
* https://en.wikipedia.org/wiki/Piece_table
