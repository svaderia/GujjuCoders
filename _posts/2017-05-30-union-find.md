---
layout: post
title: Union Find
author: mdp98
category: Blog
tags: [Data Structures, Algorithms, Competitive Programming, Java]
---

Efficiency is an important parameter when it comes to algorithms. Efficiency of algorithms sometimes depends on the type of data structure on which the algorithm is implemented i.e. certain algorithms work better when implemented on a certain specific data structure. **Union Find** or **Disjoint Set Union** is an example of one such data structure.

Suppose we have a set of N elements. Now, it might be possible to classify these N elements into specific groups  i.e. union. For example, consider 5 balls of which 3 are red coloured and 2 are green coloured. Thus, we can create two groups of balls based on their colour and operations to be carried out on balls with similar colour can be carried out with ease.

There are different approaches to converting the above description to code. However, some of the approaches are not so efficient in comparison to others. We shall discuss them one by one.

**_1. Quick Find (Eager Approach)_**

Suppose we have an array of length 10 where the indices represent the 10 elements which are 0,1,2,3,4,5,6,7,8 and 9. The indices having the same entries are said to be in the same group.
For example, here {0,5,6},{1,2,7} and {3,4,8,9} are groups.

| i | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| id[i] | 0 | 1 | 1 | 8 | 8 | 0 | 0 | 1 | 8 | 8 |

The code implementation would be something like this.

```java
public class QuickFind{
    private int[] id;

    //set id of each object to itself
    public QuickFind(int n){
        for (int i=0; i<n; i++){
            id[i]=i;
        }
    }

    //check whether p and q are in the same group
    public boolean connected(int p, int q){
        return id[p]==id[q];
    }

    //change entries with id[p] to id[q]
    public void union(int p, int q){
        int idP = id[p];
        int idQ = id[q];
        for (int i=0; i<id.length; i++){
            if (id[i]==idP){
                id[i]=idQ;
            }
        }
    }
}
```
If we check the cost model of Quick Find, we get this

| algorithm | initialize | union | find |
|---|---|---|---|
| quick find | n | n | 1 |

So, it takes n<sup>2</sup> array accesses to proccess a sequence of n union commands on n objects which is very costly and isn't scalable for huge amount of input data. Hence, an improvement is required which takes us to our next approach.

**_2. Quick Union (Lazy Approach)_**

In this approach, instead of changing entries of all elements in the same group, we create trees of elements belonging to the same group and thus, we have a structure similar to that of a forest made up of trees. Relation between the elements is defined on the basis of roots. All the elements of the same group eventually have the same root. Root of some element i is given by id[id[id[...id[i]...]]] where you need to keep going until there is no change in the entry. I know this might be a little tough to understand but bear with me, will you?
Consider this example,

| i | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| id[i] | 0 | 1 | 9 | 4 | 9 | 6 | 6 | 7 | 8 | 9 |

Here, id[3]=4, id[4]=9, id[9]=9. Thus, 9 is the root of 3.
And to merge two elements p and q, just set the id of p's root to the id of q's root. Thus, instead of changing all the entries, you just have to change one entry.

If we look at the code, 

```java
public class QuickUnion{
    private int[] id;

    //set id of each element to itself
    public QuickUnion(int n){
        for (int i=0; i<n; i++){
            id[i]=i;
        }
    }

    //get root of an element
    private int root(int i){
        while (i!=id[i]){
            i=id[i];
        }
        return i;
    }

    //check if p and q have the same root
    public boolean connected(int p, int q){
        return root(p)==root(q);
    }

    //change root of p to root of q
    public void union(int p, int q){
        int i = root(p);
        int j = root(q);
        id[i]=j;
    }
}
```
Let's have a look at the cost model of Quick Union.

| algorithm | initialize | union | find |
|---|---|---|---|
| quick union | n | n<sup>*</sup> | n |

Here, * signifies cost of finding roots.

The cost model signifies that if the tree becomes too tall, cost of finding the root would increase because tall trees would require more array accesses. Hence, we need to ensure that the tree doesn't get too tall.

Here's where **_Weighted Quick Union_** comes into picture. 
In weighted quick union, we also keep track of size of the tree. In order to make sure that the tree doesn't get tall, we would always link root of the smaller tree to root of the larger tree i.e. we would always put the smaller tree lower to the larger tree.

So, along with the id[] array, we will also maintain a size[] array. The only modification in the quick union code implementation would be 
```java
public void union(int p, int q){
    int i = root(p);
    int j = root(q);
    if(i==j){
        return;
    }
    if(size[i]>size[j]){
        id[j]=i;
        size[i] += size[j];
    }
    else{
        id[i]=j;
        size[j] += size[i];
    }
}
```

The cost model looks something like this

| algorithm | initialize | union | find |
|---|---|---|---|
| weighted quick union | n | log(n) | log(n) |

This is pretty efficient and scalable. But this can still be improved.

While computing root of an element, if we set each element such that it points to its gradparent, this would reduce the path length to half. This is also known as **Path Compression**. This would also make the tree almost flat.
Only one line of code has to be added to the root method.
```java
private int root(int p){
    while (i != id[i]){
        id[i] = id[id[i]];
        i = id[i];
    }
    return i;
}
```
Worst case scenario for a weighted quick union with path compression would be log<sup>*</sup>n where log<sup>*</sup>n is the iterative function which computes the number of times you have to take log of n till value of n reaches 1. log<sup>*</sup>n is much better than log(n), just in case you needed a perspective.
