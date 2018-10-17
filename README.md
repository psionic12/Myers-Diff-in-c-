# Myers-Diff-in-c-
c++ Myers Algorithm implementation and some extra proof.

According to Myers Diff Algorithem(http://www.xmailserver.org/diff2.pdf), there are 3 parts:
1. Find the end of the furthest reaching reverse D-path in diagonal k+∆.
2. Find the middle snake and length of an optimal path for A and B.
3. Get the SES(which is an exercise left to the reader).

which were not given by a pseudocode, this code gives a implementation of them.

The reason to use c++ is that with c++'s operator override feature, the code can be similar to the pseudocode while can be excicuted.

Note: Since the example strings is put in the graph, so the index is start from 1 in the paper, but when implement it, there's no such graph thing, so the start index is from 0, this will lead the code slightly different from the pseudocode. 

Besides, I think the paper missed a proof, which is very simple, but I think the missing will lead to some confusion (for me), so I gives this proof here:

in page 6, line 4, the code is as below:
 
     f k = −D or k ≠ D and V[k − 1] < V[k + 1] Then
        x ← V[k + 1]
     Else
        x ← V[k − 1]+1
       
I don't think lemma2 will lead to this, the purpose of lemma2 is to proof this problem can be solved with a greedy strategy. And according to ```Given the endpoints of the furthest reaching (D − 1)-paths in diagonal k+1 and k−1, say (x’,y’) and (x",y")
respectively, Lemma 2 gives a procedure for computing the endpoint of the furthest reaching D-path in diagonal k.
Namely, take the further reaching of (x’,y’+1) and (x"+1,y") in diagonal k and then follow diagonal edges until it is
no longer possible to do so or until the boundary of the edit graph is reached.``` The normal way is to get both points which extends from `v[k - 1]` and `v[k + 1]` and figure out which is a further reach path. But this will lead a double-culculate. Here's proof why only check `V[k − 1] < V[k + 1]` works:

lemma4:
if `v[k - 1] < v[k + 1]`, then path followed by `v[k + 1]` with a vertical edge with a snake will be the further rearched path in diagonal k.

proof:
let's make `v[k - 1]` to `x1` and `v[k + 1]` to `x2`. so the point followed by `x1` in diagonal k is `(x1 + 1, x1 + 1 - k)`(go right), the point followed by `x2` is `(x2, x2 - k)`(go down); the y position is useless here.
then the problem changes to: `if x1 < x2, then x1 + 1 <= x2`
since `x1 < x2 -> x2 - x1 > 0`
assume that `x1 + 1 > x2`, then `x2 - x1 < 1`, so `0 < x2 - x1 < 1`. But in edit graph, the basic move is 1, the `0 < x2 - x1 < 1` will never happen, so the assumption is wrong, so `x1 + 1 <= x2`.  
