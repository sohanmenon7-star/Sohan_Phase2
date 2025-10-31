# 3. Bare Metal Alchemist

> my friend recommended me this anime but i think i've heard a wrong name.


## Solution:

- This challenge gave you a small hint in its name and a firmware.elf file which could be downloaded
- After downloading it the first task was to view this file but I needed more context before doing this. After browsing online I realized the hint indicated the type of file firmware.elf was, a bare metal elf file
- With this knowledge I began with using `readelf -h` to see the header(About the elf) of the elf file, This gave this output
```
ELF Header:
Magic:   7f 45 4c 46 01 01 01 00 00 00 00 00 00 00 00 00
Class:                             ELF32
Data:                              2's complement, little endian
Version:                           1 (current)
OS/ABI:                            UNIX - System V
ABI Version:                       0
Type:                              EXEC (Executable file)
Machine:                           Atmel AVR 8-bit microcontroller
Version:                           0x1
Entry point address:               0x0
Start of program headers:          52 (bytes into file)
Start of section headers:          8164 (bytes into file)
Flags:                             0x5, avr:5
Size of this header:               52 (bytes)
Size of program headers:           32 (bytes)
Number of program headers:         3
Size of section headers:           40 (bytes)
Number of section headers:         14
Section header string table index: 11
``` 
- I now know this file is an AVR 8-bit microcontroller machine
- Now I just needed to focus on obtaining the code, For this I learnt about a command `avr-objdump` on firmware.elf opening the entire assembly code of the file
- Looking throught this assembly was difficult but here is what I could understand of it
- In main, an input is given which undergoes bitwise operations(Doesnt really help)
- I then saw the .text section hoping to find a string(The flag) by using `-j` alongside `avr-objdump` but to no avail
- In search of other ways to access information, I stumbled across `simavr` which simulates microcontrollers in Linux
- After installing this and learning a little about it, I ran `simavr -g -m atmega328p -f 16000000 firmware.elf` in one terminal and then connected in the another terminal and then examined the memory.
- This gave me a lot of hex data, I converted this to readable language, Among the charaters I noticed the flag

## Flag:

```
TFCCTF{Th1s_1s_som3_s1mpl3_4rdu1no_f1rmw4re}
```

## Concepts learnt:

- I learned a lot about bare metal elf files and how to view the information in them
- I learnt about AVR microcontrollers although I did not understand a lot of it
- I learnt about opening and command related to AVR, `avr-objdump` to dissassemble it, `readelf` and some of it arguments like `-h` to view the header of the elf file
- On searching for ways to see the info in firmware.elf I also learnt a little about `simavr` and how to use it

## Notes:

- Likw the previous task with .elf files, There are other applications like ida and ghidra which can be used to solve this question. But again I ended up not needing them
- It is possible that you can use QEMU to find the answer but I was not able to 

## Resources:

- https://www.youtube.com/watch?v=XnoHXyb7dkY
- https://www.youtube.com/watch?v=Uf0KKh2zRuA
- https://www.youtube.com/watch?v=IyGwvGzrqp8
- https://docs.platformio.org/en/latest/plus/debug-tools/simavr.html
- https://stackoverflow.com/questions/49913745/how-to-run-a-bare-metal-elf-file-on-qemu
- https://www.google.com

## Incorrect Tangents:
- I struggled with understanding the assembly code a lot
- I initially found that you can view bare metal elf files using qemu, Although after trying that for a long time I gave up and ended up finding `avr-objdump`. As I said in the Notes, it may be possible that I just did not know enough about qemu and thus could not solve this using qemu


***
