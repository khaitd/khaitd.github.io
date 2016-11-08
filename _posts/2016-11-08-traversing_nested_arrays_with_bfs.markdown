---
layout: post
title:  "Traversing Nested Arrays with BFS"
date:   2016-11-08 18:10:17 -0500
---


Arrays are one the most common data types in computer science. They can be used to store data structures including other arrays in an efficient and accessable manner. But often we run into nested data structures such as nested arrays that don't always allow for straight-forward traversal and retrieval of their elements. Such as in the following occurrence:

```
const collections = [1, [2, [4, [5, [6]], 3]]]
```

How might we go about returning the number 6 that is stored in the array? We take a look at the following code from the **Traversal Nested Objects** lab on Learn:

```
[1, [2, [4, [5, [6]], 3]]] // collections
[2, [4, [5, [6]], 3]]      // collections[1]
[4, [5, [6]], 3]           // collections[1][1]
[5, [6]]                   // collections[1][1][1]
[6]                        // collections[1][1][1][1]
6                          // collections[1][1][1][1][0]
```

As you can see by accessing index 1 of the collections array we are returned an additional array which was stored as the second element of collections. We must dig deeper three more times in this way to return [6] which is much closer yet still not the number we are looking for since it is still an array object. By calling the 0th index of this array we can finally return the number 6 from our collection.

In the case where we have a certian criteria by which we want to find an element in an array we can construct a basic for loop to do the trick, incorporated in the following find function:

```
function find(array, criteriaFn) {
  for (let i = 0, l = array.length; i < l; i++) {
    if (criteriaFn(array[i])) {
      return array[i]
    }
  }
}
```

This function will iterate through the inputted array and have a conditional check whether the element matches the criteria, returning it if it does or moving on to the next iteration otherwise.

You may have noticed that our find function will work on a flat array, but will fail to work on a nested array such as our collections array since well need to find a way to move down the levels of the array.

```
//breath-first search
function find(array, criteriaFn) {
  
  let current = array
  let next = []
 
 
  while (current) {
    
    if (criteriaFn(current)) {
      return current
    }
 
   
    if (Array.isArray(current)) {
      for (let i = 0, l = current.length; i < l; i++) {
        next.push(current[i])
      }
    }
 
 
    current = next.shift()
  }
 
  // if we haven't
  return null
}
```

This is the Breath-first search algorithm and it is commonly used to search through nested objects. The algorithm got its name because it looks through the siblings at the current level of the nested object before moving downward to futher levels. A related algorithm - the depth-first search runs similarly but moves down through the levels before covers the breath of a curretn level. A common use for Breath-first search algorithm is commonly used to find the shortest distance between two nodes, while a depth-first search is commonly used to identify a cycle in a graph. 

![](https://upload.wikimedia.org/wikipedia/commons/thumb/3/33/Breadth-first-tree.svg/300px-Breadth-first-tree.svg.png)

So to reiterate, the main idea behind a breath-first search is to access all the nodes of a parent before moving to the next level. So in this example we would start at one as our root node and checking 2, 3 and 4. Afterwards moving chronologically to 2 and exhausting all its nodes. Once again this is in contrast to a depth first search which would go down levels until it reaches the lowest level of tree before moving to a different node.


