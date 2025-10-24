# 2. ARMssembly 1

> For what argument does this program print `win` with variables 68, 2 and 3? File: chall_1.S Flag format: picoCTF{XXXXXXXX} -> (hex, lowercase, no 0x, and 32 bits. ex. 5614267 would be picoCTF{0055aabb})


## Solution:

- Primarily, the only problem faced in this challenge was deciphering the assembly code, so to move in a systematic order, I started by looking at the main function
- In the main function most of the registers were created, the most important part was `bl func`. Prior to this w0 was loaded so the value returned from func would moved into w0
- To find the value of w0, I then began viewing func function
- Over here, 68 was put into *(sp+16), 2 into *(sp+20), 3 into *(sp+24), the next line used `lsl` which shifts the bits of argument1 by argument2 values
- After shifting the new value obtained was 272 which was put into *(sp+28)
- 272 was then diveded by 3 by loading register *(sp+24) giving the value 90, then 90 was subtracted by the value to be entered by the user
- This brings us back to main function, where w0 is compared with 0. If the difference in w0 and 0 is not 0, then it will jump .LC4, which will display an error message
- However if it is equal to 0, it will print correct
- For it to be zero the entered value must be 90, after converting it into hexadecimal, I obtained the flag

```
func:
	sub	sp, sp, #32
	str	w0, [sp, 12]
	mov	w0, 68 ; 1000100
	str	w0, [sp, 16] ; This *(sp+16)=68
	mov	w0, 2
	str	w0, [sp, 20] ; *(sp+20)=2
	mov	w0, 3
	str	w0, [sp, 24] ; *(sp+24)=3
	ldr	w0, [sp, 20] ; 2
	ldr	w1, [sp, 16] ; 68
	lsl	w0, w1, w0 ; 100010000
	str	w0, [sp, 28] ;  *(sp+28)=272
	ldr	w1, [sp, 28] ; 272
	ldr	w0, [sp, 24] ; 3
	sdiv	w0, w1, w0 ; 272/3=90
	str	w0, [sp, 28] ; *(sp+28)=90
	ldr	w1, [sp, 28] ; 90
	ldr	w0, [sp, 12]
	sub	w0, w1, w0 ; 90-*(sp+12)
	str	w0, [sp, 28] *(sp+28)=90-*(sp+12)
	ldr	w0, [sp, 28]
	add	sp, sp, 32
	ret
	.size	func, .-func
	.section	.rodata
	.align	3

main:
	stp	x29, x30, [sp, -48]!
	add	x29, sp, 0
	str	w0, [x29, 28]
	str	x1, [x29, 16]
	ldr	x0, [x29, 16]
	add	x0, x0, 8
	ldr	x0, [x0]
	bl	atoi ; 
	str	w0, [x29, 44]
	ldr	w0, [x29, 44]
	bl	func ; 
	cmp	w0, 0 ; 
	bne	.L4 ; 
	adrp	x0, .LC0 ; 
	add	x0, x0, :lo12:.LC0
	bl	puts
	b	.L6 ; 
```

## Flag:

```
picoCTF{549698}
```

## Concepts learnt:

- I furthered my understanding on assembly language by solving and deciphering this flag
- I learned a lot of new instructions, `bl` which will return the value of function given to it, `bne` which branches to mentioned label if comparison in the above line is not equal, `adrp` calculates the adress of a register
- `lsl` which shifts the bits of operand1 by operand2, `sdiv` which divides 1st arg by 2nd and rounds down

## Notes:

- There is still a lot of assembly language I am yet to understand, and I need revision of the basics in the videos provided
- A method to verify the answer will be to run the code and enter 90 to see if the correct string is displayed

## Resources:

- https://www.youtube.com/watch?v=gh2RXE9BIN8
- https://www.youtube.com/watch?v=1d-6Hv1c39c
- https://www.youtube.com/playlist?list=PLMB3ddm5Yvh3gf_iev78YP5EPzkA3nPdL
- https://www.Google.com

## Incorrect Tangents:
- Did not face much of any errors in this challenge although I found it tedious to decipher the assembly, eventually by adding comments to the side I dug my way to the answer


***
