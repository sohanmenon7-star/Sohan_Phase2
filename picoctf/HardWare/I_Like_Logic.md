# 2. I like Logic

> i like logic and i like files, apparently, they have something in common, what should my next step be
<img width="881" height="442" alt="image" src="https://github.com/user-attachments/assets/c1d29db2-c6a6-43f0-8863-37a22a4e7aa9" />

## Solution:

- This question did not give much information to start off with, the only things provided was a hint between a connection in files and logic and .sal file
- The .sal file had 5 .bin files and one meta.json file
- Going off on the connection on files and logic, I found out something about logic files and read up on them
- I also looked up what a .sal file is found out it is a type of logic file, specifically one which uses serial communication in the form of highs and lows to form data 
- To read this data, I downloaded Logic 2(This is where the hint comes in to play) from the official saleae website to read this .sal file
- After opening the .sal file in Logic 2 I found The wave data hidden, I just needed to extract this data
- After a quick tutorial on how to operate Logic 2, I analyzed the code converting the hex data into ASCII
- This formed a long sentence, hidden within was the flag
<img width="1788" height="833" alt="image" src="https://github.com/user-attachments/assets/e7d66c6a-f736-44f4-8ba8-8da4b4366016" />

## Flag:

```
FCSC{b1dee4eeadf6c4e60aeb142b0b486344e64b12b40d1046de95c89ba5e23a9925}
```

## Concepts learnt:

- I learned about logical files and how they differ from physical files. Unlike physical files, Logical files dont ontain any data and operate independent of an OS. Logical files are a representation of one or more physical files and contain more than one type of format
- I learned about .sal which are a type of logical file, they usually contain .bin files which act as channels when viewing the file in Logic 2 and meta.json which basically tells what the file is and what it is supposed to do and show as these .sal files do not use OS
- I learned more about Logic 2 and viewing the data of .sal files

## Notes:

- If there are other techniques for viewing .sal files, I need to research on them and learn about it but using Logic 2 was the simplest one and extremely user freindly in my opinion

## Resources:

- https://www.geeksforgeeks.org/operating-systems/physical-and-logical-file-systems/
- https://www.youtube.com/watch?v=XnoHXyb7dkY
- https://www.youtube.com/watch?v=Uf0KKh2zRuA
- https://www.youtube.com/watch?v=IyGwvGzrqp8
- https://www.google.com

## Incorrect Tangents:
- The first challenge was opening up the .sal file to understand how to proceed, I tried multiple ways of accessing this file in the terminal, like `objdump`, `strings`, `file` etc. but to no avail
- Another task was navigating through Logic 2 to decipher the hidden message which contained the flag, I struggled with converting the data from hex to ASCII. Fortunately, I caught on quickly

***
