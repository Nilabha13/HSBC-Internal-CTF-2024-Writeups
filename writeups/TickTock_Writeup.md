You can decompile the executable and try to read through it and figure out what it does, but that might take a bit more than our lifetime so let's not do that!

As the name of the challenge suggests, it has something to do with time. If you try out a few inputs, you may notice that some of them take longer than others. This is the exact vulnerability that you needed to exploit. A Timing Channel!

When you input something to the executable, it calculates a character by character hash. It moves to the next character, only if the hash of the current character matches. It exits if the hash does not map. This is where the difference in the timing comes from.

Following pseudo code might help explain if better:
```
for each character 'c' in input:
    h = hash(c)

    if h != precalculatedHash:
        break
```

So to find the whole flag, we should find it character by character. We should iterate over all the possible characters and choose the one which takes the most time. As a start, we should find the first character by trying out following inputs:
```
Axyz
Bxyz
Cxyz
.
.
.
Zxyz
0xyz
1xyz
2xyz
.
.
.
9xyz
{xyz
}xyz
_xyz
```
We have appended `xyz` just for padding and it does not matter if anything else is used for padding apart from that.

Now, note the execution times for all the above inputs. You will find that one of the input takes considerably longer than all other inputs. That input corresponds to letter `N`. Now to find the 2nd character do the same thing. For reference this is what you will use as inputs:
```
NAxyz
NBxyz
NCxyz
.
.
.
NZxyz
N0xyz
N1xyz
N2xyz
.
.
.
N9xyz
{xyz
}xyz
_xyz
```
Now again note execution times and pick the highest one. Keep on doing this for rest of the characters and you'll find the flag!