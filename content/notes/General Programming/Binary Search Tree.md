#trees

# Binary Tree

- Nodes can have up to two children

## Implementation

![[Images/Algorithmics Notes.png]]

%%[[Git Ignore/Heavy Stuff/Matthew Barnes Notes/Algorithmics Notes.pdf#page=22&rect=69,440,530,729|Algorithmics Notes, p.22]]%%

# Binary Search Tree

- Stores comparable elements
- Elements are ordered
- Left child must be smaller than the parent, right child must be bigger than the parent
- Worst case search is $\Theta(\text{The height of the tree})$

## Search

![[Images/Algorithmics Notes 1.png]]

%%[[Git Ignore/Heavy Stuff/Matthew Barnes Notes/Algorithmics Notes.pdf#page=23&rect=69,300,529,533|Algorithmics Notes, p.23]]%%

## Insert

%%[[Git Ignore/Heavy Stuff/Uni PDFs/algorithmics rotated cropped.pdf#page=22&rect=208,354,405,420|Code from Original Notes]]%%

```java
public boolean add(E element) {
    // If the root is empty, add the node
    if (root == null) {
        root = new Node<E>(element, null);
        size++;
        return true;
    } else {
        Node<E> temp = root;
        while (true) {
            // Compare the current node to the element being searched for
            int comp = ((Comparable<E>)element).compareTo(temp.element);
            
            // If it is the same element, return false as the element cannot be added
            if (comp == 0)
                return false;

            // If the element precedes the current node, check if the left node is empty
            if (comp < 0) {
                if (temp.left != null)
                    // Otherwise, move on to the left child and repeat the process
                    temp = temp.left;
                else {
                    // If so, add the new element and return true
                    temp.left = new Node<E>(element, temp);
                    size++;
                    return true;
                }
            } else {
                // If the element exceeds the current node, check if the right node is empty
                if (temp.right != null)
                    // Otherwise, move on to the right child and repeat the process
                    temp = temp.right;
                else {
                    // If so, add the new element and return true
                    temp.right = new Node<E>(element, temp);
                    size++;
                    return true;
                }
            }
        }
    }
}

```

## Delete

```java
if (e.left == null && e.right == null) { 
    if (e == e.parent.left) 
        e.parent.left = null; 
    else 
        e.parent.right = null; 
} else if (e.right == null) { 
    if (e == e.parent.left) 
        e.parent.left = e.left; 
    else 
        e.parent.right = e.left; 
    e.left.parent = e.parent; 
} else if (e.left == null) { 
    if (e == e.parent.left) 
        e.parent.left = e.right; 
    else 
        e.parent.right = e.right; 
    e.right.parent = e.parent; 
}
```

### Code from Original Notes

![[Images/algorithmics rotated cropped 1.png]]

%%[[Git Ignore/Heavy Stuff/Uni PDFs/algorithmics rotated cropped.pdf#page=26&rect=54,161,418,570|Code from Original Notes]]%%