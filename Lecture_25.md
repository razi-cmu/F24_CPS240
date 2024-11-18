# Java Generic I

## Java Generic
Generics enable you to write code that works with any type while ensuring type safety.

Driver.java
```java

	package com.cmu;

	class X
	{
		private int x;

		X(int x)
		{
			this.x = x;
		}
		int getX()
		{
			return this.x;
		}
	}

	class Y
	{
		private int y;

		Y(int y)
		{
			this.y = y;
		}
		int getY()
		{
			return this.y;
		}
	}


	public class Driver 
	{
		public static void main(String[] args) 
		{
			X obj1 = new X(5);
			Y obj2 = new Y(6);
			
			int result = obj1.getX() + obj2.getY();
			
			System.out.println("Result: " + result);
			
		}

	}

```

The above program would work fine for integers. However, if we try to calculate the sum using double as below, we get an error:
```java
	public class Driver 
	{
		public static void main(String[] args) 
		{
			X obj1 = new X(5.5);
			Y obj2 = new Y(6.2);
			
			int result = obj1.getX() + obj2.getY();
			
			System.out.println("Result: " + result);
			
		}

	}

```

In a traditional program, we have to create separate X and Y classes to hold double or at least a separate data member which is double.

This program can be solved using Java Generic.

```java

	package com.cmu;

	class X<T>
	{
		private T x;
		
		X(T x)
		{
			this.x = x;
		}
		T getX()
		{
			return this.x;
		}
	}

	class Y<T>
	{
		private T y;
		
		Y(T y)
		{
			this.y = y;
		}
		T getY()
		{
			return this.y;
		}
	}


	public class Driver 
	{
		public static void main(String[] args) 
		{
			X<Integer> obj1 = new X<>(5);
			Y<Integer> obj2 = new Y<>(6);
			
			int result = obj1.getX() + obj2.getY();
			
			System.out.println("Result: " + result);
			
		}

	}


```

If we want to change the data type to double, we simply change the type to Double as below:

```java

	package com.cmu;

	class X<T>
	{
		private T x;
		
		X(T x)
		{
			this.x = x;
		}
		T getX()
		{
			return this.x;
		}
	}

	class Y<T>
	{
		private T y;
		
		Y(T y)
		{
			this.y = y;
		}
		T getY()
		{
			return this.y;
		}
	}


	public class Driver 
	{
		public static void main(String[] args) 
		{
			X<Double> obj1 = new X<>(5.6);
			Y<Double> obj2 = new Y<>(6.2);
			
			double result = obj1.getX() + obj2.getY();
			
			System.out.println("Result: " + result);
			
		}

	}


```

The above code would even work for String:

```java

	public class Driver 
	{
		public static void main(String[] args) 
		{
			X<String> obj1 = new X<>("Hello");
			Y<String> obj2 = new Y<>("World");
			
			String result = obj1.getX() + obj2.getY();
			
			System.out.println("Result: " + result);
			
		}

	}

```

## Creating an ArrayList

Let's create an ArrayList from scratch. To start with, let's create an ArrayList of int:

```java

	package com.cmu;

	class MyArrayList
	{
		int[] myArray;
		int size;
		
		MyArrayList(int capacity)
		{
			this.size = 0;
			this.myArray = new int[capacity];
		}
		public void add(int element)
		{
			if (this.size < myArray.length)
			{
				myArray[size++] = element;
			}
			else
			{
				System.out.println("Cannot add element. Array is full");
			}
		}
		public int get(int index)
		{
			if (index >= 0 && index < size)
			{
				return myArray[index];
			}
			else
			{
				throw new IndexOutOfBoundsException("Index " + index +  " is out of bound");
			}
		}
		public int getSize()
		{
			return this.size;
		}
		
		public void print()
		{
			for (int i=0; i<this.size; i++)
			{
				System.out.print(myArray[i] + " ");
			}
		}
	}


	public class Driver 
	{
		public static void main(String[] args) 
		{
			MyArrayList list = new MyArrayList(5);
			list.add(2);
			list.add(4);
			list.add(6);
			list.add(8);
			list.add(10);
			
			list.print();
			System.out.println("\nElement at index 2: " + list.get(2));
			System.out.println("Size of the list: " + list.getSize());
			
		}

	}


```

Trying to add a double value to this ArrayList would result in errors. Below is the code that would produce an error:

```java

	public static void main(String[] args) 
	{
		MyArrayList list = new MyArrayList(5);
		list.add(2.1);
		list.add(4.1);
		list.add(6.1);
		list.add(8.1);
		list.add(10.1);
		
		list.print();
		System.out.println("\nElement at index 2: " + list.get(2));
		System.out.println("Size of the list: " + list.getSize());
		
	}


```

The above issue can be resolved using Java Generic.

```java

	package com.cmu;

	class MyArrayList<T>
	{
		T[] myArray;
		int size;
		
		MyArrayList(int capacity)
		{
			this.size = 0;
			this.myArray = (T[])new Object[capacity]; // This is to ensure type safety
		}
		public void add(T element)
		{
			if (this.size < myArray.length)
			{
				myArray[size++] = element;
			}
			else
			{
				System.out.println("Cannot add element. Array is full");
			}
		}
		public T get(int index)
		{
			if (index >= 0 && index < size)
			{
				return myArray[index];
			}
			else
			{
				throw new IndexOutOfBoundsException("Index " + index +  " is out of bound");
			}
		}
		public int getSize()
		{
			return this.size;
		}
		
		public void print()
		{
			for (int i=0; i<this.size; i++)
			{
				System.out.print(myArray[i] + " ");
			}
		}
	}


	public class Driver 
	{
		public static void main(String[] args) 
		{
			MyArrayList<Double> list = new MyArrayList<>(5);
			list.add(2.1);
			list.add(4.1);
			list.add(6.1);
			list.add(8.1);
			list.add(10.1);
			
			list.print();
			System.out.println("\nElement at index 2: " + list.get(2));
			System.out.println("Size of the list: " + list.getSize());
			
		}

	}


```

The above class should work for String as below:

```java

	public static void main(String[] args) 
	{
		MyArrayList<String> list = new MyArrayList<>(5);
		list.add("Apple");
		list.add("Banana");
		list.add("Orange");
		list.add("Grape");
		list.add("Melon");
		
		list.print();
		System.out.println("\nElement at index 2: " + list.get(2));
		System.out.println("Size of the list: " + list.getSize());
		
	}


```

Specific operations can be performed based on the type of generic. 

For example, if the generic is a String, we want to join the strings, however, if the generic type is integer, we want to calculate the sum:

```java

	package com.cmu;

	class MyArrayList<T>
	{
		T[] myArray;
		int size;
		
		MyArrayList(int capacity)
		{
			this.size = 0;
			this.myArray = (T[])new Object[capacity];
		}
		public void add(T element)
		{
			if (this.size < myArray.length)
			{
				myArray[size++] = element;
			}
			else
			{
				System.out.println("Cannot add element. Array is full");
			}
		}
		public T get(int index)
		{
			if (index >= 0 && index < size)
			{
				return myArray[index];
			}
			else
			{
				throw new IndexOutOfBoundsException("Index " + index +  " is out of bound");
			}
		}
		public int getSize()
		{
			return this.size;
		}
		
		public void print()
		{
			for (int i=0; i<this.size; i++)
			{
				System.out.print(myArray[i] + " ");
			}
		}
		public void sum()
		{
			if (myArray[0] instanceof String)
			{
				StringBuilder sb = new StringBuilder();
				for (int i = 0; i < size; i++) {
					sb.append(myArray[i]);
					if (i < size - 1) {
						sb.append(", ");
					}
				}
				System.out.println("Result (String join): " + sb.toString());
			}
			
			else if (myArray[0] instanceof Integer)
			{
				int sum = 0;
				for (int i=0; i<size; i++)
				{
					sum += (Integer)myArray[i];
				}
				System.out.println("Result: " + sum);
			}
		}
	}


	public class Driver 
	{
		public static void main(String[] args) 
		{
			MyArrayList<String> list = new MyArrayList<>(5);
			list.add("Apple");
			list.add("Banana");
			list.add("Orange");
			list.add("Grape");
			list.add("Melon");
			
			list.print();
			System.out.println("\nElement at index 2: " + list.get(2));
			System.out.println("Size of the list: " + list.getSize());
			
			list.sum();
			
		}

	}


```

If we change the type to integer, the above class should give us the sum of all the integers:

```java

	public static void main(String[] args) 
	{
		MyArrayList<Integer> list = new MyArrayList<>(5);
		list.add(1);
		list.add(2);
		list.add(3);
		list.add(4);
		list.add(5);
		
		list.print();
		System.out.println("\nElement at index 2: " + list.get(2));
		System.out.println("Size of the list: " + list.getSize());
		
		list.sum();
		
	}

```