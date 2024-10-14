# Hashing - HashMap

Hashmaps are used to improve efficiency while searching

HashMap.java
```java
package HashMaps;

class Node
{
    int key;
    int value;
    Node next;

    Node(int key, int value)
    {
        this.key = key;
        this.value = value;
    }
    int getValue()
    {
        return this.value;
    }
    int getKey()
    {
        return this.key;
    }
    void setValue(int value)
    {
        this.value = value;
    }
}

public class HashMap {

    Node table[];
    int size;

    HashMap(int size)
    {
        this.size = size;
        table = new Node[size];
    }

    void put(int key, int value)
    {
        int hash = key % size;

        Node node = table[hash];

        if (node == null)
        {
            table[hash] = new Node(key, value);
        }
        else
        {
            while (node.next != null)
            {
                // update the value of the key
                if (node.getKey() == key)
                {
                    node.setValue(value);
                    return;
                }
                node = node.next;
            }

            if (node.getKey() == key)
            {
                node.setValue(value);
                return;
            }
            node.next = new Node(key, value);
        }
    }
    
    int get(int key)
    {
        int hash = key % size;
        Node node = table[hash];

        if (node == null)
        {
            return -1;
        }

        while (node != null)
        {
            if (node.getKey() == key)
            {
                return node.getValue();
            }
            node = node.next;
        }
        return -1;
    }
    
}
```

Driver.java
```java
package HashMaps;

public class Driver {
    public static void main(String[] args) {
        HashMap map = new HashMap(10);
        map.put(1, 25);
        map.put(2, 38);
        map.put(3, 46);
        map.put(4, 59);
        map.put(5, 94);
        map.put(1, 98);
        int value = 381;
        int key = 6;

        
        if ((value = map.get(key)) == -1)
        {
            System.out.println("No value found at that key");
        }
        else
        {
            System.out.printf("Value at %d: %d", key, value);
        }
    }
}
```
