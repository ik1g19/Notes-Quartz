#trees

An AVL tree is a binary search tree such that
- the heights of the left and right subtree differ by at most 1
- the left and right subtrees are AVL trees

Guarantees the worst case AVL tree has logarithmic depth

Self-balancing

%%
[[Git Ignore/Heavy Stuff/Matthew Barnes Notes/Algorithmics Notes.pdf#page=27|Matthew Barnes Notes, p.27]]
[[Git Ignore/Heavy Stuff/Uni PDFs/algorithmics rotated cropped.pdf#page=29|My Notes, p.29]]
%%

# Performance

- Height of an AVL tree is Θ(log n)
- Searching is at worst Θ(log n)
- Insertion without balancing is Θ(log n), balancing takes an additional Θ(log n) steps in the worst case
- Deletion without balancing is Θ(log n) at worst (need to find the node first), balancing takes an additional Θ(log n) steps in the worst case

%%[[Git Ignore/Heavy Stuff/Matthew Barnes Notes/Algorithmics Notes.pdf#page=29&selection=10,0,26,52&color=yellow|Algorithmics Notes, p.29]]%%

# Implementation

Include additional information at each node indicating the balance of the subtrees

## Insertion

![[Images/algorithmics rotated cropped 2.png]]

%%[[Git Ignore/Heavy Stuff/Uni PDFs/algorithmics rotated cropped.pdf#page=31&rect=71,305,540,477&color=yellow|algorithmics rotated cropped, p.31]]%%

```java
static Node insert(Node node, int key) { 
      
        // Perform the normal BST insertion
        if (node == null) 
            return new Node(key); 

        if (key < node.key) 
            node.left = insert(node.left, key); 
        else if (key > node.key) 
            node.right = insert(node.right, key); 
        else // Equal keys are not allowed in BST 
            return node; 

        // Update height of this ancestor node 
        node.height = 1 + Math.max(height(node.left), 
                                   height(node.right)); 

        // Get the balance factor of this ancestor node 
        int balance = getBalance(node); 

        // If this node becomes unbalanced,
        // then there are 4 cases 

        // Left Left Case 
        if (balance > 1 && key < node.left.key) 
            return rightRotate(node); 

        // Right Right Case 
        if (balance < -1 && key > node.right.key) 
            return leftRotate(node); 

        // Left Right Case 
        if (balance > 1 && key > node.left.key) { 
            node.left = leftRotate(node.left); 
            return rightRotate(node); 
        } 

        // Right Left Case 
        if (balance < -1 && key < node.right.key) { 
            node.right = rightRotate(node.right); 
            return leftRotate(node); 
        } 

        // Return the (unchanged) node pointer 
        return node; 
    }
```

## Deletion

1. Perform the normal BST deletion. 
2. The current node must be one of the ancestors of the deleted node. Update the height of the current node. 
3. Get the balance factor (left subtree height – right subtree height) of the current node. 
4. If balance factor is greater than 1, then the current node is unbalanced and we are either in Left Left case or Left Right case. To check whether it is Left Left case or Left Right case, get the balance factor of left subtree. If balance factor of the left subtree is greater than or equal to 0, then it is Left Left case, else Left Right case. 
5. If balance factor is less than -1, then the current node is unbalanced and we are either in Right Right case or Right Left case. To check whether it is Right Right case or Right Left case, get the balance factor of right subtree. If the balance factor of the right subtree is smaller than or equal to 0, then it is Right Right case, else Right Left case.

```java
static Node deleteNode(Node root, int key) {
        // STEP 1: PERFORM STANDARD BST DELETE
        if (root == null)
            return root;

        // If the key to be deleted is smaller 
        // than the root's key, then it lies in 
        // left subtree
        if (key < root.key)
            root.left = deleteNode(root.left, key);

        // If the key to be deleted is greater 
        // than the root's key, then it lies in 
        // right subtree
        else if (key > root.key)
            root.right = deleteNode(root.right, key);

        // if key is same as root's key, then 
        // this is the node to be deleted
        else {
            // node with only one child or no child
            if ((root.left == null) || 
                (root.right == null)) {
                Node temp = root.left != null ? 
                            root.left : root.right;

                // No child case
                if (temp == null) {
                    temp = root;
                    root = null;
                } else // One child case
                    root = temp; // Copy the contents of 
                                 // the non-empty child
            } else {
                // node with two children: Get the 
                // inorder successor (smallest in 
                // the right subtree)
                Node temp = minValueNode(root.right);

                // Copy the inorder successor's 
                // data to this node
                root.key = temp.key;

                // Delete the inorder successor
                root.right = deleteNode(root.right, temp.key);
            }
        }

        // If the tree had only one node then return
        if (root == null)
            return root;

        // STEP 2: UPDATE HEIGHT OF THE CURRENT NODE
        root.height = Math.max(height(root.left), 
                               height(root.right)) + 1;

        // STEP 3: GET THE BALANCE FACTOR OF THIS 
        // NODE (to check whether this node 
        // became unbalanced)
        int balance = getBalance(root);

        // If this node becomes unbalanced, then 
        // there are 4 cases

        // Left Left Case
        if (balance > 1 && getBalance(root.left) >= 0)
            return rightRotate(root);

        // Left Right Case
        if (balance > 1 && getBalance(root.left) < 0) {
            root.left = leftRotate(root.left);
            return rightRotate(root);
        }

        // Right Right Case
        if (balance < -1 && getBalance(root.right) <= 0)
            return leftRotate(root);

        // Right Left Case
        if (balance < -1 && getBalance(root.right) > 0) {
            root.right = rightRotate(root.right);
            return leftRotate(root);
        }

        return root;
    }
```