# 3. m00nwa1k

> Decode this message from the moon.


## Solution:

- The challenge provided a .wav file, along with two hints
- The first hint read 'How were the picture sent from the moon to earth', upon searhing it I found out it was Radio signals. This gave me the clue that the .wav file is probably a radio signal
- The second clue said 'Who is mascot of CMU', which is Scotty. This hint did not make much sense until I saw how to read read .wav files. One of the methods was using the `scottie` tool. This made me realize what the hint was trying to say
- So I simply opened an online Scottie decoder, put the .wav file in it. This genrated an image with the flag in it 

<img width="962" height="700" alt="image" src="https://github.com/user-attachments/assets/c5f9f541-5cff-4fc3-aa00-6da743f8d769" />


## Flag:

```
picoCTF{beep_boop_im_in_space}
```

## Concepts learnt:

- I learned about Scottie which is a tool that can be used to read .wav files
- I learnt about encryption using .wav file which uses radio signals to hide the message

## Notes:

- .wav files can contain another files which can removed using tools such as scottie, but it might be possible to solve this question using a different tool

## Resources:

- https://sstv-decoder.mathieurenaud.fr/
- https://www.youtube.com/watch?v=giv0DQDSsjQ
- https://0xrick.github.io/lists/stego/#steganography
- https://www.google.com

## Incorrect Tangents:
- Without looking at the hints, Initially I thought you could read the flag by plotting the frequency graph which would directly show the answer required
- The mascots name was Scotty not Scottie which made me go on a wrong tangent


***
