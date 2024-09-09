# Classes and Objects in Java

## Classes and Objects
Every object is an instance of a class, which serves as the type of the object and as a blueprint.

	Student.java
 
```java
	public class Student 
	{
		private String name;
		private int age;
		
		Student()
		{
			name = "";
			age = 0;
		}
		
		Student(String n, int a)
		{
			name = n;
			age = a;
		}
		
		public String getName()
		{
			return name;
		}
		public int getAge()
		{
			return age;
		}
		public void setName(String n)
		{
			name = n;
		}
		public void setAge(int a)
		{
			age = a;
		}
		
		public void display()
		{
			System.out.println("Name: " + name + ", Age: " + age);
		}

	}
	```

	Driver.java

	```java
	public class Driver {
		
		public static void main(String[] args) 
		{
			Student student = new Student();
			student.setName("John");
			student.setAge(22);
			student.display();
		}
		
	}
```

## Wrapper Classes
Wrapper classes are very handy as they provide excellent ways of dealing with regular data types. Let's consider an example below:

	Driver.java
	
	import java.util.ArrayList;
	import java.util.List;
	import java.util.Scanner;

	public class Driver {
		
		public static void main(String[] args) 
		{
			
			List<Student> students = new ArrayList<>();
			Scanner scanner = new Scanner(System.in);
			
			for (int i=0; i<5; i++)
			{
				System.out.print("Enter student's name: ");
				String name = scanner.nextLine();

				System.out.print("Enter student's age: ");
				int age = scanner.nextInt();
				
				Student student = new Student(name, age);
				
				students.add(student);
			}
			
			for (Student student: students)
			{
				student.display();
			}
		   
		}
	}
	
	The above program would give an issue as next characters in the line are still in the buffer and hence nextInt wont work as expected. We can update it as below:
	
	Student.java
	
	public class Student 
	{
		private String name;
		private Integer age;
		
		Student()
		{
			name = "";
			age = 0;
		}
		
		Student(String n, Integer a)
		{
			name = n;
			age = a;
		}
		
		public String getName()
		{
			return name;
		}
		public Integer getAge()
		{
			return age;
		}
		public void setName(String n)
		{
			name = n;
		}
		public void setAge(Integer a)
		{
			age = a;
		}
		
		public void display()
		{
			System.out.println("Name: " + name + ", Age: " + age);
		}

	}

	Driver.java
	
	import java.util.ArrayList;
	import java.util.List;
	import java.util.Scanner;

	public class Driver {
		
		public static void main(String[] args) 
		{
			
			List<Student> students = new ArrayList<>();
			Scanner scanner = new Scanner(System.in);
			
			for (int i=0; i<5; i++)
			{
				System.out.print("Enter student's name: ");
				String name = scanner.nextLine();

				System.out.print("Enter student's age: ");
				int age = Integer.parseInt(scanner.nextLine());
				
				Student student = new Student(name, age);
				
				students.add(student);
			}
			
			for (Student student: students)
			{
				student.display();
			}
		   
		}
		
	}
	
Another advantage of using Wrapper classes is availability of several built-in functions.

	Student.java
	
	public class Student 
	{
		private String name;
		private Integer age;
		
		Student()
		{
			name = "";
			age = 0;
		}
		
		Student(String n, Integer a)
		{
			name = n;
			age = a;
		}
		
		public String getName()
		{
			return name;
		}
		public Integer getAge()
		{
			return age;
		}
		public void setName(String n)
		{
			name = n;
		}
		public void setAge(Integer a)
		{
			age = a;
		}
		
		public void display()
		{
			System.out.println("Name: " + name + ", Age: " + age);
		}

	}

	Driver.java
	
	import java.util.ArrayList;
	import java.util.List;
	import java.util.Scanner;

	public class Driver {
		
		public static Student getYoungest(List<Student> students)
		{
			Student youngest = students.get(0);
			for (Student student: students)
			{
				if (student.getAge().compareTo(youngest.getAge()) < 0)
				{
					youngest = student;
				}
			}
			
			return youngest;
		}
		
		public static void main(String[] args) 
		{
			
			List<Student> students = new ArrayList<>();
			Scanner scanner = new Scanner(System.in);
			
			for (int i=0; i<5; i++)
			{
				System.out.print("Enter student's name: ");
				String name = scanner.nextLine();

				System.out.print("Enter student's age: ");
				int age = Integer.parseInt(scanner.nextLine());
				
				Student student = new Student(name, age);
				
				students.add(student);
			}
			
			System.out.println("\nList of Students...");
			for (Student student: students)
			{
				student.display();
			}
			
			System.out.println("\nYoungest Student:");
			
			getYoungest(students).display();
			
			scanner.close();
		   
		}
		
	}


Within the body of a method in Java, the keyword this is automatically defined as a reference to the instance upon which the method was invoked

	Student.java
	
	public class Student 
	{
		private String name;
		private Integer age;
		
		Student()
		{
			this.name = "";
			this.age = 0;
		}
		
		Student(String name, Integer age)
		{
			this.name = name;
			this.age = age;
		}
		
		public String getName()
		{
			return this.name;
		}
		public Integer getAge()
		{
			return this.age;
		}
		public void setName(String name)
		{
			this.name = name;
		}
		public void setAge(Integer age)
		{
			this.age = age;
		}
		
		public void display()
		{
			System.out.println("Name: " + this.name + ", Age: " + this.age);
		}

	}

	The Driver class remains the same.
	
	
Packages are a way to organize Java classes and interfaces. They provide a namespace to avoid naming conflicts.

	Graduate.java
	
	package com.cmu.Graduate;

	public class Student 
	{
		private String name;
		private int age;
		private String thesis;
		
		public Student(String name, int age, String thesis)
		{
			this.name = name;
			this.age = age;
			this.thesis = thesis;
		}
		
		public String toString()
		{
			return this.name + ", " + this.age + ", " + this.thesis;
		}

	}
	
	Undergraduate.java
	
	package com.cmu.Undergraduate;

	public class Student 
	{
		private String name;
		private int age;
		
		public Student(String name, int age)
		{
			this.name = name;
			this.age = age;
		}
		
		public String toString()
		{
			return this.name + ", " + this.age;
		}

	}

	Main.java
	
	package com.cmu.Driver;

	import com.cmu.Graduate.Student;

	public class Main {
		
		public static void main(String[] args) 
		{
			Student graduate = new Student("Steve", 26, "Internet of Things");
			com.cmu.Undergraduate.Student undergraduate = new com.cmu.Undergraduate.Student("John", 22);
				
			System.out.println(graduate);
			System.out.println(undergraduate);
			
			
		}

	}


Inner Classes is valuable technique when implementing data structures, as an instance of a nested use can be used to represent a small portion of a larger data structure, or an auxiliary class that helps navigate a primary data structure.

	Student.java
	
	package com.cmu;

	import java.util.Arrays;

	public class Student 
	{
		String name;
		int age;
		
		Student(String name, int age)
		{
			this.name = name;
			this.age = age;
		}

		public String getName() {
			return name;
		}

		public void setName(String name) {
			this.name = name;
		}

		public int getAge() {
			return age;
		}

		public void setAge(int age) {
			this.age = age;
		}
		
		void display()
		{
			System.out.println("Name: " + name + ", Age: " + age);
		}
		
		class StudentDetails
		{
			String getFirstName()
			{
				String firstName[];
				
				firstName = name.split(" ", 2);

				return firstName[0];
			}
		}

	}
	
	Driver.java
	
	package com.cmu;

	public class Driver 
	{
		public static void main(String[] args) 
		{
			Student student = new Student("Steve Allen Jobs", 55);
			student.display();
			
			Student.StudentDetails details = student.new StudentDetails();
			System.out.println(details.getFirstName());
			
		}

	}


A final is pretty handy keyword in java. It helps in avoiding accidental change of values for a variable

	Student.java
	
	public class Student {
		String name;
		int age;
		final String student_type = "Undergraduate";

		void setType()
		{
			this.student_type = "Graduate";
		}
	}
