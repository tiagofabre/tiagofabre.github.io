---
layout: post
title: "Binary search tree"
subtitle: "Introductory overview"
comments: true
categories: "algorithms data-structures"
tags: "english"
---

# Binary Search Tree (BST)

Is a tree with a maximum of two children per node and it's organization enables searches with `O(log n)` time complexity. Being each left node lower than it's parent and right node higher than its parent.

```
   5
  / \
 2   8
```

# Nodes

```java
class Node {
    int key;
    Node left, right;

    Node(int item) {
        key = item;
        left = right = null;
    }
}
```

# Tree

```java
class BinarySearchTree {
    Node root;

    public Node insert(int key) {
        return insertKey(root, key);
    }

    private Node insertKey(Node root, int key) {
        if(root == null) {
            root = new Node(key);
            return root;
        }

        if(key == root.key) {
            // key already exists;
            return root;                        
        } else if(key < root.key) {
            root.left = insertKey(root.left, key);
        } else if(key > root.key) {
            root.right = insertKey(root.right, key);
        }

        return root;
    }
}
```

# Search

```java
public Optional<Node> find(int key) {
    return findKey(root, key);
}

private Optional<Node> findKey(Node root, int key) {
    if(root == null) 
        return Optional.of(root);

    if(key == root.key) 
        return Optional.of(root);

    if(key < root.key) 
        return findKey(root.left, key);

    if(key > root.key) 
        return findKey(root.right, key);

    return Optional.of(root);
}
```

# Traversal

## pre-order
```java
void preOrderTraversal(Node root) {
    if(root == null) return;
    System.out.println(root.key);
    preOrderTraversal(root.left);
    preOrderTraversal(root.right);
}
```

## in-order
```java
void inOrderTraversal(Node root) {
    if(root == null) return;
    preOrderTraversal(root.left);
    System.out.println(root.key);
    preOrderTraversal(root.right);
}
```

## post-order
```java
void postOrderTraversal(Node root) {
    if(root == null) return;
    preOrderTraversal(root.left);
    preOrderTraversal(root.right);
    System.out.println(root.key);
}
```

## level order

```java
void levelOrderTraversal(Node root) {
    if(root == null) return;
    LinkedList<Node> nodes = new LinkedList<Node>();
    nodes.addLast(root);

    while(!nodes.isEmpty()) {
        var current = nodes.pollFirst();
        System.out.println(current.key);

        if(current.left != null)
            nodes.addLast(current.left);
        if(current.right != null)
            nodes.addLast(current.right);
    }
}
````

# Min and max

```java
Optional<Integer> getMax(Node root) {
    if(root == null) 
        return Optional.of(null);
    if(root.right == null)
        return Optional.of(root.key);
    return getMax(root.right);
}

Optional<Integer> getMin(Node root) {
    if(root == null) 
        return Optional.of(null);
    if(root.left == null)
        return Optional.of(root.key);
    return getMin(root.left);
}
```