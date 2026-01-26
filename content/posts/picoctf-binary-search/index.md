---
date: '2026-01-25T21:24:18+07:00'
title: 'picoCTf - Binary Search'
tags: ["ctf"]
---

- URL: https://play.picoctf.org/practice/challenge/442
- Title: Binary Search
- Tags: Easy, General Skills, picoCTF 2024, shell, browser_webshell_solvable, ls
- Author: Jeffery John
- _Started: 9 July 2025_
- _Solved: 9 July 2025_
- Description: Want to play a game? As you use more of the shell, you might be interested in how they work! Binary search is a classic algorithm used to quickly find an item in a sorted list. Can you find the flag? You'll have 1000 possibilities and only 10 guesses. Cyber security often has a huge amount of data to look through - from logs, vulnerability reports, and forensics. Practicing the fundamentals manually might help you in the future when you have to write your own tools! You can download the challenge files here:

    challenge.zip

Additional details will be available after launching your challenge instance.

So here's my terminal snippet of me answering Binary Search game

```
Welcome to the Binary Search Game!
I'm thinking of a number between 1 and 1000.
Enter your guess: 500
Higher! Try again.
Enter your guess: 750
Higher! Try again.
Enter your guess: 875
Higher! Try again.
Enter your guess: 937  
Higher! Try again.
Enter your guess: 968
Higher! Try again.
Enter your guess: 984
Higher! Try again.
Enter your guess: 992
Higher! Try again.
Enter your guess: 996
Higher! Try again.
Enter your guess: 998
Congratulations! You guessed the correct number: 998
Here's your flag: picoCTF{g00d_gu355_1597707f}
```

The method is to use [Binary Search](https://www.geeksforgeeks.org/dsa/binary-search/) to guess the number. Each time I guess, I divide the search space into two and find the mid value

| Nth guess | Start | End  | Floor((Start+End)/2) | Result  |
| --------- | ----- | ---- | -------------------- | ------- |
| 1         | 1     | 1000 | 500                  | Higher  |
| 2         | 500   | 1000 | 750                  | Higher  |
| 3         | 750   | 1000 | 875                  | Higher  |
| 4         | 875   | 1000 | 937                  | Higher  |
| 5         | 937   | 1000 | 968                  | Higher  |
| 6         | 968   | 1000 | 984                  | Higher  |
| 7         | 984   | 1000 | 992                  | Higher  |
| 8         | 992   | 1000 | 996                  | Higher  |
| 9         | 996   | 1000 | 998                  | Correct |

Here's the flag

`picoCTF{g00d_gu355_1597707f}`