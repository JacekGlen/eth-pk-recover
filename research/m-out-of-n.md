Let's say we have input data. And we need to create `n` data blocks that:
- having any `m` of blocks, input data can be recovered,
- having less than `m` of blocks, input data cannot be recovered.

Resulting data blocks are understood as user secrets and input data is intended for a private key recovery.

# Algorithm 1.

This is a simpler one but provides larger user secrets in terms of byte length.

1. Divide input data into ${n\choose n-(m-1)}$ data chunks of equal length.
2. Include every chunk in exactly `n-(m-1)` blocks, the way that any two different chunks are not included in the same `n-(m-1)` blocks.

Proof of correctness.
There are ${n\choose n-(m-1)}$ chunks and ${n\choose n-(m-1)}$ different sets of `n-(m-1)` blocks.
Thus the algorithm is doable.
Assume you know at least `m` blocks and consider a given chunk.
The chunk is included in `n-(m-1)` blocks. It holds `m+n-(m-1)>n`.
Thus the chunk is included in at least one block you know and in consequence, all input data can be recovered.
Assume you know less than `m` blocks.
There exists `n-(m-1)` blocks that you do not know.
There exists a chunk that is included only in these `n-(m-1)` blocks.
Thus there exists a chunk you do not know and input data cannot be recovered.

Note that 32-byte chunks do not weaken a private key. It means that if an adversary knows all but one chunk, the private key is still secure.

An example, 3 out of 5. `X` means that a chunk is included. Note that there are ${5\choose 5-(3-1)}=10$ chunks.

| input data | block 0 | block 1 | block 2 | block 3 | block 4 |
|---|:---:|:---:|:---:|:---:|:---:|
| chunk 0 | X | X | X |   |   |
| chunk 1 | X | X |   | X |   |
| chunk 2 | X | X |   |   | X |
| chunk 3 | X |   | X | X |   |
| chunk 4 | X |   | X |   | X |
| chunk 5 | X |   |   | X | X |
| chunk 6 |   | X | X | X |   |
| chunk 7 |   | X | X |   | X |
| chunk 8 |   | X |   | X | X |
| chunk 9 |   |   | X | X | X |
