# Collections in Java

## Collection Interface
The Collection<T> interface allows you to write code that applies to all Java collections so that you do not have to rewrite the code for each specific collection type. List is one of the collections that can help in implementing an ArrayList class as below:

Driver.java
```java	
  package com.cmu;

	import java.util.ArrayList;
	import java.util.List;

	public class Driver 
	{
		public static void main(String[] args) 
		{
			List<String> fruits = new ArrayList<>();
			fruits.add("Apple");
			fruits.add("Banana");
			fruits.add("Grapes");
			fruits.add("Cherry");
			
			// Adds an item at a specific index
			fruits.add(1, "Melon");
			
			System.out.println(fruits);
			
			// Gets an item at a specific index
			System.out.println(fruits.get(2));
			
			// Replaces an item
			fruits.set(1, "Water Melon");
			
			System.out.println(fruits);
			
			// Removes an item at a specific index
			fruits.remove(2);
			System.out.println(fruits);
			
			// Returns the size of the list 
			System.out.println("Size: " + fruits.size());
			
			// Returns true if an item is present in the list
			System.out.println("Contains: " + fruits.contains("Apple"));
		}

	}
```
## Lists as parameters to a function
Lists can be passed to a function

Driver.java
```java	
	package com.cmu;

	import java.util.ArrayList;
	import java.util.List;

	public class Driver 
	{
		public static void display(List<String> list)
		{
			System.out.println(list);
		}
		public static void main(String[] args) 
		{
			List<String> fruits = new ArrayList<>();
			fruits.add("Apple");
			fruits.add("Banana");
			fruits.add("Grapes");
			fruits.add("Cherry");
			
			display(fruits);
		}

	}
```
## Sorting an ArrayList
We can sort an ArrayList as well

Driver.java
```java	
	package com.cmu;

	import java.util.ArrayList;
	import java.util.Collections;
	import java.util.List;

	public class Driver 
	{
		public static void sort(ArrayList<Integer> list)
		{
			Collections.sort(list);
		}
		public static void main(String[] args) 
		{
			ArrayList<Integer> numbers = new ArrayList<>();
			numbers.add(2);
			numbers.add(1);
			numbers.add(3);
			numbers.add(5);
			numbers.add(4);
			
			System.out.println("Original List: " + numbers);
			
			sort(numbers);
			
			System.out.println("Modified List: " + numbers);
			
		}

	}
```
## Using Comparator with ArrayList
We can use a comparator to sort this ArrayList in descending order

Driver.java
```java	
	package com.cmu;

	import java.util.ArrayList;
	import java.util.Collections;
	import java.util.Comparator;
	import java.util.List;

	public class Driver 
	{
		public static void sort(ArrayList<Integer> list)
		{
			Collections.sort(list, new Comparator<Integer>() {
				@Override
				public int compare(Integer o1, Integer o2) {
					return o2.compareTo(o1);
				}
			});
		}
		public static void main(String[] args) 
		{
			ArrayList<Integer> numbers = new ArrayList<>();
			numbers.add(2);
			numbers.add(1);
			numbers.add(3);
			numbers.add(5);
			numbers.add(4);
			
			System.out.println("Original List: " + numbers);
			
			sort(numbers);
			
			System.out.println("Modified List: " + numbers);
			
		}

	}
```
## Linked Lists
LinkedList is a handy data structure that can be used when frequent insertion and removal are required:

Driver.java
```java	
	package com.cmu;

	import java.util.LinkedList;

	class Student
	{
		String name;
		int age;
		
		Student(String name, int age)
		{
			this.name = name;
			this.age = age;
		}
		
		@Override
		public String toString() {
			return "(" + name + ", " + age + ")";
		}
	}

	public class Driver 
	{
		
		public static void main(String[] args) 
		{
			LinkedList<Student> students = new LinkedList<>();
			students.add(new Student("Steve", 22));
			students.add(new Student("John", 23));
			students.add(new Student("Lizzy", 21));
			students.add(new Student("Elon", 20));
			students.add(new Student("Angela", 24));	
			
			System.out.println(students);
		}

	}
```
## Linked Lists as parameter to a function
Just like ArrayList, we can pass LinkedList to function as parameters as well

Driver.java
```java	
	package com.cmu;

	import java.util.LinkedList;

	class Student
	{
		String name;
		int age;
		
		Student(String name, int age)
		{
			this.name = name;
			this.age = age;
		}
		
		@Override
		public String toString() {
			return "(" + name + ", " + age + ")";
		}
	}

	public class Driver 
	{
		
		public static Student youngestStudent(LinkedList<Student> students)
		{
			Student youngest = students.get(0);
			for (Student student: students)
			{
				if (student.age < youngest.age)
				{
					youngest = student;
				}
			}
			return youngest;
		}
		
		public static void main(String[] args) 
		{
			LinkedList<Student> students = new LinkedList<>();
			students.add(new Student("Steve", 22));
			students.add(new Student("John", 23));
			students.add(new Student("Lizzy", 21));
			students.add(new Student("Elon", 20));
			students.add(new Student("Angela", 24));	
			
			System.out.println(students);
			
			System.out.println("Youngest Student: " + youngestStudent(students));
		}

	}
```
## Sorting a Linked List
Sort works for Linked List as well:

Driver.java
```java	
	package com.cmu;

	import java.util.Collections;
	import java.util.Comparator;
	import java.util.LinkedList;

	class Student
	{
		String name;
		int age;
		
		Student(String name, int age)
		{
			this.name = name;
			this.age = age;
		}
		
		@Override
		public String toString() {
			return "(" + name + ", " + age + ")";
		}
	}

	public class Driver 
	{
		
		public static Student youngestStudent(LinkedList<Student> students)
		{
			Student youngest = students.get(0);
			for (Student student: students)
			{
				if (student.age < youngest.age)
				{
					youngest = student;
				}
			}
			return youngest;
		}
		
		public static void sortStudents(LinkedList<Student> students)
		{
			Collections.sort(students, new Comparator<Student>() {
				public int compare(Student s1, Student s2) {
					return Integer.compare(s1.age, s2.age);
					
				};
			});
		}
		
		public static void main(String[] args) 
		{
			LinkedList<Student> students = new LinkedList<>();
			students.add(new Student("Steve", 22));
			students.add(new Student("John", 23));
			students.add(new Student("Lizzy", 21));
			students.add(new Student("Elon", 20));
			students.add(new Student("Angela", 24));	
			
			System.out.println(students);
			
			System.out.println("Youngest Student: " + youngestStudent(students));
			
			sortStudents(students);
			System.out.println(students);
		}

	}
```
