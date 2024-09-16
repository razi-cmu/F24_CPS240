# Exception Handling

## Exceptions
Exceptions are runtime errors. Exception handling enables a program to deal with runtime errors and continue its normal execution.

Driver.java
```java	
	import java.util.Scanner;

	public class Driver 
	{
		public static void main(String[] args) 
		{
			Scanner scanner = new Scanner(System.in);
			
			System.out.print("Enter number 1: ");
			int number1 = scanner.nextInt();
			System.out.print("Enter number 2: ");
			int number2 = scanner.nextInt();
			
			int result = number1/number2;
			
			System.out.println("Result: "+ result);
			
		}

	}
```
The above program would run just fine except when we input number2 as 0. Since, we cannot divide by 0, the program crashes.
	
One of the ways of handling this issue is to use conditional statements like if else. In order to make it more readable, let's create a separate function:
	
Driver.java
```java	
	import java.util.Scanner;

	public class Driver 
	{
		
		public static int quotient(int number1, int number2)
		{
			if (number2 == 0)
			{
				System.out.println("Cannot divide by 0.");
				System.exit(1);
			}
			int result = number1/number2;
			
			return result;
		}
		public static void main(String[] args) 
		{
			Scanner scanner = new Scanner(System.in);
			
			System.out.print("Enter number 1: ");
			int number1 = scanner.nextInt();
			System.out.print("Enter number 2: ");
			int number2 = scanner.nextInt();
			
			int result = quotient(number1, number2);
			
			System.out.println("Result: "+ result);
			
		}

	}
```
The problem with the above approach is that the method 'quotient' would terminate the program, which is not ideal. So if there is any code after the 'quotient' method calls return to main method, that code would not execute:
	
Driver.java
```java	
	import java.util.Scanner;

	public class Driver 
	{
		
		public static int quotient(int number1, int number2)
		{
			if (number2 == 0)
			{
				System.out.println("Cannot divide by 0.");
				System.exit(1);
			}
			int result = number1/number2;
			
			return result;
		}
		public static void main(String[] args) 
		{
			Scanner scanner = new Scanner(System.in);
			
			System.out.print("Enter number 1: ");
			int number1 = scanner.nextInt();
			System.out.print("Enter number 2: ");
			int number2 = scanner.nextInt();
			
			int result = quotient(number1, number2);
			
			// This code would not run
			System.out.println("Result: "+ result);
			
			// This code would not run
			System.out.println("Rest of the code");
			
		}

	}
```
## Throwing an Exception
Try Catch can be used to throw and then catch an exception that might occur in a vulernable code:

Driver.java
```java	
	package com.cmu;

	import java.util.Scanner;

	public class Driver 
	{
		
		public static int quotient(int number1, int number2)
		{
			if (number2 == 0)
			{
				throw new ArithmeticException("Cannot divide by zero");
			}
			int result = number1/number2;
			
			return result;
		}
		public static void main(String[] args) 
		{
			Scanner scanner = new Scanner(System.in);
			
			System.out.print("Enter number 1: ");
			int number1 = scanner.nextInt();
			System.out.print("Enter number 2: ");
			int number2 = scanner.nextInt();
			
			try
			{
				int result = quotient(number1, number2);
				
				System.out.println("Result: "+ result);
			}
			catch(ArithmeticException ex)
			{
				System.out.println(ex.getMessage());
			}

			System.out.println("Rest of the code");
			
		}

	}
```
## Exception Types
Let's try some other types of exceptions as well. The below program will work fine as long as we are entering the integers. However, the program crashes when a double is entered:

Driver.java
```java	
	import java.util.Scanner;

	public class Driver 
	{
		
		public static void main(String[] args) 
		{
			Scanner scanner = new Scanner(System.in);
			
			System.out.print("Enter a number: ");
			int number = scanner.nextInt();
			
			System.out.println("Number entered was " + number);
			
		}

	}
```
We can fix the above program using try catch and putting a loop so that program keeps asking the user to enter number till user inputs the correct number

Driver.java
```java	
	import java.util.InputMismatchException;
	import java.util.Scanner;

	public class Driver 
	{
		
		public static void main(String[] args) 
		{
			Scanner scanner = new Scanner(System.in);
			boolean input = true;
			
			do
			{
				try
				{
					System.out.print("Enter a number: ");
					int number = scanner.nextInt();
					
					System.out.println("Number entered was " + number);
					
					input = false;
				}
				catch(InputMismatchException ex)
				{
					System.out.println("Incorrect input. Please enter integers only: ");
					scanner.nextLine();
				}
				
			} while (input);
			
		}

	}
```
## The `throws` Keyword
Methods can throw exceptions without being explicitly declared using a keyword 'throws':

Driver.java
```java	
	import java.util.InputMismatchException;
	import java.util.Scanner;

	public class Driver 
	{
		public static void display(int[] numbers) throws ArrayIndexOutOfBoundsException
		{
			for (int i=0; i<numbers.length; i++)
			{
				System.out.print(numbers[i] + "\t");
			}
			
			System.out.println(numbers[5]);
		}
		
		public static void main(String[] args) 
		{
			int[] numbers = new int[] {1, 2, 3, 4, 5};
			
			try
			{
				display(numbers);
			}
			catch(ArrayIndexOutOfBoundsException ex)
			{
				System.out.println("\nArray Index out of bound");
			}

		}

	}
```
## Multiple catch blocks
A try block can have multiple catch blocks

Driver.java
```java
	import java.util.InputMismatchException;
	import java.util.Scanner;

	public class Driver 
	{
		
		public static void main(String[] args) 
		{
			
			String myException = "divide";
			
			try
			{
				if (myException.equals("Null"))
				{
					throw new NullPointerException();
				}
				else if (myException.equals("array"))
				{
					throw new ArrayIndexOutOfBoundsException();
				}
				else if (myException.equals("divide"))
				{
					throw new ArithmeticException();
				}
			}
			catch(NullPointerException ex)
			{
				System.out.println("Null Pointer Exception");
			}
			catch(ArrayIndexOutOfBoundsException ex)
			{
				System.out.println("Array Index out of bound");
			}
			catch(Exception ex)
			{
				System.out.println("A Generic Exception caught");
			}
			
		}

	}
```
## Order of catch blocks
The order to placement of these catch blocks is extremely important. If a catch block is placed in a way that it cannot never execute, we get an error:

Driver.java
```java
	import java.util.InputMismatchException;
	import java.util.Scanner;

	public class Driver 
	{
		
		public static void main(String[] args) 
		{
			
			String myException = "divide";
			
			try
			{
				if (myException.equals("Null"))
				{
					throw new NullPointerException();
				}
				else if (myException.equals("array"))
				{
					throw new ArrayIndexOutOfBoundsException();
				}
				else if (myException.equals("divide"))
				{
					throw new ArithmeticException();
				}
			}
			catch(Exception ex)
			{
				System.out.println("A Generic Exception caught");
			}
			catch(NullPointerException ex)
			{
				System.out.println("Null Pointer Exception");
			}
			catch(ArrayIndexOutOfBoundsException ex)
			{
				System.out.println("Array Index out of bound");
			}
		}
	}
```
The above code generates an error as Exception is the parent class and would end up catching all the exceptions which makes NullPointerException and ArrayIndexOutOfBoundsException unreachable.

 ## The `finally` Keyword
The finally keyword in Java is useful for ensuring that specific code runs regardless of whether an exception is thrown or not. 

Driver.java
```java	
	package com.cmu;

	import java.io.BufferedReader;
	import java.io.FileInputStream;
	import java.io.FileReader;
	import java.io.IOException;
	import java.util.InputMismatchException;
	import java.util.Scanner;

	public class Driver 
	{
		public static void readFile(String fileName)
		{
			BufferedReader reader = null;
			
			try
			{
				reader = new BufferedReader(new FileReader(fileName));
				
				String line;
				
				while ((line = reader.readLine()) != null)
				{
					System.out.println(line);
				}	
			}
			catch(IOException ex)
			{
				System.out.println(ex.getMessage());
			}
			finally
			{
				try 
				{
					if (reader != null)
					{
						reader.close();
					}
					
				} 
				catch (IOException e) 
				{
					e.printStackTrace();
				}
			}
		}
		
		public static void main(String[] args) 
		{
			readFile("sample1.txt");
		}

	}
```
The above program makes sure that reader is closed no matter an exception occurs or not.

