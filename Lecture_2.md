# I/O, Arrays, Complexities, Sorting and Searching

## Reading Files
Java provides an efficient way of reading from files using built-in classes
```java
	import java.io.BufferedReader;
	import java.io.FileNotFoundException;
	import java.io.FileReader;
	import java.io.IOException;

	public class Driver {

		public static void main(String[] args) 
		{
			FileReader fileReader;
			try 
			{
				fileReader = new FileReader("sample.txt");
				BufferedReader reader = new BufferedReader(fileReader);
				String line;
				
				while ((line = reader.readLine()) != null)
				{
					System.out.println(line);
				}
			} catch (IOException e) {
				System.out.println("An error occurred");
				e.printStackTrace();
			}
			
		}
	}
```

## Writing Files
Just like reading, Java provides built-in classes for writing to the files as well
```java
	import java.io.BufferedReader;
	import java.io.BufferedWriter;
	import java.io.FileNotFoundException;
	import java.io.FileReader;
	import java.io.FileWriter;
	import java.io.IOException;

	public class Driver {

		public static void main(String[] args) 
		{
			try 
			{
				FileWriter fileWriter = new FileWriter("sample.txt");
				BufferedWriter writer = new BufferedWriter(fileWriter);
				writer.write("Postal Code: 48859");
				System.out.println("Data written to the file");
				writer.close();
				fileWriter.close();
			} catch (IOException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
			
		}
	}
```
## Array
3. Array is a collection of elements of the same type.
```java
	public class Driver 
	{
		public static void main(String[] args) 
		{
			int[] numbers = new int[5];
			numbers[0] = 2;
			numbers[1] = 4;
			numbers[2] = 6;
			numbers[3] = 8;
			numbers[4] = 10;
			
			for (int i=0; i<numbers.length; i++)
			{
				System.out.println(numbers[i]);
			}		
		}
	}
```

Arrays can be used as data members of a class as well:

- Numbers.java
 
```java
	import java.util.Scanner;

	public class Numbers 
	{
		private int[] numbers;
		
		Numbers(int size)
		{
			numbers = new int[size];
		}
		
		public void insert_elements()
		{
			Scanner scanner = new Scanner(System.in);
			for (int i=0; i<numbers.length; i++)
			{
				System.out.printf("Enter elements at index %d: ", i);
				numbers[i] = scanner.nextInt();
			}
			
		}
		
		public void print_elements()
		{
			for (int i=0; i<numbers.length; i++)
			{
				System.out.println(numbers[i]);
			}
		}
		
		public boolean search_element(int element)
		{
			for (int number: numbers)
			{
				if (number == element)
				{
					return true;
				}
			}
			return false;
		}

	}
```
- Driver.java
```java
	public class Driver {

		public static void main(String[] args) 
		{
			Numbers num = new Numbers(5);
			num.insert_elements();
			num.print_elements();
			System.out.println(num.search_element(5)? "Found" : "Not Found");
		}
	}
```
## Selection Sort
5. We can sort collections (arrays) using Selection Sort:
```java
	public void selection_sort()
	{
		int size = numbers.length;
		
		for (int i=0; i<size; i++)
		{
			int smallest = i;
			
			for (int j = i + 1; j<size; j++)
			{
				if (numbers[smallest] > numbers[j])
				{
					smallest = j;
				}
			}
			
			int temp = numbers[smallest];
			numbers[smallest] = numbers[i];
			numbers[i] = temp;
		}
	}
```
## Binary Search
Binary Search provides an efficient way of search in a sorted array:
```java
	public boolean binary_search(int element)
	{
		int head = 0;
		int tail = numbers.length - 1;
		
		
		while (head <= tail)
		{
			int mid = (head + tail) / 2;
			if (element == numbers[mid])
			{
				return true;
			}
			else if (element < numbers[mid])
			{
				tail = mid - 1;
			}
			else
			{
				head = mid + 1;
			}
		}
		return false;
		
	}
```
