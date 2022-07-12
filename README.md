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

  
