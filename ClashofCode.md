# Clash of Code
## Goal
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
        # s,e=i,j
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
