---
layout: post
title: "Red-Black tree"
subtitle: "Source code and rotation details"
comments: true
categories: "algorithms data-structures"
tags: "english"
---

## Rotation

<style>
.tree-rotation {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
 }   

</style>

<script>

let sketch = function(p) {
    p.setup = function() {
        p.textSize("30px");
        p.createCanvas(900, 600);
        rSlider = p.createSlider(0, 3, 0);
    }

    p.draw = function() {
        p.background(220);
        let xOffset = -60;
        let yOffset = 90;
        let xTextOffset = -7;
        let yTextOffset = 4;
        let step = rSlider.value();
        
        if(step == 0) {
            p.line(400 + xOffset, 50 + yOffset, 500 + xOffset, 130 + yOffset);
            p.line(400 + xOffset, 50 + yOffset, 300 + xOffset, 130 + yOffset);

            p.line(500 + xOffset, 130 + yOffset, 580 + xOffset, 210 + yOffset);
            p.line(500 + xOffset, 130 + yOffset, 420 + xOffset, 210 + yOffset);

            p.line(580 + xOffset, 210 + yOffset, 520 + xOffset, 280 + yOffset);
            p.line(580 + xOffset, 210 + yOffset, 660 + xOffset, 290 + yOffset);

            
            p.ellipse(400 + xOffset, 50 + yOffset, 40, 40);
            p.ellipse(500 + xOffset,130 + yOffset, 40, 40); // root right <-- x
            p.ellipse(300 + xOffset,130 + yOffset, 40, 40); // root left

            p.ellipse(420 + xOffset, 210 + yOffset, 40, 40); // right left
            p.ellipse(580 + xOffset, 210 + yOffset, 40, 40); // right right <-- y

            p.ellipse(520 + xOffset, 290 + yOffset, 40, 40); // bottom left
            p.ellipse(660 + xOffset, 290 + yOffset, 40, 40); // bottom right
            
            p.text(' 7', 400 + xOffset + xTextOffset, 50 + yOffset + yTextOffset);
            p.text('11', 500 + xOffset + xTextOffset, 130 + yOffset + yTextOffset);
            p.text(' 4', 300 + xOffset + xTextOffset, 130 + yOffset + yTextOffset);
            
            p.text(' 9', 420 + xOffset + xTextOffset, 210 + yOffset + yTextOffset);
            p.text('18', 580 + xOffset + xTextOffset, 210 + yOffset + yTextOffset);
            
            p.text('14', 520 + xOffset + xTextOffset, 290 + yOffset + yTextOffset);
            p.text('19', 660 + xOffset + xTextOffset, 290 + yOffset + yTextOffset);
            
        } else if (step == 1) {
            
            p.line(400 + xOffset, 50 + yOffset, 500 + xOffset, 130 + yOffset);
            p.line(400 + xOffset, 50 + yOffset, 300 + xOffset, 130 + yOffset);

            // line(500 + xOffset, 130 + yOffset, 580 + xOffset, 210 + yOffset);
            p.line(500 + xOffset, 130 + yOffset, 420 + xOffset, 210 + yOffset);

            p.line(500 + xOffset, 130 + yOffset, 520 + xOffset, 280 + yOffset);
            p.line(580 + xOffset, 210 + yOffset, 660 + xOffset, 290 + yOffset);

            p.ellipse(400 + xOffset, 50 + yOffset, 40, 40);
            p.ellipse(500 + xOffset,130 + yOffset, 40, 40); // root right <-- x
            p.ellipse(300 + xOffset,130 + yOffset, 40, 40); // root left

            p.ellipse(420 + xOffset, 210 + yOffset, 40, 40); // right left
            p.ellipse(580 + xOffset, 210 + yOffset, 40, 40); // right right <-- y

            p.ellipse(520 + xOffset, 290 + yOffset, 40, 40); // bottom left
            p.ellipse(660 + xOffset, 290 + yOffset, 40, 40); // bottom right
            
            p.text(' 7', 400 + xOffset + xTextOffset, 50 + yOffset + yTextOffset);
            p.text('11', 500 + xOffset + xTextOffset, 130 + yOffset + yTextOffset);
            p.text(' 4', 300 + xOffset + xTextOffset, 130 + yOffset + yTextOffset);
            
            p.text(' 9', 420 + xOffset + xTextOffset, 210 + yOffset + yTextOffset);
            p.text('18', 580 + xOffset + xTextOffset, 210 + yOffset + yTextOffset);
            
            p.text('14', 520 + xOffset + xTextOffset, 290 + yOffset + yTextOffset);
            p.text('19', 660 + xOffset + xTextOffset, 290 + yOffset + yTextOffset);
        } else if (step == 2) {
            
            p.line(400 + xOffset, 50 + yOffset, 500 + xOffset, 130 + yOffset);
            p.line(400 + xOffset, 50 + yOffset, 300 + xOffset, 130 + yOffset);

            p.line(500 + xOffset, 130 + yOffset, 580 + xOffset, 100 + yOffset);
            p.line(500 + xOffset, 130 + yOffset, 420 + xOffset, 210 + yOffset);

            p.line(500 + xOffset, 130 + yOffset, 520 + xOffset, 280 + yOffset);
            p.line(580 + xOffset, 100 + yOffset, 660 + xOffset, 290 + yOffset);

            p.ellipse(400 + xOffset, 50 + yOffset, 40, 40);
            p.ellipse(500 + xOffset,130 + yOffset, 40, 40); // root right <-- x
            p.ellipse(300 + xOffset,130 + yOffset, 40, 40); // root left

            p.ellipse(420 + xOffset, 210 + yOffset, 40, 40); // right left
            p.ellipse(580 + xOffset, 100 + yOffset, 40, 40); // right right <-- y

            p.ellipse(520 + xOffset, 290 + yOffset, 40, 40); // bottom left
            p.ellipse(660 + xOffset, 290 + yOffset, 40, 40); // bottom right
            
            p.text(' 7', 400 + xOffset + xTextOffset, 50 + yOffset + yTextOffset);
            p.text('11', 500 + xOffset + xTextOffset, 130 + yOffset + yTextOffset);
            p.text(' 4', 300 + xOffset + xTextOffset, 130 + yOffset + yTextOffset);
            
            p.text(' 9', 420 + xOffset + xTextOffset, 210 + yOffset + yTextOffset);
            p.text('18', 580 + xOffset + xTextOffset, 100 + yOffset + yTextOffset);
            
            p.text('14', 520 + xOffset + xTextOffset, 290 + yOffset + yTextOffset);
            p.text('19', 660 + xOffset + xTextOffset, 290 + yOffset + yTextOffset);
        } else {
            
            p.line(400 + xOffset, 50 + yOffset, 580 + xOffset, 100 + yOffset);
            p.line(400 + xOffset, 50 + yOffset, 300 + xOffset, 130 + yOffset);

            p.line(500 + xOffset, 130 + yOffset, 580 + xOffset, 100 + yOffset);
            p.line(500 + xOffset, 130 + yOffset, 420 + xOffset, 210 + yOffset);

            p.line(500 + xOffset, 130 + yOffset, 520 + xOffset, 280 + yOffset);
            p.line(580 + xOffset, 100 + yOffset, 660 + xOffset, 290 + yOffset);

            p.ellipse(400 + xOffset, 50 + yOffset, 40, 40);
            p.ellipse(500 + xOffset,130 + yOffset, 40, 40); // root right <-- x
            p.ellipse(300 + xOffset,130 + yOffset, 40, 40); // root left

            p.ellipse(420 + xOffset, 210 + yOffset, 40, 40); // right left
            p.ellipse(580 + xOffset, 100 + yOffset, 40, 40); // right right <-- y

            p.ellipse(520 + xOffset, 290 + yOffset, 40, 40); // bottom left
            p.ellipse(660 + xOffset, 290 + yOffset, 40, 40); // bottom right
            
            
            p.text(' 7', 400 + xOffset + xTextOffset, 50 + yOffset + yTextOffset);
            p.text('11', 500 + xOffset + xTextOffset, 130 + yOffset + yTextOffset);
            p.text(' 4', 300 + xOffset + xTextOffset, 130 + yOffset + yTextOffset);
            
            p.text(' 9', 420 + xOffset + xTextOffset, 210 + yOffset + yTextOffset);
            p.text('18', 580 + xOffset + xTextOffset, 100 + yOffset + yTextOffset);
            
            p.text('14', 520 + xOffset + xTextOffset, 290 + yOffset + yTextOffset);
            p.text('19', 660 + xOffset + xTextOffset, 290 + yOffset + yTextOffset);
        }
    }
}

new p5(sketch, 'test-bugs');
</script>

<div id="test-bugs" class="tree-rotation"></div>

```java
public void leftRotate(Node x) {
    var y = x.right;             // y is the x's right child
    
    // y's child
    x.right = y.left;           // y's child goes to x
    if(y.left != NIL) {         // if y child wasn't null, change it's parent
        y.left.parent = x;
    }
    
    // fix x's parent
    y.parent = x.parent;
    if(x.parent == NIL) {           // if X is the ROOT
        this.root = y;    
    } else if(x == x.parent.left) {  // if x is left child
        x.parent.left = y;    
    } else {                        // if x is right child
        x.parent.right = y;
    }

    // swap x with y
    y.left = x;
    x.parent = y;
}
```

## Complete source code

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Scanner;

class RedBlackTree {
    public enum Colors  {
        RED, BLACK;
    }
    public class Node {
        int key;
        Colors color;
        Node left, right, parent;

        public Node(int key) {
            this.key = key;
            this.color = Colors.RED;
        }
        
        private String keyOrNull(Node node) {
            return (parent != null ? parent.key : "null")
        }

        private String interleave(String n) {

        }

        @Override
        public String toString() {
            
            String parentStr = keyOrNull(parent);
            String leftStr = keyOrNull(left);
            String rightStr = keyOrLeft(right);

            return String.format("{K:%1 C:%2 P:%3 L:%4 R:%5}", key, color, parentStr, leftStr, rightStr);
        }
    }
    public Node root, NIL;
    RedBlackTree() {
        Node nilNode = new Node(0);
        nilNode.color = Colors.BLACK;
        this.NIL = nilNode;
        this.root = nilNode;
    }
    
    @Override
    public String toString() {
        if(this.root == null) return "";
        
        StringBuilder strBuilder = new StringBuilder();
        LinkedList<Node> nodes = new LinkedList<Node>();
         
        nodes.addLast(this.root);

        while(!nodes.isEmpty()) {
            var current = nodes.pollFirst();
            strBuilder.append(current.toString());
            if(current.left != null)
                nodes.addLast(current.left);
            if(current.right != null)
                nodes.addLast(current.right);
        }
        
        return strBuilder.toString();
    }
    
    @Override
    public boolean equals(Object rb) {
        return toString().equals(rb.toString());
    }
    
    private void prettyPrintTree(Node node, String prefix, boolean isLeft) {
        if (node == null) {
            System.out.println("Empty tree");
            return;
        }

        if (node.right != null) {
            prettyPrintTree(node.right, prefix + (isLeft ? "│    " : "     "), false);
        }

        System.out.println(prefix + (isLeft ? "└─── " : "┌─── ") + node.key + " " + node.color);

        if (node.left != null) {
            prettyPrintTree(node.left, prefix + (isLeft ? "     " : "│    "), true);
        }
    }
    
    public void print(){
       prettyPrintTree(root,  "", true); 
    }
    
    public Node find(Node root, int key) {
        if(root == null)
            return null;
        
        if(root.key == key)
            return root;
        
        if(key < root.key)
            return find(root.left, key);
        
        if(key > root.key)
            return find(root.right, key);
        
        return null;
    }
    
    private void insertFixUp(Node z) {
        while(z.parent.color == Colors.RED) {
            if(z.parent == z.parent.parent.left) {
                var y = z.parent.parent.right;
                if(y.color == Colors.RED) {
                    z.parent.color = Colors.BLACK;
                    y.color = Colors.BLACK;
                    z.parent.parent.color = Colors.RED;
                    z = z.parent.parent;
                } else {
                    if(z == z.parent.right) {
                        z = z.parent;
                        this.leftRotate(z);
                    }
                    z.parent.color = Colors.BLACK;
                    z.parent.parent.color = Colors.RED;
                    this.rightRotate(z.parent.parent);
                }
            } else {
                var y = z.parent.parent.left;      
                if(y.color == Colors.RED) {
                    z.parent.color = Colors.BLACK;
                    y.color = Colors.BLACK;
                    z.parent.parent.color = Colors.RED;
                    z = z.parent.parent;
                } else {
                    if(z == z.parent.left) {
                        z = z.parent;
                        this.rightRotate(z);
                    }
                    z.parent.color = Colors.BLACK;
                    z.parent.parent.color = Colors.RED;
                    this.leftRotate(z.parent.parent);
                }
            }
        }
        this.root.color = Colors.BLACK;
    }
    
    private void insert(Node z) {
        Node x = root;
        Node y = NIL;
        
        // find the position and store it's parent
        while(x != NIL) {
            y = x;
            if(z.key < x.key) {
                x = x.left;
            } else {
                x = x.right;
            }
        }
        
        z.parent = y;
        // check which child it should replace
        if(y == NIL) { // if tree is empty
            root = z;
        } else if(z.key < y.key) {
            y.left = z;
        } else {
            y.right = z;
        }
        
        z.left = NIL;
        z.right = NIL;
        z.color = Colors.RED;
        
        this.insertFixUp(z);
    }
    
    public Node insert(int key) {
        var newNode = new Node(key);
        this.insert(newNode);
        return newNode;
    }
    
    public void addAll(int[] items) {
        for(var e: items) insert(e);
    }
    
    public void addAll(List<Integer> items) {
        for(var e: items) insert(e);
    }
    
    public void leftRotate(Node x) {
        var y = x.right;             // y is the x's right child
        
        // y's child
        x.right = y.left;           // y's child goes to x
        if(y.left != NIL) {         // if y child wasn't null, change it's parent
            y.left.parent = x;
        }
        
        // fix x's parent
        y.parent = x.parent;
        if(x.parent == NIL) {           // if X is the ROOT
            this.root = y;    
        } else if(x == x.parent.left) {  // if x is left child
            x.parent.left = y;    
        } else {                        // if x is right child
            x.parent.right = y;
        }

        // swap x with y
        y.left = x;
        x.parent = y;
    }
    
    public void rightRotate(Node y) {
        var x = y.left;
        
        y.left = x.right;
        
        if(x.right != NIL) {
            x.right.parent = y;
        }
        
        x.parent = y.parent;
        
        if(y.parent == NIL) {           // if y is the ROOT
            this.root = x;    
        } else if(y == y.parent.right) {  // if y is right child
            y.parent.right = x;    
        } else {                        // if y is left child
            y.parent.left = x;
        }

        x.right = y;
        y.parent = x;
    }
    
    private void transplant(Node u, Node v) {
        if(u.parent == NIL)
            root = v;
        else if(u == u.parent.left)
            u.parent.left = v;
        else
            u.parent.right = v;
        v.parent = u.parent;
    }
    
    public Node minimum(Node x) {
      while(x.left != this.NIL)
        x = x.left;
      return x;
    }
    
    private void deleteFixup(Node x) {
        while(x != root && x.color == Colors.BLACK) {
            if(x == x.parent.left) {
                var w = x.parent.right;
                if(w.color == Colors.RED) {
                    w.color = Colors.BLACK;
                    x.parent.color = Colors.RED;
                    leftRotate(x.parent);
                    w = x.parent.right;
                }
                
                if(w.left.color == Colors.BLACK && w.right.color == Colors.BLACK) {
                    w.color = Colors.RED;
                } else {
                    if(w.right.color == Colors.BLACK) {
                        w.left.color = Colors.BLACK;
                        w.color = Colors.RED;
                        rightRotate(w);
                        w = x.parent.right;
                    }
                    w.color = x.parent.color;
                    x.parent.color = Colors.BLACK;
                    w.right.color = Colors.BLACK;
                    leftRotate(x.parent);
                    x = root;
                }
            } else {
                var w = x.parent.left;
                if(w.color == Colors.RED) {
                    w.color = Colors.BLACK;
                    x.parent.color = Colors.RED;
                    rightRotate(x.parent);
                    w = x.parent.left;
                }
                
                if(w.right.color == Colors.BLACK && w.left.color == Colors.BLACK) {
                    w.color = Colors.BLACK;
                    x = x.parent;
                } else {
                    if(w.left.color == Colors.BLACK) {
                        w.right.color = Colors.BLACK;
                        w.color = Colors.RED;
                        leftRotate(w);
                        w = x.parent.left;
                    }
                    w.color = x.parent.color;
                    x.parent.color = Colors.BLACK;
                    w.left.color = Colors.BLACK;
                    rightRotate(x.parent);
                    x = root;
                }
            }
        }
        x.color = Colors.BLACK;
    }
    
    public void delete(Node z) {
        var y = z;
        var yColor = y.color;
        Node x = new Node(0);
        if(z.left == NIL) {
            x = z.right;
            transplant(z, z.right);
        } else if(z.right == NIL) {
            z = z.left;
            transplant(z, z.left);
        } else {
            y = minimum(z.right);
            yColor = y.color;
            x = y.right;
            if(y != z.right) {
                transplant(y, y.right);
                y.right = z.right;
                y.right.parent = y;
            } else {
                x.parent = y;
            }
            transplant(z, y);
            y.left = z.left;
            y.left.parent = y;
            y.color = z.color;
        }
        if(yColor == Colors.BLACK) {
            deleteFixup(x);
        }
    }
}

public class Main {   
    public static void main(String[] args) { 
        RedBlackTree rbt1 = new RedBlackTree();
        
        // rbt1.addAll(new int[]{5, 4, 6, 7, 10, 2, 11,8, 9, 3, 22});        
        // rbt1.addAll(new int[]{7, 4, 11, 3, 6, 9, 18, 2, 14, 19, 12, 17, 22, 20});
        rbt1.addAll(new int[]{26, 17, 41, 14, 21, 30, 47, 10, 16, 19, 23, 28, 38, 7, 12, 15, 20, 35, 39, 3});
        
        rbt1.print();
        
        // rbt1.delete(rbt1.find(rbt1.root, 11));
        // rbt1.delete(rbt1.find(rbt1.root, 2));
        
        rbt1.print();
    }
}

// Main m = new Main(); m.main();
```