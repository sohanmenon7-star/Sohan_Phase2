# 3. Vault Door 3

> This vault uses for-loops and byte arrays. The source code for this vault is here: VaultDoor3.java

## Solution:

- In this challenge, a code was given in java which was to be read to obtain a password which would comprise the body of the flag.
- Fortunately, I know the basics of Java
- The code starts of by creating a main function, in which the user is to input a password which if correct displays an appropriate message
- The challenge starts when the main code calls a function to check if the password is correct, then I read the function to find out how it checks to see if the password is correct
- At the end it compared the manipulated password to `jU5t_a_sna_3lpm12g94c_u_4_m7ra41`
- At the start of the function, it created a string which assigns the characters of the entered password to itself in a pattern using 4 different `for` loops. This was then compared to `jU5t_a_sna_3lpm12g94c_u_4_m7ra41`
- After writing out each index of buffer and password(Since I already know what buffer is), I deciphered the passcode and got the flag

<img width="526" height="296" alt="image" src="https://github.com/user-attachments/assets/8296729d-4877-4cce-9b6e-d127457e8424" />

```
public boolean checkPassword(String password) {
        if (password.length() != 32) {
            return false;
        }
        char[] buffer = new char[32];
        int i;
        for (i=0; i<8; i++) {
            buffer[i] = password.charAt(i);
        }
        for (; i<16; i++) {
            buffer[i] = password.charAt(23-i);
        }
        for (; i<32; i+=2) {
            buffer[i] = password.charAt(46-i);
        }
        for (i=31; i>=17; i-=2) {
            buffer[i] = password.charAt(i);
        }
        String s = new String(buffer);
        return s.equals("jU5t_a_sna_3lpm12g94c_u_4_m7ra41"); }
```

## Flag:

```
picoCTF{jU5t_a_S1mpl3_an4gr4m_4_u_c79a21}
```

## Concepts learnt:

- Due to my prior knowledge on Java I was able to read the code with relative ease althoough there were still plenty of functinos which I could not recall, this included scanner.next() which is used to obtain input from user
- I also had a nice revision on Java and ended up learning about it again

## Notes:

- Since this was a Java code, I initially thought of running it although that didnt work since a proper main function was not defined
- I also revised Java a little to understand what the beginning of the code meant which helped me solve the challenge

## Resources:

- https://www.youtube.com/watch?v=gh2RXE9BIN8
- https://www.youtube.com/watch?v=1d-6Hv1c39c
- https://www.youtube.com/playlist?list=PLMB3ddm5Yvh3gf_iev78YP5EPzkA3nPdL
- https://www.Google.com

## Incorrect Tangents
- I did not consider the for loops in the beginning and directly tried "jU5t_a_sna_3lpm12g94c_u_4_m7ra41" which obviously did not work
- While deciphering the password I mixed up some of the indexes which gave me an error


***

