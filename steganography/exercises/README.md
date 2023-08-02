# File Analysis Exercises

## Tools

- file
- strings
- hexdump / xxd
- grep
- bgrep
- binwalk / foremost
- dd
- stegsolve
- zsteg
- steghide
- stegseek

## Exercise 1 - hidden in plain sight

Can you find a flag in the `lipsum.txt` file? Try using `grep` instead of just searching. `grep` by default returns the entire line containing the match - use `grep -o` to _only_ return the match.

<details>
<summary>Hint 1</summary>
<code>grep PATTERN lipsum.txt</code>
</details>

<details>
<summary>Hint 2</summary>
Try to <code>grep</code> for the flag format, i.e. <code>"DDC{.*}"</code>
</details>

## Exercise 2 - docx archive?

There are two flags hidden in the file `empty.docx`. Try to find out what the DOCX format really is!

<details>
<summary>Hint 1</summary>
Can you find a flag in the document itself when you open it?
</details>

<details>
<summary>Hint 2</summary>
Did you know that DOCX files (and other Office file types) are actually just ZIP archives?
</details>

<details>
<summary>Hint 3</summary>
Try unzipping the word document (possibly change the extension to .zip first) - can you find anything in the extracted files?
</details>

## Exercise 3 - ghost data

There is something different hidden in the file `ghost.png` - can you find two flags?

<details>
<summary>Hint 1</summary>
Maybe there is a flag hiding directly as text in the binary somewhere? How would you look for it?
</details>

<details>
<summary>Hint 2</summary>
Try running <code>strings</code> on the file and look for the flag with <code>grep</code>
</details>

<details>
<summary>Hint 3</summary>
Try some file carving techniques and see if there is one more file hiding
</details>

<details>
<summary>Hint 4</summary>
<code>binwalk</code> finds an additional PNG file. However, <code>binwalk -e</code> does not work in this case. When that happens, you can use <code>binwalk --dd=".*"</code> to force <code>binwalk</code> to extract everything it finds. You can then run <code>file</code> on each extracted file to see what they contain, and then give them the correct extension and open. Alternatively, you can use <code>foremost</code>, which in this case extracts the saved PNG.
</details>

### Exercise 4 - psyduck

Try browsing each bit plane for the RGB channels in the image `psyduck.png`. What can you see? In which plans and channels do you see it?

<details>
<summary>Hint</summary>
Open the image with <code>stegsolve</code>. Run with <code>java -jar Stegsolve.jar</code> if you have not renamed the file and created an alias.
</details>

### Exercise 5 - Hackerman

Are you a real hacker? See if there's anything hiding in `hackerman.jpg' to prove it! However, I don't think you'll get very far without my password!

<details>
<summary>Hint 1</summary>
The data is saved with <code>steghide</code>. What can you do without a password?
</details>

<details>
<summary>Hint 2</summary>
Try to bruteforce the password with <code>stegseek</code>. It requires a wordlist of passwords that <code>stegseek</code> can test. The most popular one is called <code>rockyou.txt</code>. There is a copy in the ZIP file <code>rockyou.zip</code> if you don't have it yourself.
</details>

<details>
<summary>Hint 3</summary>
The flag is base64 encoded
</details>
