# B-Trees
## Objectives
* The idea of external searches
* Multiway Search Trees
* The definition of B-Trees
* Insertion into B-trees (optional)
* Deletion from B-trees (optional)
## Motivation
*
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
