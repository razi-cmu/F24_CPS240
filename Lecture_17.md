# GUI (Basic Components and Event Driven Programming)

## JavaFX Basics
JavaFX is the recommended framework for developing modern Java applications, providing a rich set of features and tools to create dynamic, user-friendly interfaces.

### Setting up JavaFX in Eclipse
* Download JavaFX SDK from https://openjfx.io/index.html
* Once downloaded, extract to some location on your computer
* In Eclipse go to Preferences > Build Path > User Libraries and add a new library "JavaFX" and from Add External JARs, add all the JAR files in the downloaded folder's lib folder
* Apply and Close.
* In Eclipse > Help > Eclipse Marketplace, add JavaFX plugin
* You can now create a new Java Project
  
In some cases, you might have to add the above created User Library manually to your Java projects. Follow steps below:
* Right Click your Java Project in Eclipse and Click Build Path > Configure Build Path
* Select the Libraries Tab and click Classpath.
* Click Add Library > User Library, select JavaFX and click Finish.
  
In most of the cases, the above would solve the problem of JavaFX classes not available to use. However, in extreme cases you might have to configure the runtime environment for JavaFX
* In Eclipse in the Menu Bar select Run > Run ConfigurationS. A window will pop up; click Arguments and paste the following in the VM Arguments:
```
--module-path "D:\Utils\openjfx-23.0.1_windows-x64_bin-sdk\javafx-sdk-23.0.1/lib" --add-modules javafx.controls,javafx.fxml
```
Make sure you update the above highlighted part to the path of JavaFX SDK you downloaded and extracted.
	
### First JavaFX Application
Once JavaFX is setup, you are now ready to create a GUI application using JavaFX in Java.

`Main.java`
```java
	package com.cmu;

	import javafx.application.Application;
	import javafx.scene.Scene;
	import javafx.scene.control.Button;
	import javafx.stage.Stage;

	public class MyGUI extends Application 
	{

		@Override
		public void start(Stage primaryStage) throws Exception 
		{
			Button btn = new Button("Click me");
			Scene scene = new Scene(btn, 300, 300);
			
			primaryStage.setTitle("My GUI");
			primaryStage.setScene(scene);
			primaryStage.show();

			
		}
		
		public static void main(String[] args) {
			launch(args);
		}

	}
```	
	
### Multistage JavaFX Application
Multiple stages can be added to a JavaFX Application

`Main.java`
```java
	package com.cmu;

	import javafx.application.Application;
	import javafx.scene.Scene;
	import javafx.scene.control.Button;
	import javafx.stage.Stage;

	public class MyGUI extends Application 
	{

		@Override
		public void start(Stage primaryStage) throws Exception 
		{
			Button btn = new Button("Click me");
			Scene scene = new Scene(btn, 300, 300);
			
			primaryStage.setTitle("My GUI");
			primaryStage.setScene(scene);
			primaryStage.show();
			
			Stage stage = new Stage();
			stage.setTitle("Another Scene");
			Scene scene2 = new Scene(new Button("Hello"), 200, 200);
			stage.setScene(scene2);
			stage.show();
			
		}
		
		public static void main(String[] args) {
			launch(args);
		}

	}
```

### Grouping multiple nodes
A Group helps in holding multiple nodes. The code below creates a Group, adds both buttons to it and then adds the group to the scene.

`Main.java`
```java
	package com.cmu;

	import javafx.application.Application;
	import javafx.scene.Group;
	import javafx.scene.Scene;
	import javafx.scene.control.Button;
	import javafx.stage.Stage;

	public class MyGUI extends Application 
	{

		@Override
		public void start(Stage primaryStage) throws Exception 
		{
			Button btn1 = new Button("Click me");
			Button btn2 = new Button("Click me 2");
			
			btn1.setLayoutX(50);
			btn1.setLayoutY(100);
			
			btn2.setLayoutX(150);
			btn2.setLayoutY(100);
			
			Group group = new Group(btn1, btn2);
			Scene scene = new Scene(group, 300, 300);
			
			primaryStage.setTitle("My GUI");
			primaryStage.setScene(scene);
			primaryStage.show();
	
		}
		
		public static void main(String[] args) {
			launch(args);
		}

	}
```
### Working with Text
A Text can also be added to a Group.
```java
	@Override
	public void start(Stage primaryStage) throws Exception 
	{
		Button btn1 = new Button("Click me");

		Text txtHello = new Text("Hello I am Text");

		btn1.setLayoutX(110);
		btn1.setLayoutY(100);
		
		txtHello.setLayoutX(110);
		txtHello.setLayoutY(160);
		
		Group group = new Group(btn1, txtHello);
		Scene scene = new Scene(group, 300, 300);
		
		primaryStage.setTitle("My GUI");
		primaryStage.setScene(scene);
		primaryStage.show();
		
	}
```

### Look and Feel of Nodes
Several properties of nodes can be changed

`Main.java`
```java
	package com.cmu;

	import javafx.application.Application;
	import javafx.scene.Group;
	import javafx.scene.Scene;
	import javafx.scene.control.Button;
	import javafx.scene.paint.Color;
	import javafx.scene.text.Font;
	import javafx.scene.text.Text;
	import javafx.stage.Stage;

	public class MyGUI extends Application 
	{

		@Override
		public void start(Stage primaryStage) throws Exception 
		{
			Button btn1 = new Button("Click me");
			btn1.setMinWidth(80);
			btn1.setFont(new Font("Arial", 18));
			Text txtHello = new Text("Hello I am Text");
			txtHello.setFont(new Font("Arial", 18));
			txtHello.setFill(Color.RED);
			
			
			btn1.setLayoutX(110);
			btn1.setLayoutY(100);
			
			txtHello.setLayoutX(110);
			txtHello.setLayoutY(160);
			
			Group group = new Group(btn1, txtHello);
			Scene scene = new Scene(group, 300, 300);
			
			primaryStage.setTitle("My GUI");
			primaryStage.setScene(scene);
			primaryStage.show();
			
		}
		
		public static void main(String[] args) {
			launch(args);
		}

	}
```

### Working with Shapes
Shapes can also be added to a scene in JavaFX Application
```java
	@Override
	public void start(Stage primaryStage) throws Exception 
	{
		Circle circle = new Circle(150,110,50);
		
		Pane pane = new Pane(circle);
		
		Scene scene = new Scene(pane, 300, 300);
		
		primaryStage.setTitle("My GUI");
		primaryStage.setScene(scene);
		primaryStage.show();
		
	}
```
