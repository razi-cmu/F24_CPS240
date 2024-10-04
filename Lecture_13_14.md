# Multithreading

## Single threaded Application
Single threaded environments work in sequence. Task 1 needs to complete before Task 2. Below is example where downloadFile needs to complete before print function can work:

Driver.java

```java
	package com.cmu;

	public class Driver 
	{
		public static void downloadFile()
		{
			System.out.println("Starting file download...");
			
			try 
			{
				Thread.sleep(5000);
			} 
			catch (InterruptedException e) 
			{
				e.printStackTrace();
			}
			
			System.out.println("File download completed.");
		}
		public static void print()
		{
			for (int i=0; i<100; i++)
			{
				System.out.printf("%d ", i);
			}
		}
		public static void main(String[] args) 
		{
			downloadFile();
			print();
		}

	}
```
## Multithreaded Application
The above program can be made more efficient if both functions can work in parallel. For this we have to create separate classes to run each function in their own threads
	
Driver.java

```java
	package com.cmu;

	class DownloadThread extends Thread
	{
		public void run()
		{
			downloadFile();
		}
		public void downloadFile()
		{
			System.out.println("Starting file download...");
			
			try 
			{
				Thread.sleep(5000);
			} 
			catch (InterruptedException e) 
			{
				e.printStackTrace();
			}
			
			System.out.println("File download completed.");
		}
	}

	class PrintThread extends Thread
	{
		public void run()
		{
			print();
		}
		
		public void print()
		{
			for (int i=0; i<100; i++)
			{
				System.out.printf("%d ", i);
			}
			System.out.println();
		}
	}

	public class Driver 
	{
		public static void main(String[] args) 
		{
			DownloadThread download = new DownloadThread();
			download.start();
			
			PrintThread print = new PrintThread();
			print.start();
		}

	}
```
### Runnable Interface
We can use Runnable Interface to clean the above code

Driver.java
```java	
	package com.cmu;

	public class Driver 
	{
		public static void downloadFile()
		{
			System.out.println("Starting file download...");
			
			try 
			{
				Thread.sleep(5000);
			} 
			catch (InterruptedException e) 
			{
				e.printStackTrace();
			}
			
			System.out.println("File download completed.");
		}
		public static void print()
		{
			for (int i=0; i<100; i++)
			{
				System.out.printf("%d ", i);
			}
			System.out.println();
		}
		public static void main(String[] args) 
		{
			Thread downloadThread = new Thread(new Runnable() {
				@Override
				public void run() {
					downloadFile();
				}
				
			});
			
			Thread printThread = new Thread(new Runnable() {
				@Override
				public void run() {
					print();
				}
				
			});
			
			downloadThread.start();
			printThread.start();
		}

	}
```
## Threads Communication
Threads can communicate with each other using variables. Let's make download thread communicate with print thread

Driver.java
```java
	package com.cmu;

	public class Driver 
	{
		private static int progress = 0;

		public static void downloadFile() {
			System.out.println("Starting file download...");

			for (int i = 0; i <= 100; i++) {
				try 
				{
					Thread.sleep(50);
					progress = i;
				} catch (InterruptedException e) {
					e.printStackTrace();
				}
			}
			
			System.out.println("\nFile download completed.");
		}

		public static void print() 
		{
			while (progress < 100) 
			{
				System.out.print("Progress: " + progress + "% \n");
				try 
				{
					Thread.sleep(100);
				} 
				catch (InterruptedException e) 
				{
					e.printStackTrace();
				}
			}
		   
		}

		public static void main(String[] args) {
			Thread downloadThread = new Thread(new Runnable() {
				@Override
				public void run() {
					downloadFile();
				}
				
			});
			
			Thread printThread = new Thread(new Runnable() {
				@Override
				public void run() {
					print();
				}
				
			});
			
			downloadThread.start();
			printThread.start();
		}
	}
```
### Lambda Functions for Threads	
We can simplify the above main method by using lambda function as well. This is easier to write and Java -8 and above support this way of writing threads but it is less readable, however much cleaner:
```java
public static void main(String[] args) 
  {
    	Thread downloadThread = new Thread(()->{
    		downloadFile();
    	});
		
		Thread printThread = new Thread(()->{
			print();
		});
        
        downloadThread.start();
        printThread.start();
  }
```
### Method Referencing for Threads
We can even simply the above main method by using method referencing. This is even easier to write and provide much cleaner code. This can be used if no other functionality in the run method is required but to call the methods.
```java
public static void main(String[] args) 
  {
    	Thread downloadThread = new Thread(Driver::downloadFile);
		
		Thread printThread = new Thread(Driver::print);
        
        downloadThread.start();
        printThread.start();
  }
```

## Joining Threads
It is sometimes desirable to make sure that main thread does not exist before all the threads have completed their execution. Joining threads can be beneficial in such cases:

Driver.java
```java
	package com.cmu;

	import java.io.BufferedReader;
	import java.io.BufferedWriter;
	import java.io.FileNotFoundException;
	import java.io.FileReader;
	import java.io.FileWriter;
	import java.io.IOException;

	public class Driver 
	{

		public static void readFile()
		{
			BufferedReader reader = null;
			try 
			{
				reader = new BufferedReader(new FileReader("input.txt"));
				String line;
				
				while ((line = reader.readLine()) != null)
				{
					System.out.println("Read: " + line);
					Thread.sleep(500);
				}
			} 
			catch (FileNotFoundException e) 
			{
				e.printStackTrace();
			} 
			catch (IOException e) 
			{
				e.printStackTrace();
			} 
			catch (InterruptedException e) 
			{
				e.printStackTrace();
			}
			finally
			{
				try 
				{
					reader.close();
				} 
				catch (IOException e) 
				{
					e.printStackTrace();
				}
			}
		}
		
		public static void writeFile()
		{
			BufferedWriter writer = null;
			try 
			{
				writer = new BufferedWriter(new FileWriter("output.txt"));
				for (int i=0; i<5; i++)
				{
					String data = "Line " + i;
					writer.write(data);
					writer.newLine();
					System.out.println("Written: " + data);
					Thread.sleep(1000);
				}
			} 
			catch (IOException e) 
			{
				e.printStackTrace();
			} 
			catch (InterruptedException e) 
			{
				e.printStackTrace();
			}
			finally {
				try 
				{
					writer.close();
				} 
				catch (IOException e) 
				{
					e.printStackTrace();
				}
			}
			
		}

		public static void main(String[] args) throws InterruptedException 
		{
			Thread readerThread = new Thread(()->{
				readFile();
			});
			
			Thread writerThread = new Thread(()->{
				writeFile();
			});
			
			readerThread.start();
			writerThread.start();
			
			readerThread.join();
			writerThread.join();
			
			System.out.println("\nReading Writing Completed!");
		}
	}
 ```
