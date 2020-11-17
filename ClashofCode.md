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
### solution
only 77%
```python
def GetNum(n, array):
    maxArea = 0
    for i in range(n):
        minhigh = array[i]
        for j in range(i, n):
            minhigh = min(minhigh, array[j])
            maxArea = max(maxArea, minhigh*(j-i+1))
    return maxArea
h = int(input())
l = []
wl=0
for i in range(h):
    line = input()
    for i in line:
        if i.isalpha():
            wl+=1
    l.append(len(line))
# print(wl)
res = GetNum(h, l)
print(res)
```
##  	Goal
Can a Rubik's cube be solved by Restickering™?  

A popular method to pretend you can solve the Rubik's cube when no one's watching is to peel the stickers off and glue them back into place. It's not a very good method, as it tends to damage the stickers irreparably, but from a theoretical point of view it does the job.

Feliks has left his scrambled cube on the table for only a few minutes, but as he comes back from his break, he notices an evil grin on Lucas's face. Has Lucas been messing around with the cube and spare stickers in a way that makes it unsolvable using the Restickering™ method? Help Feliks by telling him whether or not he can peel and glue the stickers back into place.

You are given a cube state in pattern format. A solved cube looks like this:  

    UUU  
    UUU  
    UUU  

LLL FFF RRR BBB  
LLL FFF RRR BBB  
LLL FFF RRR BBB  

    DDD  
    DDD  
    DDD  

Letters ULFRBD mean “this sticker belongs on the Up/‌Left/‌Front/‌Right/‌Back/‌Down face”.

A monochrome cube, e.g. with only U stickers, is obviously unsolvable using the Restickering™ method.

A cube where an R′ move (right face counterclockwise quarter turn, in standard notation) has been applied is solvable using the Restickering™ method and looks like the example below.
Input  
11 lines (including 2 blank): a cube pattern  
Output  
SOLVABLE if it is possible to peel the stickers off and glue them back in a solved cube.  
UNSOLVABLE otherwise.
Constraints  
Apart from the stickering, all cubes are standard 3×3×3 Rubik's cubes.  
Only valid sticker colors are provided.    
Example  
Input  
    UUB  
    UUB  
    UUB  

LLL FFU RRR DBB  
LLL FFU RRR DBB  
LLL FFU RRR DBB  

    DDF  
    DDF  
    DDF  
Output  
SOLVABLE  

```python
t=$<.read.scan(/\w/)
$><<('ULFRBD'.chars.all?{|c|t.count(c)==9}?"":"UN")<<:SOLVABLE
```
```python
all cases
 R′
    UUB
    UUB
    UUB

LLL FFU RRR DBB
LLL FFU RRR DBB
LLL FFU RRR DBB

    DDF
    DDF
    DDF
SOLVABLE

 Solved
    UUU
    UUU
    UUU

LLL FFF RRR BBB
LLL FFF RRR BBB
LLL FFF RRR BBB

    DDD
    DDD
    DDD
SOLVABLE

 Pure White
    UUU
    UUU
    UUU

UUU UUU UUU UUU
UUU UUU UUU UUU
UUU UUU UUU UUU

    UUU
    UUU
    UUU
UNSOLVABLE

04 L2 D R′ D′ F′ D′ R D′ R2 F2
    DUD
    DUU
    BDL

LLL UFF ULR FBF
LLR BFF URB DBF
FRD BUU BFB DBR

    LRR
    DDR
    ULR
SOLVABLE

05 UF edge flip
    UUU
    UUU
    UFU

LLL FUF RRR BBB
LLL FFF RRR BBB
LLL FFF RRR BBB

    DDD
    DDD
    DDD
SOLVABLE

06 UFR corner twist
    UUU
    UUU
    UUF

LLL FFR URR BBB
LLL FFF RRR BBB
LLL FFF RRR BBB

    DDD
    DDD
    DDD
SOLVABLE

07 Random stickers
    LRD
    DFR
    RBD

ULF LRB DBD LLB
RLL BUU BFD FFU
BDR URL UDF RFL

    FBU
    LRU
    DFU
UNSOLVABLE

08 More random stickers
    BDL
    DBL
    LUR

BFR BBD LUFDUR
UBR RRD DLDFUR
RBF FUU FRFBFD

    UBF
    LLD
    LUR
UNSOLVABLE
```
## Goal
The program:
Your given a scrambled sentence. You must output an unscrambled version of the same sentence using these rules:
- First, print one in every two characters.
- Then print every other character starting from the end, going backwards. Make sure you handle strings of both even and odd lengths.

INPUT:  
Line 1: One string scrambled.  

OUTPUT:  
A single line containing an unscrambled version of scrambled.  

CONSTRAINTS:  
scrambled contains at least 1 character.  
scrambled contains less than 400 characters.  

EXAMPLE:  
Input  
H!e ldllor oW  
Output  
Hello World !  

Solution
```python
s=input()
print(s[::2]+s[1::2][::-1])
```
## Goal
n clones of Fokz are standing in a circular order (numbered from 1 to n) . Number 1 has a sword. He kills the next person (i.e. No. 2) and gives the sword to the next (i.e. No. 3). All people do the same until only 1 survives. You are expected to output the number of the last survivor.
{Where should the real Fokz stand so that he is the last survivor?}  
Input  
1 Line containing a number n  
Output  
Number of the last survivor  
Constraints  
1 <= n <= 10^5  
Example  
Input  
5  
Output  
3  
### Solution
约瑟夫环
```python
def josephus(n, k):
    # n代表总人数，k代表报数的数字
    List = list(range(1, n + 1))
    index = 0
    while List:
        temp = List.pop(0)
        index += 1
        if index == k:
            index = 0
            continue
        List.append(temp)
        if len(List) == 2:
            print(List[-1])
            break
print(j(n, 2))
```

```python
def j(n,k):
    r=0
    for i in range(1, n+1):
        r=(r+k)%i
    return r+1
n = int(input())
print(j(n, 2))
```
##  Goal
Beginner astrophotographer Oleg took a photo of the night sky. Now he wants to find a number of constellations in it. This photo is h pixels in height and w pixels in width and each pixel is either a star (*) or an empty region (.). A star can be described by its coordinates (x, y) in the photo. He found following algorithm to identify constellations:

0) Initially, each star is considered as a separate constellation  
1) Choose two stars in different constellations. Let (x1, y1) and (x2, y2) be coordinates of those stars.  
2) If the rectilinear distance between stars is under given threshold t, i.e. |x1 - x2|+|y1 - y2|≤ t, then merge corresponding constellations.  
3) Repeat steps #1-2 until no merging occurs  

Oleg asks you to implement above algorithm and count constellations in the photo.  
Input  
Line 1: Three space-separated integers h (height of the photo), w (width of the photo), t (distance threshold)  
Next h lines: String representing a row of the photo. It consists of characters . (empty region) and * (star)  
Output  
Print a number of constellations in the photo  
Constraints  
1 ≤ h, w < 100  
1 ≤ t < 200  
Number of stars is guaranteed to be less than or equal to 256.  
Example  
Input  
4 5 1  
```python
**...  
*....  
....*  
...**  
```
Output  
2  

Solution
```python
h, w, t = [int(i) for i in input().split()]
m = [input() for _ in range(h)]
stars = []
for i in range(h):
    for j in range(w):
        if m[i][j] == '*':
            stars.append((i, j))
const = list(range(len(stars)))
for i in range(len(stars)):
    c = const[i]
    yi,xi = stars[i]
    for j in range(i+1, len(stars)):
        yj,xj = stars[j]
        c2 = const[j]
        if abs(yj-yi)+abs(xj-xi) <= t:
            for k in range(len(const)):
                if const[k] == c2:
                    const[k] = c


print(len(set(const)))
```
##  	Goal
Check if a given number N is a perfect r-th power. That is, check whether there exist integers a and r ≥ 2 such that a multiplied by itself r times is equal to N, i.e. a^r = N.
Input  
A line containing a single integer N.  
Output  
Perfect if N is a perfect power.  
Flawed if N is not a perfect power.  
Constraints  
1 < N < 10^18  
Example  
Input  
9  
Output  
Perfect  

75%, for big cube case time out
```python
n = int(input())
r = 2
ans = "Flawed"
end = int(n**0.5)
for i in range(r, end+1):
    if int(n**(1/i))**i == n:
        ans = "Perfect"
        break
print(ans)
```
## 	Goal
Ali is given the number of visitors at her local theme park on N consecutive days. A day is record-breaking if it satisfies both of the following conditions:

1) The number of visitors on the day is strictly larger than the number of visitors on each of the previous days.

2) Either it is the last day, or the number of visitors on the day is strictly larger than the number of visitors on the following day.

Note that the very first day could be a record-breaking day!  

Please help Ali find out the number of record-breaking days R.  
Input  
Line 1: An integer N: The number of days.  
Line 2: N space-separated integers: The number of visitors on each day.  
Output  
R - the number of record-breaking days.  
Constraints  
1 ≤ N ≤ 1000  
Example  
Input  
8  
1 2 0 7 2 0 2 0  
Output  
2  
```python
n = int(input())
l = list(map(int, input().split()))
bemax=l[0]

res=0
for i in range(n):
    if i==0 and l[i] > l[i+1]:
        res+=1
    elif i<n-1:
        if l[i] > bemax and l[i] > l[i+1]:
            res+=1
    else:
        if l[i]>bemax:
            res+=1
    bemax = max(bemax, l[i])
print(res)
```
## Goal
Determine the age of a tree by counting the number of rings in a horizontal cross-section of its trunk.

You are presented with a 10×N grid representing a cross-section of a tree.

Every year, the tree alternates between a phase of rapid and slow growth depending on the season.

To compute the age of the tree, count the number of transitions between a cycle of rapid grow (line of 0), and slow growth (a line of 1).

A few considerations:  

- There is an arbitrary number of lines per cycle.  

- The tree trunk is not perfect and you must expect to see errors (i.e a 0 instead of 1 or vice-versa) or unwanted particles (represented by any other printable character).  

- However, on any given line there will always be 10 characters, and less errors than valid characters.  

Here is an example:  
0000001000  
1111111111  
111111?111  
0000000000  
The age of this tree is 2 years since there are 2 transitions.  
Input  
Line 1: An integer N representing the height of the grid  
Next N lines: Lines of 10 characters representing a section of the tree trunk  
Output  
An integer representing the age of the tree  
Constraints  
0 < N ≤ 1000  
Example  
Input  
2  
0000000000  
1111111111  
Output  
1  

```
n=int(input())
l=[]
res=0
f=['0','1']
for i in range(n):
    t = list(input())
    for j in f:
        if t.count(j)>5:l.append(j)
for i in range(len(l)-1):
    if l[i]!=l[i+1]:res+=1
print(res)
```

## Goal
You are given a polynomial represented as a list of floats A,B,C,... of length M, where A,B,C... are coefficients used in the following way p(x) = A + BX + CX^2 + DX^3.... You must find the derivative with respect to X.

The derivative D of a polynomial with respect to X is calculated in the following manner (letters represent constants, except for x)
D (a*x^p) = a*p*x^(p-1)  
D (a*x^p + b*x^q + c*x^r...) = D (a*x^p) + D (b*x^q) + D (c*x^r) ...  

EXAMPLE DERIVATIVE:  
D(13.421 + 14.2X + 6X^2) = 14.2 + 12X  
Input  
Line 1: An integer M for the length of the list of polynomial coefficients  
Next M lines: The list of polynomial coefficients starting with the coefficient on x^0 A  
Output  
M - 1 lines: The list of polynomial coefficients starting with the coefficient on x^0 A rounded to the tenths place(5.1, 3.2, 19.3).  
Constraints  
2 ≤ M < 10  
-500 ≤ A,B,C....(input polynomial) ≤ 500  
-5000 ≤ A,B,C....(output polynomial) ≤ 5000  
Example  
Input  
9  
0  
0  
0  
0  
0  
0  
0  
0  
0  
Output  
0.0  
0.0  
0.0  
0.0  
0.0  
0.0  
0.0  
0.0  

### Solution
```python
m = int(input())
res = []
for i in range(m):
    coefficient = float(input())
    if i != 0:
        res.append(round(coefficient*(i),1))

for r in res:
    print(r)
```

## 	Goal
Fred works in a warehouse handling boxes. Every box has a reference number (up to 7 digits) printed on it.  

Some numbers look like a different number if the box is upside-down.  
Example: 18609 ➠ 60981. Fred calls these NUISANCE numbers.  

Given a number, determine if it is a NUISANCE number (output yes or no).  

In the font used by the box printer:  
• an upside-down 0 looks like a 0  
• an upside-down 1 looks like a 1  
• an upside-down 6 looks like a 9  
• an upside-down 8 looks like a 8  
• an upside-down 9 looks like a 6  

A number which looks the same when upside-down (Example: 86098 ➠ 86098) is NOT a NUISANCE number.  
Input  
The number printed on the box, N  
Output  
yes if N is a NUISANCE number  
no if N is not a NUISANCE number  
Constraints  
N is an integer with no more than 7 digits  
Example  
Input  
6  
Output  
yes  

### Solution
note:if [2,5,7] in n, is not nuisance number.
```python
import sys
import math

# Auto-generated code below aims at helping you parse
# the standard input according to the problem statement.

n = input()
d = {'6':'9', '9':'6'}
# Write an answer using print
# To debug: print("Debug messages...", file=sys.stderr, flush=True)
res = ""
for i in n[::-1]:
    if i in d:
        res+=d[i]
    else:
        res+=i
if '5' in n or '7' in n or '2' in n or res == n:
    print("no")
else:
    print("yes")

```

##  	Goal  
Turn an input name into a palindrome using this simple concept:

Take a name like "Abe Simpson" and alternate each letter with the reverse name "nospmiS ebA" to get:  

Abe Simpson +  
nospmiS ebA =  
Anboes pSmiimSp seobnA  

Now you have your name Palindromified!  

Take an input string (name) and Palindromify it!  
Input  
A single line: A string representing a name  
Output  
A single line: The Palindromified name (formed by reading characters alternately from left and right).  
Constraints  
Input names will have no double whitespace characters and will only use Latin (and Latin-1 Supplement e.g. ãéïôñ) unicode characters.  
Example  
Input  
Rihanna  
Output  
RainhnaanhniaR  

### Solution
```python
name = input()
res = ""
for i,j in zip(name, name[::-1]):
    res+=i
    res+=j
print(res)
```

## 	Goal
Junior did a big mistake. He deleted the FileSystem of his computer. Now he is left only with the root folder ("/"). Fortunately he has a backup. However the backup tool is quite basic, and Junior has to re-create by hands all the folders. Junior has the list of paths of the folders to be restored from back-up. He wants to know how many folders must be created to achieve the full restore.  
Input  
Line 1: an Integer N, the number of paths of folders to be restored
N following lines: a string representing the path of a folder to be restored.  
Output  
Number of folders that must be created  
Constraints  
Each path is given in the Unix format (e.g. /usr/local/bin), and uses only alphanum characters.  
Each path starts with "/" and ends with an alphanum.  
Example  
Input  
1  
/usr/bin  
Output  
2  

### Solution
```python

```

## Goal
A message has been encrypted with Pi cipher encryption.
You need to print the decrypted message.  

In the Pi cipher encryption, each character is shifted by the value of the digit in Pi at the position of the letter in the message skipping non-letter characters (ex: 'T' is the 3rd letter in 'HI THERE', so its position is 3)  

Only shift if it is a letter.  
All characters in the input are upper case.  

For your information: Pi starts with 3.1415926535897932384626433832795028841971693993751058209749445923078164062862089986280348253421170679

Example:  
```
Original message:  HELLO WORLD!  
Pi used as a key:  31415 92653  
Encrypted message: KFPMT FQXQG!  
```

Again, you have to decrypt the message, not encrypt it.  
Input  
A string s which you need to decrypt  
Output  
A string which is the decrypted message  
Constraints  
1 ≤ s length ≤ 100  
Letters in s are capital only.  
Example  
Input  
KFPMT FQXQG!  
Output  
HELLO WORLD!  

### Solution
```python
import sys
import math

# Auto-generated code below aims at helping you parse
# the standard input according to the problem statement.

s = input()
p="31415926535897932384626433832795028841971693993751058209749445923078164062862089986280348253421170679"
# Write an answer using print
# To debug: print("Debug messages...", file=sys.stderr, flush=True)
res = ""
k=0
for i,c in enumerate(s):
    if c.isalpha():
        # print(p[k])
        res += chr(65+(ord(c)-65-int(p[k]))%26)
        k+=1
    else:
        res += c
print(res)
```


## Goal
A government has a progressive tax system.  

- First $5,000 of income ($1 - $5,000) - taxed at 0% (no tax)  
- Next $5,000 of income ($5,001 - $10,000) - taxed at 5%  
- Next $10,000 of income ($10,001 - $20,000) - taxed at 10%  
- Next $20,000 of income ($20,001 - $40,000) - taxed at 20%  
- Afterwards ($40,001 onwards) - taxed at 30%  

If you are taxed $X, how much was your income? Assuming that your income is an integer dollar value. If there are multiple possible answers, give the lowest possible amount.  

More specifically, find the minimum integer dollar value of income N such that incomeTax(N) = X. For example, if you are taxed $1.25, then your income is $5,025.  
Input  
Line 1: X - the income tax, represented as a number with 2 decimal points  
Output  
Line 1: N  
Constraints  
0 ≤ X ≤ 500000  
Example  
Input  
1.25  
Output  
5025  


### Solution
```python

x=float(input())
n=5e3*(x>0)
for i in[1,2,4]:v=min(250*i*i,x);n+=v*20/i;x-=v
print(int(n+x*10/3))
```

## Goal
Kanji are symbols used by Japanese people to form words.
Traditionally, these symbols are written vertically.
Given a sentence, you must transcribe it vertically, in the same way as kanji.
Input  
n : The maximum vertical size of a column.  
s : A string of characters written horizontally.  
Output  
The string s written vertically from the top to the bottom and from the right to the left.  
The last column must be filled with spaces.  
Constraints  
Example  
Input  
4  
Hello World  
Output  
```
roH  
l e  
dWl  
 ol  
```
### Solution
```python
n=int(input())
s=input()
l= [""]*n
k=int(len(s)/n+0.5)
for i,c in enumerate(s):
    l[i%n]=c+l[i%n]
for i in l:
    print((k-len(i))*" "+i)
```
## 	Goal
You are given two sorted lists of positive integers, A and B.

Find all the integers, Z that are divisible by all integers in list A (Z mod A = 0) and also divide all integers in list B (B mod Z = 0).

If no intermediate factors exist, just print "None".
Input  
Line 1: Two integers, sizeA and sizeB separated by a space, denoting the sizes of lists A and B.  
Line 2: sizeA space separated integers in list A.  
Line 3: sizeB space separated integers in list B.  
Output  
Line 1: A space separated list of integers that are evenly divisible by all integers in list A and evenly divide all integers in list B.  
If no intermediate factors exist, just print "None".  
Constraints  
1 ≤ A, B < 2^31 - 1  
1 ≤ sizeA, sizeB ≤ 10  
Example  
Input  
2 3  
2 3  
6 12 24  
Output  
6  

### Solution
```python
import sys
import math

# Auto-generated code below aims at helping you parse
# the standard input according to the problem statement.
def gbs(s):
    if len(s) <=1:
        return s[0]
    a,b = s[0],s[1]
    a = a // math.gcd(a, b) * b // math.gcd(a, b) * math.gcd(a, b)
    if len(s)>2:
        for i in range(2,len(s)):
            b = s[i]
            a = a//math.gcd(a,b) * b//math.gcd(a,b) * math.gcd(a, b)
    return a

size_a, size_b = [int(i) for i in input().split()]
al = list(map(int,input().split()))
bl = list(map(int,input().split()))

g = gbs(al)
res = []
for i in range(1,bl[0]+1):
    if i%g==0 and all(b%i==0 for b in bl):
        res.append(i)
if res:
    print(*res)
else:
    print("None")

```
##  	Goal  
It is NOW (time) and we must arrive at ARRIVAL (time), but the duration of the travel is DURATION minutes. Are we late?  
Input  
Line 1: A string NOW representing the current time  
Line 2: A string ARRIVAL representing the wanted arrival time  
Line 3: A number DURATION representing the number of minutes needed to get there  
Output  
A line with "OK" if we are on time, otherwise a line with "LATE"  
Constraints  
Example  
Input  
15:32   
16:45  
35  
Output  
OK  

### Solution
```python
from dateutil.parser import parse
n = input()
a = input()

d = int(input())

res = (parse(a)-parse(n)).seconds
if res >= d*60:
    print("OK")
else:
    print("LATE")
```

## Goal  
The Intersection over Union (IoU) is known to be a good metric for measuring overlap between two bounding boxes or masks.  

It is calculated as Area of the intersection / Area of the union.  

You will receive two bounding boxes:  
- x_1, y_1, w_1, h_1  
- x_2, y_2, w_2, h_2  
where x and y represent the top-left coordinate and w and h represent the width and the height.  

Compute the IoU!  

Warning:  
- The test cases are defined in a way that no approximation are   required (e.g., no result is 0.33333333...).  
- Get rid of trailing 0s (1.0 should be 1).  
Input  
Line 1: x_1, y_1, w_1, h_1  
Line 2: x_2, y_2, w_2, h_2  
Output  
Line 1: The IoU  
Constraints  
0 ≤ x_1, y_1, x_2, y_2 < 1000  
0 < w_1, h_1, w_2, h_2 < 1000  
Example  
Input  
1 1 2 2  
2 1 2 3  
Output  
0.25  
### Solution
```python
def computeArea( A,B,C,D,E,F,G,H):
  area_max=abs(C-A)*abs(D-B)+abs(G-E)*abs(H-F)
  
  if C<=E or G<=A or D<=F or H<=B:return 0
  else:
      rx = min(G,C)-max(A,E)
      ry = min(D, H)-max(B,F)
      return (abs(rx*ry))/(area_max - abs(rx*ry))

x1, y1, w1, h1 = map(int, input().split())
x2, y2, w2, h2 = map(int, input().split())

res = computeArea(x1, y1, x1+w1, y1+h1, x2,y2, x2+w2, y2+h2)
if res == int(res):res = int(res)
print(res)
```

## 	Goal  
The goal is to reformat a sequence of integers, so that each pair is separated by a number of points ('.') equal to the number on the left.
Input  
Line 1: An integer sequence T  
Output  
Line 1: A string containing the sequence of integers, T, separated by the correct number of '.'s  
Constraints  
1 ≤ Length_of_T ≤ 50  
0 ≤ Element_of_T ≤ 500  
Example  
Input  
5  
1 2 3 4 5  
Output  
1.2..3...4....5

### Solution
```python
len_t = int(input())
l = list(map(int, input().split()))
s = ""
for i in range(len_t-1):
    s += str(l[i])+"."*l[i]
s+=str(l[-1])
print(s)
```

## 	Goal
Given a set of N integers (P1,P2...Pn), and a sequence of consecutive increasing integers, starting at X : (X,X+1,X+2,...)
Remove any values from the sequence which are multiples of any member of the set and return the Cth remaining value of the sequence.  

For example: Consider a set with N=2 integers (P1=2, P2=3); and a sequence starting with X=1 : ( 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 ... )  

From this sequence we remove all multiples of our N integers in the set (P1..Pn), so in this example we remove all multiples of 2 and 3, giving: 1 5 7 11 13 17...  

Finally, we take the Cth number from the resulting sequence, let's say in this example C=5 so then our answer = 13.  
Input  
Line 1: 3 space-separated integers N set size, X sequence start, C the enumerated result to return.  
Next N lines: An integer Pi in the set.  
Output  
The Cth value remaining from the sequence after removing those which are multiples of any member of the set.  
Constraints  
1 ≤ N ≤ 99  
1 ≤ X ≤ 10^6  
1 ≤ C ≤ 10^5  
2 ≤ Pi ≤ 999  
Example  
Input  
2 1 5  
2  
3  
Output  
13  

### Solution
```python
n,x,c=map(int, input().split())
l=[]
for i in range(n):l+=[int(input())]
while c>0:
    f=1
    for p in l:
        if x%p==0:f=0
    if f:c-=1   
    x+=1
print(x-1)
```

## 	Goal
As you know, unicorns are nearly extinct. It is your mission to supply the world with unicorns aged just right for whatever purpose they'll serve. You'll be given an age and are to produce an ascii-unicorn of that age.
Input
Line 1: An integer age specifying the unicorn's age.
Output
You are to produce a unicorn following the "International Unicornial Standard 6887 specification" (which you might want to copy and paste) as follows:

A basic unicorn looks like this:
```
 _oO^____
(._,     \
   \  _\ /\
    || ||
~~~~~~~~~~~~~
```

With age, it's horn grows by one \ a year. A one year old unicorn will hence look like this:
```
  \
 _oO^____
(._,     \
   \  _\ /\
    || ||
~~~~~~~~~~~~~
```
A unicorn of age 2 looks like this:
```
 \
  \
 _oO^____
(._,     \
   \  _\ /\
    || ||
~~~~~~~~~~~~~
```
Constraints  
0 ≤ age ≤ 100 as unicorns only get 100 years old.  

Unicorn must be as far left as possible.  
No trailing spaces.  
No extra lines.  
Example  
Input  
1  
Output
```
  \
 _oO^____
(._,     \
   \  _\ /\
    || ||
~~~~~~~~~~~~~
```
### Solution
```python
a = int(input())
hl = []
bl=[' _oO^____','(._,     \\','   \  _\ /\\','    || ||','~~~~~~~~~~~~~']
o=e=0
if a<=3:o=3-a
else:e=a-3
for i in range(1,a+1):hl.append(' '*(o+i-1)+'\\')
if a>0:
    for h in hl:print(h)
for b in bl:print(' '*e+b)
```
