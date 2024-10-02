# Design Patterns II

## Adapter Pattern
Adapter Patterns help in making incompatible types work together.
- Let's assume we have a sensor that give us temperature in celsius and we have a display that shows us temperature only in Fahrenheit.
- We can create an adapter for these two incompatible types to work with each other, e.g., changing between color and black & white.

Temperature.java
```java	
	public interface Temperature 
	{
		double getTempCelsius();
		
	}
```
Celsius.java
```java	
	public class Celsius implements Temperature
	{

		@Override
		public double getTempCelsius() 
		{
			return 25.0;
		}
		
	}
```
FahrenheitTemp.java
```java
	public interface FahrenheitTemp 
	{
		double getTempFahrenheit();
		
	}
```
Fahrenheit.java
```java	
	public class Fahrenheit implements FahrenheitTemp
	{
		private Temperature temp;

		Fahrenheit(Temperature temp)
		{
			this.temp = temp;
		}

		@Override
		public double getTempFahrenheit() 
		{
			double celsius = temp.getTempCelsius();
			return celsius * (9/5) + 32;
		}
		
	}
```
Driver.java
```java	
	public class Driver
	{
		public static void main(String[] args) 
		{
			Temperature celiusTemp = new Celsius();
			Fahrenheit fahrenheit = new Fahrenheit(celiusTemp);

			double temp = fahrenheit.getTempFahrenheit();

			System.out.println("25.0 Celius in Fahrenheit is " + temp);
		}
	}
```
Let's take another example of Adapter that is built-into Java

Driver.java
```java	
	import java.util.Arrays;
	import java.util.List;

	public class Driver {

		public static void main(String[] args) 
		{
			String[] fruits = {"Apple", "Banana", "Cherry"};
					
			System.out.println(fruits);
			
		}

	}
```
- The above program would simply display the object as string instead of showing the elements of the array as regular arrays do not have any built-in method for showing their elements except manually iterating through them.
- We can modify the above program to use an Adapter that can help above array work with a List interface which has better methods to display elements of the array
```java	
	import java.util.Arrays;
	import java.util.List;

	public class Driver {

		public static void main(String[] args) 
		{
			String[] fruits = {"Apple", "Banana", "Cherry"};
			
			List<String> list = Arrays.asList(fruits);
			
			System.out.println(list);
			
		}

	}
```
## Chain of Responsiblity
Chain of Responsibility patterns help in handling request in a chain
- Let's assume we have some purchase requests which are to be approved by each chain
	- Manager handles requests < $ 100
	- Director handles requests < $ 1000
	- President handles requests > $ 5000
		
PurchaseRequest.java
```java	
	public class PurchaseRequest
	{
		private double amount;

		PurchaseRequest(double amount)
		{
			this.amount = amount;
		}
		public double getAmount()
		{
			return this.amount;
		}
	}	
```	
PurchaseHandler.java
```java	
	public interface PurchaseHandler 
	{
		void setNextHandler(PurchaseHandler handler);
		void handleRequest(PurchaseRequest request);
	}
```	
Manager.java
```java	
	public class Manager implements PurchaseHandler
	{
		private static final double ALLOWABLE_AMOUNT = 100;
		private PurchaseHandler nextHandler;

		@Override
		public void setNextHandler(PurchaseHandler handler) 
		{
			this.nextHandler = handler;

		}

		@Override
		public void handleRequest(PurchaseRequest request) 
		{
			if (request.getAmount()<= ALLOWABLE_AMOUNT)
			{
				System.out.println("Manager approves the request of $"+ request.getAmount());
			}
			else if (nextHandler != null)
			{
				nextHandler.handleRequest(request);
			}
			else
			{
				System.out.println("Request exceeds the allowable limit");
			}
		}
		
	}
```
Director.java
```java	
	public class Director implements PurchaseHandler
	{
		private static final double ALLOWABLE_AMOUNT = 1000;
		private PurchaseHandler nextHandler;

		@Override
		public void setNextHandler(PurchaseHandler handler) 
		{
			this.nextHandler = handler;

		}

		@Override
		public void handleRequest(PurchaseRequest request) 
		{
			if (request.getAmount()<= ALLOWABLE_AMOUNT)
			{
				System.out.println("Director approves the request of $"+ request.getAmount());
			}
			else if (nextHandler != null)
			{
				nextHandler.handleRequest(request);
			}
			else
			{
				System.out.println("Request exceeds the allowable limit");
			}
		}
		
	}
```
President.java
```java	
	public class President implements PurchaseHandler
	{
		private static final double ALLOWABLE_AMOUNT = 5000;

		@Override
		public void setNextHandler(PurchaseHandler handler) 
		{

		}

		@Override
		public void handleRequest(PurchaseRequest request) 
		{
			if (request.getAmount() <= ALLOWABLE_AMOUNT)
			{
				System.out.println("President approves the request of $"+ request.getAmount());
			}
			else
			{
				System.out.println("Request cannot be approved");
			}
		}
		
	}
```
Driver.java
```java	
	public class Driver 
	{
		public static void main(String[] args) 
		{
			PurchaseHandler manager = new Manager();
			PurchaseHandler director = new Director();
			PurchaseHandler president = new President();

			manager.setNextHandler(director);
			director.setNextHandler(president);

			PurchaseRequest request1 = new PurchaseRequest(100);
			PurchaseRequest request2 = new PurchaseRequest(1000);
			PurchaseRequest request3 = new PurchaseRequest(5000);

			manager.handleRequest(request1);
			manager.handleRequest(request2);
			manager.handleRequest(request3);

			
		}
	}
```

Let's take another example of Chain of Responsibilities that is built-into Java

Driver.java
```java	
	public class Driver 
	{

		public static void main(String[] args) 
		{
			try
			{
				processRequest(null);
				//processRequest("Invalid");
				//throw new Exception("General");
			}
			catch(Exception e)
			{
				handleException(e);
			}

		}
		
		public static void processRequest(String input)
		{
			if (input == null)
			{
				throw new NullPointerException("Input cannot be null");
			}
			else if ("Invalid".equals(input))
			{
				throw new IllegalArgumentException("Invalid Input Provided");
			}

		}
		public static void handleException(Exception e)
		{
			if (e instanceof NullPointerException)
			{
				System.out.println("Handling Null Pointer Exception");
			}
			else if (e instanceof IllegalArgumentException)
			{
				System.out.println("Handling Illegal Argument Exception");
			}
			else
			{
				System.out.println("Handling General Exception");
			}
		}

	}
```	
- If it’s a NullPointerException, it prints a specific message.
- If it’s an IllegalArgumentException, it prints a different message.
- For any other exception, it falls back to a general handling message.
