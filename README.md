# B-Trees
## Objectives
* The idea of external searches
* Multiway Search Trees
* The definition of B-Trees
* Insertion into B-trees (optional)
* Deletion from B-trees (optional)
## Motivation
* Internal search
  - The data structure is kept in RAM
  - E.g., binary search trees and AVL trees: performance is proportional to their height
* External search
  - Locate and retrieve records stored in hard disks
    - Search trees are expensive when they are stored on disl, because disk access are incredible expensive
    - Access time: Milliseconds
    - Access units: Pages or blocks (usually 1 KB or more)
  - B-trees are designed for external searches
    - Minimize the number of disk accesses
    - More branching means less height and better performance

## Multiway Search Trees
* Or m-ary search tree: m is the order
  - The height is roughly logMN
  - If k<= m is the number of children, then the node contains exactly k-1 keys, which partition all the keys into k subsets consisting of
    - all the keys less than the first key in the node
    - all the keys between a pair of keys in the node, and
    - all keys greater than the largest key in the node
  - <img width="873" alt="Screen Shot 2022-07-07 at 6 27 23 PM" src="https://user-images.githubusercontent.com/89602311/177887776-1c9c7a17-ed7c-4642-883e-dfb83bb67348.png">
* Another 5-way search tree
  - <img width="751" alt="Screen Shot 2022-07-07 at 6 28 29 PM" src="https://user-images.githubusercontent.com/89602311/177887869-af47418b-239d-45c8-8f7f-a6f5263a6fc0.png">
## Balanced Multiway Tree: B-Trees
* Motivation (minimizing disk accesses)
  - Reduce then height of the tree as much as possible
* Solution 
  - No empty subtrees appear above the leaves
    - The division of keys in subsets is efficient
  - All leaves stay on the same level
    - Guarantee the worst case performace
  - Every internal (non-leaf) node has at least some minimal number of children
## B-Tree: Definiton
* A B-Tree of order m is an m-way search tree in which
  - All leaves are on the same level
  - All internal nodes except the root have at most m nonempty children, and at least |- m/2 -| nonempty children
  - The number of keys in each internal node is one less than the number of its nonempty children, and these keys partition the keys in the children in the fashiion of a search tree
  - The root has most m children, but may have as few as two if u=it is not a leaf, or none if the tree consists of the root alone
  - Note: in many implementations, only leaf nodes hold the data (less heavy operations on splitting, etc)
* A B-tree of order 5
  - <img width="660" alt="Screen Shot 2022-07-12 at 4 06 40 PM" src="https://user-images.githubusercontent.com/89602311/178595361-db98fdae-56c7-46ee-965b-d70c8e37303a.png">
* Another B-tree of order 5
  - Each node represents a disk block, we choose M on the basis of the size of the items that are being stores.
  - <img width="495" alt="Screen Shot 2022-07-12 at 5 04 42 PM" src="https://user-images.githubusercontent.com/89602311/178603448-e554d15a-add0-4524-8201-b7ce921858db.png">
* Assume the size of a block in the disk is 8192 bytes (8 KB)
* How to decide M?
  - Greedy: as large as possible -> height will be as small as possible
  - For internal nodes: store M-1 keys,
  - If each key is big int (32 bytes)
    - 32M - 32 <= 8192 -> M = 228
  - If we customized data type, e.g. its size is 256 byts
    - 265M <= 8192 -> M = 228
  - Note: in many implementation, the number of data nodes in each leaf block could be different from M, i.e., L data items for a leaf block and L != M, to get better use of internal nodes.
## B-Tree: Insertion (optional)
* B-trees grow in a bottum-up fashion
  - Due to the condition that all leaves be on the same level
  - Similar as binary search trees: new node as a leaf
* General idea
  - Search the tree for the new key
    - If the key is not truly new, this search will terminate in dailure at a leaf
  - Insert the new key into the leaf node
    - If the node was not previously full, then the insertion is finished
    - Overflow: If the leaf node is full, the node splits into two nodes, side by side on the same level
    - When a node splits, insert the median key of the old leaf into its parent node
      - Repeat the splitting process in the parent node if necessary
    - When a key is added to a full root, then the root splits in two
      - The median key is sent upward becomes a new root
      - This is the only time when the B-tree grown in height
* Example: B-tree insertion (order: 5)
  - <img width="626" alt="Screen Shot 2022-07-14 at 3 25 19 PM" src="https://user-images.githubusercontent.com/89602311/179076850-6b3a2448-27e6-4a76-b9bf-5438ab90c52e.png">
  - <img width="559" alt="Screen Shot 2022-07-14 at 3 25 34 PM" src="https://user-images.githubusercontent.com/89602311/179076885-da0dfaac-a91b-4cbe-b1fb-847a5552f12d.png">
  - <img width="619" alt="Screen Shot 2022-07-14 at 3 25 47 PM" src="https://user-images.githubusercontent.com/89602311/179076914-e8b1b05c-f869-42fb-b407-be91ce98a8a2.png">
## B-Tree: Deletion (optional)
* Related to the constraint of minimum keys in a node (|- m/2 -|)
* General method
  - If the entry to be deleted isnot in a leaf, then its immediate predecessor (or successor) is guaranteed to be in a leaf
  - The immediate predecessor (or successor) is promosted into the position of the deleted entry, and the entry is deleted from the leaf
    - Similar as the deletion on a BST
  - If the leaf contains more than the minimim number of entries, then one of them can be deleted with no further action
  - If the leaf contains the minimum number of records (underflow), then we first look at the two sibling leaves (or, in the case of a node in the outside, one leaf) that are immediately adjacent to each other and are children of the same node
    - If one of these has more than the minimum number of entries, then one of the entries can be move into the parent node, and the entry from the parent moved into the leaf where the deletion is occurring
    - If the adjacent leaf has only the minimum number of entries, then the two leaves and the median entry from the parent can all be combined as one new leaf, which will contain no more than the maximum number of entries allowed. 
  - If this step leaves the parent node with too few entries, then the proccess propogates upwatd. In the extreme case, the last entry is removed from the root, and then the height of the tree decreases
* Example: B-tree deletion (order: 5)
  - <img width="591" alt="Screen Shot 2022-07-14 at 3 32 03 PM" src="https://user-images.githubusercontent.com/89602311/179077876-3b44a846-5159-400d-befa-7295829801a6.png">
  - <img width="597" alt="Screen Shot 2022-07-14 at 3 32 21 PM" src="https://user-images.githubusercontent.com/89602311/179077942-fa049478-34cd-4b05-8a8e-713f3dbac2c3.png">
* When underflow occurs
  - Check the number of entries/keys in the direct neighboring node: > |- m/2 -| ?
* <img width="563" alt="Screen Shot 2022-07-14 at 3 33 14 PM" src="https://user-images.githubusercontent.com/89602311/179078101-9ae32711-6833-46ac-9c29-3d1dac67c66e.png">
## Self test
* How to implement a node for an m-way search tree? (make it simple: still stored in memory, before being flushed into the disk)
* How to traverse an m-way search to get the natural order?
  - <img width="348" alt="Screen Shot 2022-07-14 at 3 34 14 PM" src="https://user-images.githubusercontent.com/89602311/179078264-da7f26af-a0e2-4ec1-b0b4-36c91f55554f.png">


  
