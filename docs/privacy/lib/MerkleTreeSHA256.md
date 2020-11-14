## `MerkleTreeSHA256`






### `constructor(uint256 _treeHeight)` (internal)





### `insertLeaf(bytes32 leafValue) → bytes32` (internal)

Insert a leaf into the Merkle Tree, update the root, and update any values in the (persistently stored) frontier.




### `insertLeaves(bytes32[] leafValues) → bytes32` (internal)

Insert multiple leaves into the Merkle Tree, and then update the root, and update any values in the (persistently stored) frontier.





### `NewLeaf(uint256 leafIndex, bytes32 leafValue, bytes32 root)`

Explanation of the Merkle Tree in this contract:
This is an append-only merkle tree; populated from left to right.
We do not store all of the merkle tree's nodes. We only store the right-most 'frontier' 
of nodes required to calculate the new root when the next new leaf value is added.
TREE (not stored)                       FRONTIER (stored)
0                                     ?
/             \
1                             2                     ?
/       \                     /       \
3             4               5               6             ?
/   \         /   \           /   \           /    \
7       8      9      10      11      12      13      14        ?
/  \    /  \   /  \    /  \    /  \    /  \    /  \    /  \
15  16  17 18  19  20  21  22  23  24  25  26  27  28  29  30      ?
level  row  width  start#     end#
4     0   2^0=1   w=0     2^1-1=0
3     1   2^1=2   w=1     2^2-1=2
2     2   2^2=4   w=3     2^3-1=6
1     3   2^3=8   w=7     2^4-1=14
0     4   2^4=16  w=15    2^5-1=30
height = 4
w = width = 2 ** height = 2^4 = 16
#nodes = (2 ** (height + 1)) - 1 = 2^5-1 = 31



### `NewLeaves(uint256 minLeafIndex, bytes32[] leafValues, bytes32 root)`





### `Output(bytes27 leftInput, bytes27 rightInput, bytes32 output, uint256 nodeIndex)`





