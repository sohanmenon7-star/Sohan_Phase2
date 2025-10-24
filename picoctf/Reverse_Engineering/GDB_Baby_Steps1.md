# 1. GDB Baby Steps 1

> Can you figure out what is in the eax register at the end of the main function? Put your answer in the picoCTF flag format: picoCTF{n} where n is the contents of the eax register in the decimal number base. If the answer was 0x11 your flag would be picoCTF{17}.
Disassemble this(link to a file).


## Solution:

- Before I even began to solve this I needed to first understand and learn how to read the disassembled format, for which I viewed the refernce videos
- The first hurdle I faced was debugging the file using `objdump` on WSL as the file was downloaded on Windows
- I simply used `/mnt/c/users/` to access the files in my Windows
- After changing the directory to the one in which I stored the downloaded file, I used `objdump -d -Mintel debugger0_a | less`. This disassembled all the functions
- Then I searched for the main function and then looked for the `eax` register, a line read `mov eax, 0x86342`, since I know how to read assembly, I undesrstood that this is the value moved into the `eax` register
- After converting it into decimal, I obtained my answer

```
root@DESKTOP-AFFIDQC:~# cd /mnt/c/Users/SOHAN
root@DESKTOP-AFFIDQC:/mnt/c/Users/SOHAN# ls
 -1.14-windows.xml
 AppData
'Application Data'
 Contacts
 Cookies
 Documents
 Downloads
 Favorites
 IntelGraphicsProfiles
 Links
'Local Settings'
'Muse Hub'
 Music
'My Documents'
 NTUSER.DAT
 NTUSER.DAT{a2232d02-f513-11ef-92b9-8d2b0ef9d8f0}.TM.blf
 NTUSER.DAT{a2232d02-f513-11ef-92b9-8d2b0ef9d8f0}.TMContainer00000000000000000001.regtrans-ms
 NTUSER.DAT{a2232d02-f513-11ef-92b9-8d2b0ef9d8f0}.TMContainer00000000000000000002.regtrans-ms
 NetHood
 OneDrive
 Pictures
 PrintHood
 Recent
'Saved Games'
 Searches
 SendTo
'Start Menu'
 Templates
 Videos
 bluej
 ntuser.dat.LOG1
 ntuser.dat.LOG2
 ntuser.ini
root@DESKTOP-AFFIDQC:/mnt/c/Users/SOHAN# objdump -d -Mintel debugger0_a | less
root@DESKTOP-AFFIDQC:/mnt/c/Users/SOHAN# cd Desktop
-bash: cd: Desktop: No such file or directory
root@DESKTOP-AFFIDQC:/mnt/c/Users/SOHAN# cd cookies
root@DESKTOP-AFFIDQC:/mnt/c/Users/SOHAN/cookies# ls
DNTException  ESE  Low  PrivacIE  container.dat  deprecated.cookie
root@DESKTOP-AFFIDQC:/mnt/c/Users/SOHAN/cookies# cd ../.
root@DESKTOP-AFFIDQC:/mnt/c/Users/SOHAN# cd OneDrive
root@DESKTOP-AFFIDQC:/mnt/c/Users/SOHAN/OneDrive# cd Desktop
root@DESKTOP-AFFIDQC:/mnt/c/Users/SOHAN/OneDrive/Desktop# cd Cryptonite
root@DESKTOP-AFFIDQC:/mnt/c/Users/SOHAN/OneDrive/Desktop/Cryptonite# cd PicoCTF
root@DESKTOP-AFFIDQC:/mnt/c/Users/SOHAN/OneDrive/Desktop/Cryptonite/PicoCTF# objdump -d -Mintel debugger0_a | less
```

## Flag:

```
picoCTF{549698}
```

## Concepts learnt:

- Considering how I am new to the world of Reverse Engineering, I learnt everything from scratch
- I learned what reverse engineering is, various instructions in assembly like `mov`, `cmp` etc.
- Importantly, I learned how to disaasemble Binary code using `objdump` in WSL, additionally I learned how to access files in my Windows in WSL using `mnt`
- I learned about registers in assembly, `AX CX BX DX EAX RAX` and how to write a code line in assembly with the format, <instruction> <operand1>, <operand2> ; <comments>

## Notes:

- In one of the reference videos, it was told that to disassemble, something called `ida` is useful, since `objdump` can be a little tricky for someone to read. I attempted to use that but since it needed to be downloaded, I settled for objdump as this file was not that complex. In the future If I need its simplicity, I will consider downloading and using it.

## Resources:

- https://www.youtube.com/watch?v=gh2RXE9BIN8
- https://www.youtube.com/watch?v=1d-6Hv1c39c
- https://www.youtube.com/playlist?list=PLMB3ddm5Yvh3gf_iev78YP5EPzkA3nPdL

## Incorrect Tangents:
- After objdumping the file, I ended up looking at the wrong function, specifically the one at the top, this happened due to negligience which I have to avoid in future tasks
- Similarily, On converting the hexadecimal to decimal, I added a , which gave me the wrong flag error


***


.
