# File Analysis Exercises

## Tools

- file
- strings
- hexdump / xxd
- hexedit / ghex / HxD / Hex Fiend
- base64
- exiftool
- pngcheck

## Exercise 1 - encodings

Decode the following:

    001101010011000000100000001101000011000100100000001101010011010000100000001101010011100000100000001101010011000000100000001101010011000000100000001100110011100100100000001101100011000100100000001110010011100000100000001101010011000100100000001101000011001100100000001101100011001000100000001110010011100000100000001100010011000100110000001000000011000100110001001101100010000000110101001100000010000000110110001110000010000000110001001100000011100000100000001110000011010100100000001101010011001100100000001101000011100100100000001101000011001000100000001101100011010100100000001101110011000100100000001101010011001000100000001101000011001100100000001101100011001100100000001101000011000100100000001101000011011100100000001100110011010100100000001101010011000000100000001101000011000100100000001100010011000100110111001000000011000100110000001100000010000000110101001101100010000000110100001110010010000000110100001100100010000000110110001101010010000000110110001101010010000000110101001100110010000000110100001100110010000000110110001100110010000000110011001100110010000000111001001100010010000000110111001110010010000000110101001100000010000000110110001110000010000000110111001100100010000000110110001100010010000000110101001100010010000000110101001100000010000000111001001100110010000000110001001100010011010100100000001100010011000100110000001000000011010100110100001000000011010000110011001000000011011000110011001000000011001100110011001000000011000100110000001100000010000000111000001100100010000000110101001100000010000000110110001110000010000000111001001100000010000000110111001100110010000000110101001100010010000000110100001110000010000000110001001100000011000000100000001100110011100000100000001101010011011000100000001101010011001000100000001101000011001100100000001101100011001000100000001100010011000100110111001000000011010100110000001000000011001100110111001000000011010100110000001000000011011000111000001000000011100000110001001000000011011000110111001000000011010100110001001000000011010100110000001000000011100100110011001000000011000100110001001101100010000000110011001101110010000000110110001100010010000000110100001100110010000000110110001100100010000000110001001100010011011100100000001101000011010000100000001100110011010100100000001101010011000000100000001101100011100000100000001110010011100100100000001101110011100100100000001101010011001100100000001101010011000000100000001110010011001100100000001100010011000100110110001000000011001100110100001000000011011000110000001000000011010000110011001000000011011000110011001000000011001100110011001000000011100100110100001000000011100000110000001000000011010100110000001000000011010000110001001000000011000100110000001110000010000000111001001101000010000000110101001101010010000000110100001110010010000000110110001110010010000000111001001100100010000000111000001100110010000000110101001100100010000000110100001100110010000000110110001100100010000000110001001100010011011100100000001101010011000000100000001100110011011100100000001101010011000000100000001101100011100000100000001100010011000000111000001000000011100000110101001000000011010100110101001000000011010100110001001000000011001100110110001000000011010100111000001000000011001100110100001000000011010100110000001000000011010000110011001000000011011000110010001000000011100100110001001000000011011100111001

<details>
	<summary>Hint 1</summary>
	Decode from binary to ASCII (it's typically ASCII when we talk about decoding)
</details>

<details>
<summary>Hint 2</summary>
Decode result from decimal
</details>

<details>
<summary>Hint 3</summary>
Decode result from base85
</details>

<details>
<summary>Hint 4</summary>
Decode result from hex
</details>

<details>
<summary>Hint 5</summary>
Decode result from base64
</details>

## Exercise 2 - file extension

Try opening the file `funny_video.mp4`. What happens? Why?

<details>
<summary>Hint</summary>
Don't rely on extension, use <code>file</code>
</details>

## Exercise 3 - magic numbers

Files have a signature - a magic number - that determines the file type. `file` uses that magic number to identify the file type.

A list of file signatures can be found here: https://www.garykessler.net/library/file_sigs.html

1. What is the signature for PDF files in hex and in ASCII?

<details>
<summary>Hint</summary>
Search for "PDF" in the list of file signatures
</details>

---

In addition to a magic header, some files also have a trailer that ends the file.

2. What is the trailer for PNG files?

<details>
<summary>Hint</summary>
Search for "PNG" in the list of file signatures
</details>

---

3. The file signature for the `what_filetype` file has been changed slightly so that the magic bytes no longer match the actual file type. Try running `file what_filetype` and see what `file` outputs. Can you find the correct signature anyway and fix it so the file can be opened?

<details>
<summary>Hint 1</summary>
Make a hexdump or open the file in a hex editor to see what the first bytes are. Try searching for some of them in the list of file signatures and see if you can find an "almost" match.
</details>

<details>
<summary>Hint 2</summary>
The signature of the file after the change is <code>38 7A BC AF 27 11</code> and only the first and last bytes are changed.
</details>

<details>
<summary>Hint 3</summary>
Try using a hex editor to fix the two changed bytes. If you use <code>hexedit</code> you can save and close the file with <code>Ctrl+X</code>.
</details>

## Exercise 4 - metadata

When analyzing a file, it is important not only to look at the file's content, but also metadata - this can provide very valuable information about the file.

Take a look at the image `so_meta.jpg' and see if you can find anything interesting in the file's metadata.

<details>
<summary>Hint 1</summary>
Use <code>exiftool</code> to view the file's metadata
</details>

<details>
<summary>Hint 2</summary>
Check the field "XP Comment"
</details>

## Exercise 5 - corrupted file

The file `corrupted.png` appears to be corrupted and cannot be opened properly. `file` cannot identify the file type either. Try using the PNG specification (http://www.libpng.org/pub/png/spec/1.2/PNG-Contents.html) to assess what is wrong and fix it with a hex editor. The `pngcheck` tool can help to identify the errors.

<details>
<summary>Hint 1</summary>
Start by running <code>xxd corrupted.png</code> or open the file in a hex editor. Is the file's magic number correct? Compare with https://www.garykessler.net/library/file_sigs.html (search on PNG)
</details>

<details>
<summary>Hint 2</summary>
Try running <code>pngcheck</code> on the file once its magic byte has been fixed - what does <code>pngcheck</code> expect to find? And what do you find instead? Fix it!
</details>

<details>
<summary>Hint 3</summary>
Try running <code>pngcheck</code> on the file now - do you get a different error? Remember to find help in the PNG specification!
</details>

<details>
<summary>Hint 4</summary>
<code>pngcheck</code> complained about the IHDR length. IHDR is one of the different chunk types in PNG files. <a href="http://www.libpng.org/pub/png/spec/1.2/PNG-Structure.html#PNG-file-signature">PNG specs</a> tells you that each chunk consists of a 4-byte length, then a 4-byte chunk type, chunk data, and finally a 4-byte CRC. So it's the 4 bytes just before "IHDR" that it's crazy about.
</details>

<details>
<summary>Hint 5</summary>
IHDR length is currently <code>00 00 0B AD</code>, but what should it actually be? Again we use the PNG specification and find the page about <a href="http://www.libpng.org/pub/png/spec/1.2/PNG-Chunks.html#C.IHDR">IHDR Image Header</a> under "Chunk Specifications".

What does the IHDR chunk consist of? How many bytes in total? What should IHDR length be replaced with?

</details>

<details>
<summary>Hint 6</summary>
Now magic bytes, IHDR chunk type and IHDR chunk length are fixed. Try running <code>pngcheck</code> again. What do you get to know? Where should you fix the error? Either try searching for the wrong bytes in your hex editor or use the PNG specification to see where they are.
</details>
