# s193 - Alice's Housekeeper
## Problem Statement
- Convert a string of length `N` into one that has no "consecutive repeats" by replacing the minimum number of letters.
- `K` letters are allowed for the string
- If impossible, print "Impossible"
- 1 ≤ `N` ≤ 10<sup>6</sup>
- 2 ≤ `K` ≤ 26

## Analysis of test inputs
1. When there are "repeats", you can just replace 1 of the 2 letters to resolve the repeats
2. When the "repeats chunk" is longer than 2 letters, you replace every other letters in the "chunk". Starting with the second letter is the optimal way.
3. Sometimes you run out of letters. Also what if K=3 were the case in this sample? The circular nature of the menu needs to be dealt with.
4. Needs to deal with the circular feature of the menu.

## Solution Guide
1. How should you store the menu?<br>
`string` C++ object
2. Don't skip subtask 2. Subtask 2 reveals a great deal.<br>
To see the importance of subtask 2, try the following exercise:
Given K=3, solve the following in order:
    1. `aaaabb`
    2. `aaaabbb`
    3. `aaaabbba`
    4. `aaaabbbba`<br>
Then try the above assuming K=2. The problem is much cleaner if you can assume K>2
3. Solution for subtask 2<br>
It's either `ababababab...` or `bababababa...`. You just pick the one with shorter *distance* from the menu. 
4. For the whole problem (subtask 4), how to deal with the circular feature?<br>
Make sure you start from the *real* beginning of a "chunk". (can rewind or fast forward)
In this example below you either start from the "w chunk" or from the *real* beginning of the "q chunk".
```
0123456789     0123456789
qqwwwwreeq     qqwwwwreeq
  ^                     ^
```
---
## Pseudocode
```
start from menu[0] or whatever the beginning of a chunk is
go over the chunks and replace every other letter
```
Issues to consider:
1. Do you fast forward or rewind to get to the *real* beginning of a chunk?
2. How do I implement the control flow so it goes around the string from tail to head? Make sure the loop stops after 1 full loop.
3. Replace every other letter with what letter?
```
i <- next(start)
dist = 0
repeat N times:
  if menu[i] == menu[prev(i)]:
    menu[i] = get_another_letter(menu[prev(i)], menu[next(i)]
    dist += 1
  i <- next(i)
print dist, menu
```
