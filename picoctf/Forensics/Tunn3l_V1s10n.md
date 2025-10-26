# 2. tunn3l v1s10n

> We found this file. Recover the flag.


## Solution:

- The question provides you with a file of an unknown type, so the first task was to figure out what the file type was
- I looked up how to do it, and I was told it could be done by looking at the hexvalue of the bits
- I downloaded HxD and put the file in it and the first four bytes would tell me about the file type. I found the provided file was a .bmp image file
- This file was corrupted so my next hurdle was to figure out how it was corrupted and fixing it
- The best thing I was told to do was compare it with an actual .bmp file, I compared the hex of myfile vs the an actual file and fixed the first few bytes as they were corrupted
- I could now open the image but it did not give me the flag. At this point I was stuck, No other info was given So I went back to the question for hints
- The challenge name was 'tunnel vision' which made me think if the image was cropped or zoomed in 
- I changed the height of the image after learning how to do so. This gave me the complete picture which had the flag present in it  

<img width="1137" height="307" alt="image" src="https://github.com/user-attachments/assets/47315c20-0700-4ae1-8e02-6cdd5f03e7dc" />
<img width="1331" height="417" alt="image" src="https://github.com/user-attachments/assets/38b67bba-6ea9-4022-8087-3604c50c728e" />
<img width="880" height="596" alt="image" src="https://github.com/user-attachments/assets/9b5e9525-7eae-4290-9d8e-e0d57453cfe7" />


## Flag:

```
picoCTF{qu1t3_a_v13w_2020}
```

## Concepts learnt:

- I learned a lot of things from this challenge, most importantly, reading the hex of a file to obtain a lot of information about it mainly the file type
- If the file type is an image, I learned how to view properties like image width, height, size and whether any of it is hidden or not
- If a file is corrupted, how to identify the corruption type is the most important as you can only proceed after that. An excellent way to do this is by comparing it to a not corrupted file
- Additionally, I learned that image files can be zoomed in to hide certain information and what a .bmp file(Bitmap)

## Notes:

- I tried to fix any corruptions using an online debugger which did end up working so if any time it is too tedious to compare corrupted files with actual ones, this is a viable option


## Resources:

- https://www.donwalizerjr.com/understanding-bmp/
- https://www.youtube.com/watch?v=giv0DQDSsjQ
- https://0xrick.github.io/lists/stego/#steganography
- https://www.google.com
- HxD64.exe application

## Incorrect Tangents:
- I first tried to see the filetype by using an online filetype determiner, this gave me an incorrect filetypeforcing me to learn about hex of a file to understand its filetype
- The major problem I faced was fixing the corruption, it wasnt until I compared it to an actual file that I could understand why it was corrupted
- While trying to adjust the filesize and fix it, I ended up corrupting the file further causing it to not display even for the correct parameters
- If the height of the image is set to be bigger than it can actually be, the image file will corrupt, I found an appropriate height which contained the flag by trial and error, landing on `3E 03 00 00`



***
