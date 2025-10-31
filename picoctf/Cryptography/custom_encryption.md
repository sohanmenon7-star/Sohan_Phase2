# 2. custom_encryption

> Can you get sense of this code file and write the function that will decode the given encrypted file content.
Find the encrypted file here flag_info and code file might be good to analyze and get the flag.


## Solution:

- In this challenge, two important hints were given, first I needed to make a python function second stated that the function needed to decrypt, this was to be done by understanding the encryption algorithm
- So I opened up the pythonfile which had the code, and the textfile which had the value of the cipher and 'a' and 'b'
```
from random import randint
import sys


def generator(g, x, p):
    return pow(g, x) % p


def encrypt(plaintext, key): # cipher_text, key
    cipher = []
    for char in plaintext: #ord() converts character into Unicode
        cipher.append(((ord(char) * key*311)))
    return cipher


def is_prime(p):
    v = 0
    for i in range(2, p + 1):
        if p % i == 0:
            v = v + 1
    if v > 1:
        return False
    else:
        return True


def dynamic_xor_encrypt(plaintext, text_key): #message, trudeau
    cipher_text = ""
    key_length = len(text_key) 7
    for i, char in enumerate(plaintext[::-1]):  
        key_char = text_key[i % key_length]  #scrambles the entire key, We need to figure out how to unscramble it
        encrypted_char = chr(ord(char) ^ ord(key_char)) #uses char and ket_char to generate an encrypted character
        cipher_text += encrypted_char #forms a string from the encrypted char
    return cipher_text


def test(plain_text, text_key): #message, trudeau
    p = 97
    g = 31
    if not is_prime(p) and not is_prime(g):
        print("Enter prime numbers")
        return
    a = randint(p-10, p)  #a and b are given so these wont be needed
    b = randint(g-10, g)
    print(f"a = {a}") 
    print(f"b = {b}")
    u = generator(g, a, p) #pow(g,a) % p
    v = generator(g, b, p) #pow(g,b) % p
    key = generator(v, a, p) #pow(v,a) % p
    b_key = generator(u, b, p)
    shared_key = None
    if key == b_key:
        shared_key = key 
    else:
        print("Invalid key")
        return
    semi_cipher = dynamic_xor_encrypt(plain_text, text_key)
    cipher = encrypt(semi_cipher, shared_key)
    print(f'cipher is: {cipher}') #We know the cipher, So we need to back track


if __name__ == "__main__":
    message = sys.argv[1]
    test(message, "trudeau")

```
- To understand this code, I had to go step wise, I have written comments based on what I understood a line or segment of code does
- I went about this in a stepwise manner first noting down what all I knew and what all I had to find out
```
a = 89
b = 27
p = 97
g = 31
def generator(g, x, p):
    return pow(g, x) % p

def is_prime(p): We already know p,q are prime so this is not needed
    v = 0
    for i in range(2, p + 1):
        if p % i == 0:
            v = v + 1
    if v > 1:
        return False
    else:
        return True
    
def dynamic_xor_encrypt(plaintext, text_key): 
    cipher_text = ""
    key_length = len(text_key) 
    for i, char in enumerate(plaintext[::-1]): 
        key_char = text_key[i % key_length]
        encrypted_char = chr(ord(char) ^ ord(key_char)) 
        cipher_text += encrypted_char 
    return cipher_text


cipher = [33588, 276168, 261240, 302292, 343344, 328416, 242580, 85836, 82104, 156744, 0, 309756, 78372, 18660, 253776, 0, 82104, 320952, 3732, 231384, 89568, 100764, 22392, 22392, 63444, 22392, 97032, 190332, 119424, 182868, 97032, 26124, 44784, 63444]
u = generator(g, a, p) #pow(g,a) % p
v = generator(g, b, p) #pow(g,b) % p
key = generator(v, a, p) #pow(v,a) % p
b_key = generator(u, b, p)
shared_key = None
if key == b_key:
    shared_key = key 
print(key) #key = 12
#We have the cypher, So we can not go backwards to decrypt the cipher
#cipher = ord(char)*key*311
#So, we can find out the characters of semicipher by, ord(char)=cipher/(key*311)
#Also need to convert char into a character, this can be done with chr()
d = ""
for i in cipher:
    d += chr(i //(key*311)) #This will add each indivisual character with respect to corresponding cipher value
print(d) #This is semi-cipher
print(dynamic_xor_encrypt(d,"picoCTF")) # If you use xor on plaintext it gives ciphertext, if you use xor on ciphertext it will give plain text
#I put picoCTF in the text_key section, since I know that is part of the flag
# That gives me the scrambled key, on noticing the scrambling closely I could make out that `trudeau` was scrambled(Almost reversed except the last u)
print(dynamic_xor_encrypt(d, "aedurtu"))# I now know what jumbled test_key will give picoCTF So I simply put 'aedurtu' as the text_key and that ended up giving me the flag
```
- The encryption had three parts to it, The first reversed the input value, the second acted on the text_key using a modulus to scramble it and finally the third one jumbled it up a lot using both xor operator and the values obtained from the previous two encryptions, understanding this was important as now I could work against it

<img width="1477" height="177" alt="image" src="https://github.com/user-attachments/assets/784ee4df-8d04-4b6e-b589-dc55f53890ee" />


## Flag:

```
picoCTF{custom_d2cr0pt6d_dc499538}
```

## Concepts learnt:

- I learned a lot about python, I already knew the basics but there was still so much I learned in this challenge as I was forced to write almost an entire python script
- I studied up on XOR encryption after looking at the code of this challenge, which ended up being helpful in understanding what was going on

## Notes:

- There can be many possible variations of python programs used in this to solve the problem, This vode seemed to work the best for me
- It was important that I go step wise to understand exactly what was going on, Even after completing this challenge, I still am not fully sure about XOR encryption.
I did enjoy doing it, I hope to learn more about this topic

## Resources:

- https://ctf101.org/cryptography/what-is-rsa/
- https://www.w3schools.com/python/
- https://www.youtube.com/playlist?list=PLBlnK6fEyqRhBsP45jUdcqBivf25hyVkU
- https://www.dcode.fr/rsa-cipher
- https://www.google.com

## Incorrect Tangents:
- This challenge was packed with errors and incorrect tangents, especially with the code
- I forgot to convert the characters of semicipher from unicode back to char, I initially had not added the `+=` which ended up only giving me the last value of char(I forgot cipher was a list)
- It took me a while before I understood the algorithm that encrypted it
- I put the test key 'trudeau' hoping that would be enough alongside semicipher to give the answer 
- I also needed to learn what XOR is better to understand putting the semicipher as argument would give me back the plain text


***
