# 1. Trivial Flag transfer protocol

> Figure out how they moved the flag.


## Solution:

- The question started off by giving me a .pcapng file, so the first hurdle was how to view this file. To view it I downloaded WireShark and uploaded the file to it which gave me all the data packets
- The data packets seen was available was extremely unreadable, but it was possible to filter out the TFTP objects
- After filtering it out I obtained two text files, 3 pictures and one .deb file
- Upon opening the text files, it was obvious that the text files were encrypted data. I ran these messages through an online decoder and found out it was encrypted with ROT13
- On decoding the messages, I found the hints, The flag was embedded into the one of the pictures and the password to the file was also given
- Then I searched up what embedding file in an image is called and learnt it was called steganogrpahy
- Looking up common tools for decryption of steganography, I found `steghide --extract -sf <filename>`
- Throught trial and error I found out the flag was present in picture3.bmp and put the password `DUEDILIGENCE` to extract the flag

<img width="952" height="307" alt="image" src="https://github.com/user-attachments/assets/ef17d569-4fe9-466c-b83c-2b8adeaeb0ea" />
<img width="1015" height="307" alt="image" src="https://github.com/user-attachments/assets/9e4ff984-ebd8-4a08-a576-5f76e793d955" />



```
root@DESKTOP-AFFIDQC:/mnt/c/users/SOHAN/OneDrive/Desktop/Cryptonite/PicoCTF/Forensics/TFTPFiles# steghide --extract -sf picture3.bmp -p DUEDILIGENCE
wrote extracted data to "flag.txt"
```

## Flag:

```
picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}
```

## Concepts learnt:

- Primarily, I learnt what steganogrphy is, encrypting files in images
- I learned how to read a .pcapng file using WireShark which will give all the data packets and it is possible to filter out the types of data packets
- I learned about ROT13 encryption
- I learned how to extract files from images using a command `steghide --extract -sf <filename> -p <password>` in the linux bash
- Additionally, I learned about `binwalk` and `foremost` which are also used for extraction. Also how to view .deb file

## Notes:

- The intended solve was to open the .deb file which told us we need to use steghide function to extract from the picture

## Resources:

- https://github.com/JohnHammond/ctf-katana?tab=readme-ov-file#forensics
- https://www.youtube.com/watch?v=giv0DQDSsjQ
- https://0xrick.github.io/lists/stego/#steganography
- https://www.google.com
- https://www.dcode.fr/rot-13-cipher

## Incorrect Tangents:
- Firstly while trying to read the .pcapng file, I was unable to view the pictures since the challenge is only compatible with WireShark 4.4.2 and not the latest version
- While trying to extract the file I tried using `binwalk` but that did not work
- I should have tried opening the .deb file since that gave me additional hints on the solution 


***
