Let say we have input data. And we need to create `n` data sets that:
- having any `m` of data sets, input data can be recovered,
- having less than `m` of data sets, input data cannot be recovered.

Resulting data sets are understood as user secrets and input data is used to compute a private key:
```script
pk = keccak256(input_data)
```

# Algorithm 1.

This is simpler one but provides larger user secrets in terms of bytes length.

1. Divide input data into ${n\choose n-(m-1)}$ equal segments.
2. Assing each segment into a different `n-(m-1)`-element subset of data sets. There is ${n\choose n-(m-1)}$ such subsets. This assignment is a bijection.
3. A segment is included in its assigned data sets, and not included in others.

Proof of correctness. Assume you know at least `m` data sets and a given segment. 
The segment is included in `n-(m-1)` data sets. It holds `m+n-(m-1)>n`.
Thus the segment is included in at least one data set you know and all input data can be recovered.
Assume you know less than `m` data sets. 
There exists `n-(m-1)`-element subset of data sets that you do not know. 
You do not know a segment assigned to this subset.
Thus there exists a segment you do not know and input data cannot be recovered.

Note that 32 bytes segments do not weaken a private key. It means that, if an adversary knows `n-1` segments, the private key is still secure.

An example, 3 out of 5. `X` means that a segment is included. Note that there are ${5\choose 5-(3-1)}=10$ segments.

| input data | data set 0 | data set 1 | data set 2 | data set 3 | data set 4 |
|---|---|---|---|---|---|
| X | X | X | X |   |   |
| X | X | X |   | X |   |
| X | X | X |   |   | X |
| X | X |   | X | X |   |
| X | X |   | X |   | X |
| X | X |   |   | X | X |
| X |   | X | X | X |   |
| X |   | X | X |   | X |
| X |   | X |   | X | X |
| X |   |   | X | X | X |



