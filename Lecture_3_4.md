# Overview of Data Structures (Review CPS 181)

## Linked Lists
A Link List is a series of nodes connected together. We can implement LinkedList from scratch in Java.

`LinkedList.java`
```java
package LinkedList_Implementation;

class Node
{
    public int data;
    public Node next;

    public Node(int data)
    {
        this.data = data;
    }
}

public class LinkedList {

    Node head;

    LinkedList()
    {
        this.head = null;
    }

    public void insertElement(int number)
    {
        Node node = new Node(number);

        if (this.head == null)
        {
            this.head = node;
        }
        else
        {
            Node currentNode = this.head;
            while (currentNode.next != null)
            {
                currentNode = currentNode.next;
            }
            currentNode.next = node;
        }
    }
    public void print()
    {
        Node currentNode = this.head;

        while (currentNode != null)
        {
            System.out.println(currentNode.data);
            currentNode = currentNode.next;
        }
    }
    
}
```
`Driver.java`
```java
package LinkedList_Implementation;

public class Driver {
    public static void main(String[] args) {
        LinkedList list = new LinkedList();
        list.insertElement(2);
        list.insertElement(4);
        list.insertElement(6);
        list.insertElement(8);
        list.insertElement(10);

        list.print();
    }
}
```

### Linked List Search Operation
LinkedList can perform operations like search. Below function returns true if found else false

```java
public Boolean search(int number)
    {
        Boolean found = false;

        Node currentNode = this.head;

        while (currentNode != null)
        {
            if (currentNode.data == number)
            {
                found = true;
                break;
            }
            currentNode = currentNode.next;
        }

        return found;
    }
```
### Linked List Delete Operation
We can delete elements from the linkedlist as well. An important thing to note here is to connect the previous node to the next node of the deleted node to make sure that Linked List is connected.

`LinkedList.java`
```java
package LinkedList_Implementation;

class Node
{
    public int data;
    public Node next;

    public Node(int data)
    {
        this.data = data;
    }
}


public class LinkedList {

    Node head;

    LinkedList()
    {
        this.head = null;
    }

    public void insertElement(int number)
    {
        Node node = new Node(number);

        if (this.head == null)
        {
            this.head = node;
        }
        else
        {
            Node currentNode = this.head;
            while (currentNode.next != null)
            {
                currentNode = currentNode.next;
            }
            currentNode.next = node;
        }
    }
    public void print()
    {
        Node currentNode = this.head;

        if (this.head == null)
        {
            System.out.println("List is empty");
        }

        while (currentNode != null)
        {
            System.out.println(currentNode.data);
            currentNode = currentNode.next;
        }
    }

    public Boolean search(int number)
    {
        Boolean found = false;

        Node currentNode = this.head;

        while (currentNode != null)
        {
            if (currentNode.data == number)
            {
                found = true;
                break;
            }
            currentNode = currentNode.next;
        }

        return found;
    }

    public void delete(int number)
    {
        Node currentNode = this.head;
        Node previousNode = this.head;

        if (this.head == null)
        {
            System.out.println("List is empty");
        }

        if (head.data == number)
        {
            this.head = this.head.next;
        }

        while (currentNode != null)
        {
            if (currentNode.data != number)
            {
                previousNode = currentNode;
                currentNode = currentNode.next;
            }
            else
            {
                previousNode.next = currentNode.next;
                currentNode = null;
            }
        }
        
    }
    
}
```
`Driver.java`
```java
package LinkedList_Implementation;

public class Driver {
    public static void main(String[] args) {
        LinkedList list = new LinkedList();
        list.insertElement(2);
        list.insertElement(4);
        list.insertElement(6);
        list.insertElement(8);
        list.insertElement(10);

        System.out.println("Before deleting...");
        list.print();

        list.delete(2);
        list.delete(6);
        list.delete(8);
        list.delete(4);
        list.delete(10);
        System.out.println("After deleting...");
        list.print();
    }
}
```
## Binary Search Trees
Binary Search Trees can be implemented using recursive and iterative approach. Below is the iterative approach

`BinarySearchTree.java`
```java
class Node
{
    int value;
    Node left;
    Node right;

    Node(int value)
    {
        this.value = value;
    }
}

public class BinarySearchTree 
{
    Node root;

    public void insertNode(int value)
    {
        Node node = new Node(value);

        if (root == null)
        {
            root = node;
        }
        else
        {
            Node currentNode = root;
            Node parent;
            while (true)
            {
                parent = currentNode;
                if (value < currentNode.value)
                {
                    currentNode = currentNode.left;
                    if (currentNode == null)
                    {
                        parent.left = node;
                        return;
                    }
                }
                else
                {
                    currentNode = currentNode.right;
                    if (currentNode == null)
                    {
                        parent.right = node;
                        return;
                    }
                }
            }
        }

        // Time Complexity if O(n)
        // Space Complexity is O(n)
    }

    public void printNodes()
    {
        Stack<Node> stack = new Stack<>();
        Node currentNode = root;

        while (currentNode!=null || !stack.empty())
        {
            if (currentNode!=null)
            {
                stack.push(currentNode);
                currentNode = currentNode.left;
            }
            else
            {
                currentNode = stack.pop();
                System.out.println(currentNode.value);
                currentNode = currentNode.right;
            }
        }

        // Time Complexity if O(n)
        // Space Complexity is O(n)
    }

}
```
`Driver.java`

```java
package BST;

public class Driver {

    public static void main(String[] args) {
        BinarySearchTree tree = new BinarySearchTree();
        tree.insertNode(5);
        tree.insertNode(10);
        tree.insertNode(2);
        tree.insertNode(11);
        tree.insertNode(1);
        tree.insertNode(3);
        tree.insertNode(20);
        tree.insertNode(15);
        tree.insertNode(90);

        tree.printNodes();
    }
}
```
### Binary Search Tree Search Operation
Binary Search Trees are very efficient when it comes to searching as they'll only search half of the tree pretty much similar to binary search.
```java
    public Node search(int value)
    {
        Node currentNode = root;

        while (currentNode.value != value)
        {
            if (value < currentNode.value)
            {
                currentNode = currentNode.left;
            }
            else
            {
                currentNode = currentNode.right;
            }

            if (currentNode == null)
            {
                return null;
            }
        }
        return currentNode;

        // Time Complexity: O(logn)
        // Space Complexity: O(n)
    }
```
### Binary Search Tree Insertion using Recursion
Recursion can be used to simplify the code for insertion as below:
```java
    public void insertion(int value)
    {
        root = insertNode_recursion(root, value);
    }

    public Node insertNode_recursion(Node root, int value)
    {
        if (root == null)
        {
            root = new Node(value);
            return root;
        }
        else if (value < root.value)
        {
            root.left = insertNode_recursion(root.left, value);
        }
        else
        {
            root.right = insertNode_recursion(root.right, value);
        }
        return root;
    }
```
### Binary Search Tree Search using Recursion
Recursion can be used for Search as well
```java
    public Node search_recursion(Node root, int value)
    {
        if (root == null || root.value == value)
        {
            return root;
        }
        if (value < root.value)
        {
            return search_recursion(root.left, value);
        }
        else
        {
            return search_recursion(root.right, value);
        }
    }

    public void search_it(int value)
    {
        if (search_recursion(root, value) == null)
        {
            System.out.println("\nElement not found");
        }
        else
        {
            System.out.println("\nElement found");
        }
    }
```
