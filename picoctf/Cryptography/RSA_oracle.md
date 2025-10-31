# 1. RSA oracle

> Can you abuse the oracle?
An attacker was able to intercept communications between a bank and a fintech company. They managed to get the message (ciphertext) and the password that was used to encrypt the message.
After some intensive reconassainance they found out that the bank has an oracle that was used to encrypt the password and can be found here nc titan.picoctf.net 62342. Decrypt the password and use it to decrypt the message. The oracle can decrypt anything except the password.


## Solution:

- The challenge provides you a password.enc file which is just an extremely large number and secret.enc which is encrypted(Begining with Salted__), this means it was encrypted with OpenSSL
- In the hints provided, It said Chosen Plaintext Attack, `OpenSSL can be used to decrypt the message. e.g openssl enc -aes-256-cbc -d ...` and The key to getting the flag is by sending a custom message to the server by taking advantage of the RSA encryption algorithm. With all this in mind, I opened the terminal provided with nc titan.picoctf.net
- I saw that the program can encrypt inputs, gives back the hex and then the encrypted ciphertext, Along with the formula of RSA encryption
- As told in the challenge, I tried to decrypt the password directly but that was not allowed
- After learning about RSA, I learnt that the `message is raised to power e(65587 usually) mod N`.
- After viewing some videos in the resources provided and external ones I learnt you can exploit this, I encrypted 2, which means `2^e % n`
- Multiplying this with `m^e % n` (This is the password) would give me `(2m)^e % n`, This can now be decrypted to yield `2m`
- That gave me a hex string response which I converted to integer decimal divided by two, then back to hexadecimal and then ASCII(Since only ASCII can be used a key to arguemnt)
- I now came to a bit of a stand still, So I decided to learn about openssl where I learnt you can give a key for the decryption using `-k`
- So I typed `openssl enc -aes-256-cbc -d -in secret.enc -k da099`. This gave me the flag

## Flag:
```
picoCTF{su((3ss_(r@ck1ng_r3@_da099d93}
```
## Concepts learnt:

- I studied up on RSA quite a bit, learning the formula of encryption and decryption (M^E%n)
- Very importantly I learned how to exploit this property of RSA to obtain a hidden message if not safeguarded properly. Since the encryption uses mathamatical functions, you can multiply the cipher of a known text to it and obtain the message which can be used to obtain the password by dividing it with the original text
- This method is known as Chosen PlainText Attack(CPA), which I learned by surfing through the web
- I also learned about OpenSSL which encryptes files, and to find out how to use the password to break secret.enc open I had to search the arguemnts that could be added to `openssl enc -aes-256-cbc -d`

## Notes:

- The password can be decoded in numerous ways using different plain text although If I am not wrong, It would be most accurate by doing what I have done

## Resources:

- https://ctf101.org/cryptography/what-is-rsa/
- https://www.w3schools.com/python/
- https://www.youtube.com/playlist?list=PLBlnK6fEyqRhBsP45jUdcqBivf25hyVkU
- https://www.geeksforgeeks.org/computer-networks/rsa-algorithm-cryptography/
- https://codedinsights.com/cryptanalysis/chosen-plaintext-attack/#howachosenplaintextattackworks
- https://github.com/zweisamkeit/RSHack/tree/master/Attacks/Chosen_Plaintext
- https://www.google.com

## Incorrect Tangents:
- This challenge was quite tricky to understand first, because of the hint of `openssl`, I spent a lot of time trying to figure out how to use this to decrypt password.enc
- It took me a while before I understood what exactly a Chosen-PlainText-Attack is and how to correctly execute it
- I initially tried decoding the hex string provided directly into ASCII, this gave me errors and a incomplete answer
- I later realized I had to convert the hex string into integer decimal first, I found a python snippet online that would help me do this
```
num=int("c8c2607272", 16)//2
print(hex(num))
```
Without this snippet, I was getting odd values for some reason
- I also tried to directly put the hex value obtained from as the key for secret.enc which did not work


***
