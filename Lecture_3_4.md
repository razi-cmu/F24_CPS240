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
