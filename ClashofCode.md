# Clash of Code
##  Goal
Put parentheses around a series of words in an odd way.

- There should be no parentheses surrounding the entire phrase.
- The first set of parenthesis should encase all words except the last one.
- The second set should be inside the first set and encase all words except the first one in the set.
- The third set should be inside the second set and encase all words except the last one in the set.
- The fourth set should be inside the third set and encase all words except the first one in the set.
- Stop when there are no more words to put in the next set.

For an example, consider the title of the problem:  
Inward Flowing Text Nest  
(Inward Flowing Text) Nest  
(Inward (Flowing Text)) Nest  
(Inward ((Flowing) Text)) Nest  
Input  
Line 1: A series of N words W separated by spaces.  
Output  
Line 1: The series of words W with parentheses placed around them.  
Constraints  
1 ≤ N ≤ 100
1 ≤ Length of W ≤ 50  
Example  
Input  
1 2 3 4 5  
Output  
(1 ((2 (3)) 4)) 5  
### Solution  
```python
line = input()
l = list(line.split())
# print(l, file=sys.stderr)
n = len(l)
# print(n)
res = 0
if n<2:
    print(line)
else:
    res = line
    i=0
    j=len(line)-1
    while i < j:
        # print(i,j)
        # print(line[i:j], line[i], line[j])
        # print(line[i:j], line[i]==" ", line[j]==" ")
        rep="(" + line[i:j].strip() + ")"
        if line[i+1] == " " or line[i]==" ":
            rep = " (" + line[i:j].strip() + ")"
        if line[j-1] == " ":
            rep = "(" + line[i:j].strip() + ") "
        # print(rep)
        res = res.replace(line[i:j], rep)

        # print(res)
        i+=1
        j-=1
    # print("(1 ((2 (3)) 4)) 5")
    print(res)
```
##  Goal
Print loop if the path starting from the start checking point leads to an infinite loop, cul-de-sac otherwise.  
Input
Line 1: start the name of the start checking point  
Line 2: n the total number of check point connections  
Next n lines: Two space separated names prev and next for the name of a check point connected to a next check point in a one way direction (prev to next).  
Output  
loop or cul-de-sac  
Constraints  
Example  
Input  
cp6  
4  
cp4 cp9  
cp9 cp5  
cp6 cp1  
cp1 cp4  
Output  
cul-de-sac  
### solution  
```python 
start = input()
n = int(input())
d = {}
for i in range(n):
    prev, _next = input().split()
    d[prev] = _next
# print(d)
v = d[start]
f=False
slow = fast = start
while slow in d.keys() and fast in d.keys():
    slow = d[slow]
    fast = d[d[fast]]
    if slow == fast:
        f=True
        break

if f:
    print("loop")
else:
    print("cul-de-sac")
```
## Goal
Thanks to our mathematicians, the British have decrypted the entire German communication! Now we can spot the exact location of their submarines. You'll be given an NxM matrix containing the allied ships and the enemy submarines. Tile description follows as:  

*=empty  
0=allied ship  
1=enemy submarine  

Enemy submarines can shoot at 4 directions at once but they can't hit more than one ship in a single direction. Enemy torpedos will ignore and pass thru enemy submarines. For every enemy submarine, calculate the count of allied ships it can hit and print the total. For instance:
```python
**0*  
1*10  
**0*  
0*0*  
```
There are 2 enemy submarines at coordinates (0,1) and (2,1). First submarine can hit 2 allied ships at locations (0,3) and (3,1). Second submarine can hit (2,0), (3,1) and (2,2). 2+3=5 allied ships at total, print 5. Notice how second submarine couldn't hit the target at (2,3) because they can't hit more than one ship in a single direction

"I guess they never miss, huh?" - Winston Churchill  
Input  
Line 1: An integer N for the number of the rows  
Line 2: An integer M for the number of the columns  
Next N lines: M chars as contents of the row  
Output  
An integer that represents the total allied ships hit by enemy submarines  
Constraints  
Enemy submarines cannot hit more than one ship in a single direction  
Enemy torpedos will ignore and pass thru enemy submarines  
0 < N < 10  
0 < M < 10  
Example  
Input  
4  
4  
```python
**0*  
1*10  
**0*  
0*0*  
```
Output  
5  

## Goal
You ask your friend if you can borrow a sheet of paper for the pop quiz that your teacher just announced. He takes out his journal and writes the title of the quiz at the top left:  

QUIZ########  
############  
############  
############  
############  
############  
############  
############  

But then your friend does the unthinkable: he tears the page from his journal without using the perforated line, so that you paper ends up looking like this:  

QUIZ####  
######  
############  
###########  
########  
##########  
#######  
####  

What a ripoff. You decide to pull out some scissors to try to salvage the biggest rectangular area on the page without losing any part of the title. You decide to keep this portion of the page:

QUIZ..##  
......  
......######  
......#####  
......##  
......####  
......#  
####  

That's 42 units of paper space, which is the best you can do.  

Now, given any ripped sheet of paper with a title at the top, what is the biggest area you can get for a rectangular section that preserves the title?  
Input  
Line 1: H, the height of the paper.  
Next H lines: A series of characters denoting the length of the paper at that row.  
Output  
Line 1: The biggest rectangular area you can trim from the piece of paper, keeping the title intact.  
Constraints  
1 ≤ H ≤ 200  
The number of characters in any line is at least 1 and no greater than 200.  

All characters will be #, except for parts of the title, which are alphanumeric characters appearing only in line 1 of the page on the very left.
Title will be at least 1 character long.
Example  
Input  
8  
QUIZ####  
######  
############  
###########  
########  
##########  
#######  
####  
Output  
42  
