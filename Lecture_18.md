# Event Driven Programming

## Event Handling
The interface contains the  method for processing the action event. Your handler class must override this method to respond to the event.

Driver.java
```java	
	package com.cmu;

	import javafx.application.Application;
	import javafx.event.ActionEvent;
	import javafx.event.EventHandler;
	import javafx.scene.Scene;
	import javafx.scene.control.Button;
	import javafx.scene.layout.Pane;
	import javafx.scene.text.Text;
	import javafx.stage.Stage;

	public class MyGUI extends Application implements EventHandler<ActionEvent>
	{
		private Text txt;

		@Override
		public void start(Stage primaryStage) throws Exception 
		{
			Button btnShow = new Button("Show Text");
			txt = new Text("Initial Text");
			
			btnShow.setLayoutX(100);
			btnShow.setLayoutY(150);
			
			btnShow.setOnAction(this);
			
			txt.setLayoutX(100);
			txt.setLayoutY(80);

			Pane pane = new Pane();
			
			pane.getChildren().add(btnShow);
			pane.getChildren().add(txt);

			Scene scene = new Scene(pane, 300, 300);

			primaryStage.setTitle("My GUI");
			primaryStage.setScene(scene);
			primaryStage.show();	
			
		}
		
		public static void main(String[] args) {
			launch(args);
		}

		@Override
		public void handle(ActionEvent event) {
			System.out.println("Button Clicked");
			
		}

	}
```

Instead of showing the message on the console, let's show that message on the text:
```java
@Override
public void handle(ActionEvent event) 
{
   txt.setText("Button Clicked");	
}
```		

## Handling Events with Shapes
Let's now work with shapes and event handling. Let's create a Java program that resizes the circle on the click of a button.

Driver.java
```java	
	package com.cmu;

	import javafx.application.Application;
	import javafx.event.ActionEvent;
	import javafx.event.EventHandler;
	import javafx.scene.Scene;
	import javafx.scene.control.Button;
	import javafx.scene.control.SplitPane.Divider;
	import javafx.scene.layout.Pane;
	import javafx.scene.paint.Color;
	import javafx.scene.shape.Circle;
	import javafx.scene.text.Text;
	import javafx.stage.Stage;

	public class MyGUI extends Application implements EventHandler<ActionEvent>
	{
		private Circle circle;

		@Override
		public void start(Stage primaryStage) throws Exception 
		{
			Button btnShow = new Button("Reduce Size");
			
			btnShow.setLayoutX(110);
			btnShow.setLayoutY(220);
			
			btnShow.setOnAction(this);
			
			circle = new Circle(50);    

			Pane pane = new Pane();
			
			circle.centerXProperty().bind(pane.widthProperty().divide(2));
			circle.centerYProperty().bind(pane.heightProperty().divide(2));
			
			pane.getChildren().add(btnShow);
			pane.getChildren().add(circle);

			Scene scene = new Scene(pane, 300, 300);

			primaryStage.setTitle("My GUI");
			primaryStage.setScene(scene);
			primaryStage.show();	
			
		}
		
		public static void main(String[] args) {
			launch(args);
		}

		@Override
		public void handle(ActionEvent event) {
			System.out.println("Button Clicked");
			
			circle.setRadius(20);
			circle.setFill(new Color(0.5, 0.0, 0.0, 1));
			
		}

	}
```

## Anonymous Inner Class Handlers

In order to simplify the handling of events, annonymous inner classes can be used to handle the action events. The above code can be simplified using annonymous inner class handlers as below:\

Driver.java
```java	
	package com.cmu;

	import javafx.application.Application;
	import javafx.event.ActionEvent;
	import javafx.event.EventHandler;
	import javafx.scene.Scene;
	import javafx.scene.control.Button;
	import javafx.scene.control.SplitPane.Divider;
	import javafx.scene.layout.Pane;
	import javafx.scene.paint.Color;
	import javafx.scene.shape.Circle;
	import javafx.scene.text.Text;
	import javafx.stage.Stage;

	public class MyGUI extends Application
	{
		private Circle circle;

		@Override
		public void start(Stage primaryStage) throws Exception 
		{
			Button btnShow = new Button("Reduce Size");
			
			btnShow.setLayoutX(110);
			btnShow.setLayoutY(220);
			
			btnShow.setOnAction(new EventHandler<ActionEvent>() {
				
				@Override
				public void handle(ActionEvent event) 
				{
					System.out.println("Button Clicked");
					
					circle.setRadius(20);
					circle.setFill(new Color(0.5, 0.0, 0.0, 0.5));
					
				}
			});
			
			circle = new Circle(50);    

			Pane pane = new Pane();
			
			circle.centerXProperty().bind(pane.widthProperty().divide(2));
			circle.centerYProperty().bind(pane.heightProperty().divide(2));
			
			pane.getChildren().add(btnShow);
			pane.getChildren().add(circle);

			Scene scene = new Scene(pane, 300, 300);

			primaryStage.setTitle("My GUI");
			primaryStage.setScene(scene);
			primaryStage.show();	
			
		}
		
		public static void main(String[] args) {
			launch(args);
		}


	}
```

## Event Handlers and Lambda Expressions

The above code can be further simplified using lambda expressions as below:

Driver.java
```java	
	package com.cmu;

	import javafx.application.Application;
	import javafx.event.ActionEvent;
	import javafx.event.EventHandler;
	import javafx.scene.Scene;
	import javafx.scene.control.Button;
	import javafx.scene.control.SplitPane.Divider;
	import javafx.scene.layout.Pane;
	import javafx.scene.paint.Color;
	import javafx.scene.shape.Circle;
	import javafx.scene.text.Text;
	import javafx.stage.Stage;

	public class MyGUI extends Application
	{
		private Circle circle;

		@Override
		public void start(Stage primaryStage) throws Exception 
		{
			Button btnShow = new Button("Reduce Size");
			
			btnShow.setLayoutX(110);
			btnShow.setLayoutY(220);
			
			btnShow.setOnAction(event-> 
			{
				System.out.println("Button Clicked");
				circle.setRadius(20);
				circle.setFill(new Color(0.5, 0.0, 0.0, 0.5));
					
				
			});
			
			circle = new Circle(50);    

			Pane pane = new Pane();
			
			circle.centerXProperty().bind(pane.widthProperty().divide(2));
			circle.centerYProperty().bind(pane.heightProperty().divide(2));
			
			pane.getChildren().add(btnShow);
			pane.getChildren().add(circle);

			Scene scene = new Scene(pane, 300, 300);

			primaryStage.setTitle("My GUI");
			primaryStage.setScene(scene);
			primaryStage.show();	
			
		}
		
		public static void main(String[] args) {
			launch(args);
		}


	}
```

## Mouse Events
A Mouse Event is fired whenever a mouse button is pressed, released, clicked, moved, or dragged on a node or a scene.

Let's write a program that shows on a text a message whenenver cursor enters the circle and changes it back to initial text when cursor exits the circle

Driver.java
```java	
	package com.cmu;

	import javafx.application.Application;
	import javafx.event.ActionEvent;
	import javafx.event.EventHandler;
	import javafx.scene.Scene;
	import javafx.scene.control.Button;
	import javafx.scene.control.SplitPane.Divider;
	import javafx.scene.layout.Pane;
	import javafx.scene.paint.Color;
	import javafx.scene.shape.Circle;
	import javafx.scene.text.Text;
	import javafx.stage.Stage;

	public class MyGUI extends Application
	{
		private Circle circle;

		@Override
		public void start(Stage primaryStage) throws Exception 
		{
			Button btnShow = new Button("Reduce Size");
			
			btnShow.setLayoutX(110);
			btnShow.setLayoutY(220);
			
			btnShow.setOnAction(event-> 
			{
				System.out.println("Button Clicked");
				circle.setRadius(20);
				circle.setFill(new Color(0.5, 0.0, 0.0, 0.5));
					
				
			});
			
			circle = new Circle(50);    
			
			Text txt = new Text("Initial Text");
			
			txt.setLayoutX(120);
			txt.setLayoutY(280);

			Pane pane = new Pane();
			
			circle.centerXProperty().bind(pane.widthProperty().divide(2));
			circle.centerYProperty().bind(pane.heightProperty().divide(2));
			
			pane.getChildren().add(btnShow);
			pane.getChildren().add(circle);
			pane.getChildren().add(txt);
			
			circle.setOnMouseEntered(event->
			{
				txt.setText("Cursor entered circle");
			});
			
			circle.setOnMouseExited(event -> 
			{
				txt.setText("Initial Text");
			});

			Scene scene = new Scene(pane, 300, 300);

			primaryStage.setTitle("My GUI");
			primaryStage.setScene(scene);
			primaryStage.show();	
			
		}
		
		public static void main(String[] args) {
			launch(args);
		}


	}
```

## Key Events

Besides capturing the mouse events, we can capture keyboard's key events. 

Let's create a program that moves the circle up and down on pressing the UP and DOWN arrow keys on the keyboard

Driver.java
```java	
	package com.cmu;

	import javafx.application.Application;
	import javafx.event.ActionEvent;
	import javafx.event.EventHandler;
	import javafx.scene.Scene;
	import javafx.scene.control.Button;
	import javafx.scene.control.SplitPane.Divider;
	import javafx.scene.layout.Pane;
	import javafx.scene.paint.Color;
	import javafx.scene.shape.Circle;
	import javafx.scene.text.Text;
	import javafx.stage.Stage;

	public class MyGUI extends Application
	{
		private Circle circle;

		@Override
		public void start(Stage primaryStage) throws Exception 
		{
					
			circle = new Circle(20);    
			
			Pane pane = new Pane();
			
			circle.setCenterX(150); 
			circle.setCenterY(150);  
			
			pane.getChildren().add(circle);

			Scene scene = new Scene(pane, 300, 300);
			
			scene.setOnKeyPressed(e -> 
			{
				switch(e.getCode())
				{
					case UP: circle.setCenterY(circle.getCenterY() - 10); break;
					case DOWN: circle.setCenterY(circle.getCenterY() + 10); break;
					default:
					break; 
				}
			});

			primaryStage.setTitle("My GUI");
			primaryStage.setScene(scene);
			primaryStage.show();	
			
			
		}
		
		public static void main(String[] args) {
			launch(args);
		}


	}
```
