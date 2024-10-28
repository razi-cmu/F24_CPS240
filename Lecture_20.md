# Java GUI Layouts II

## HBox and VBox
Recall that a FlowPane can lay out its children in multiple rows or multiple columns, but an HBox or a VBox can lay out children only in one row or one column

### HBox
An HBox lays out its children in a single horizontal row.

MyGUI.java
```java

	package com.cmu;

	import javafx.application.Application;

	import javafx.geometry.Pos;
	import javafx.scene.Scene;
	import javafx.scene.control.Label;
	import javafx.scene.layout.HBox;
	import javafx.stage.Stage;

	public class MyGUI extends Application
	{

		@Override
		public void start(Stage primaryStage) throws Exception 
		{
			Label[] courses = {
					new Label("CPS 190"),
					new Label(" CPS 191"),
					new Label(" CPS 240"),
					new Label(" CPS 245"),
					new Label(" CPS 353"),
					};
			
			HBox hBox = new HBox();
			
			for (Label course: courses)
			{

				hBox.getChildren().add(course);
				
			}
			
			hBox.setStyle("-fx-border-color: red;");
			hBox.setAlignment(Pos.CENTER);
			
			
			Scene scene = new Scene(hBox, 300, 300);
			
			primaryStage.setTitle("My GUI");
			primaryStage.setScene(scene);
			primaryStage.show();
			
		}
		
		public static void main(String[] args) {
			launch(args);
		}


	}

```

### VBox
A VBox lays out its children in a single Vertical column.

```java
	package com.cmu;

	import javafx.application.Application;

	import javafx.geometry.Pos;
	import javafx.scene.Scene;
	import javafx.scene.control.Label;
	import javafx.scene.layout.HBox;
	import javafx.scene.layout.VBox;
	import javafx.stage.Stage;

	public class MyGUI extends Application
	{

		@Override
		public void start(Stage primaryStage) throws Exception 
		{
			Label[] courses = {
					new Label("CPS 190"),
					new Label(" CPS 191"),
					new Label(" CPS 240"),
					new Label(" CPS 245"),
					new Label(" CPS 353"),
					};
			
			HBox hBox = new HBox();
			
			for (Label course: courses)
			{

				hBox.getChildren().add(course);
				
			}
			
			hBox.setStyle("-fx-border-color: red;");
			hBox.setAlignment(Pos.CENTER);
			
			VBox vBox = new VBox(hBox);
			vBox.setStyle("-fx-border-color: blue;");
			vBox.setAlignment(Pos.CENTER);
			
			
			Scene scene = new Scene(vBox, 300, 300);
			
			primaryStage.setTitle("My GUI");
			primaryStage.setScene(scene);
			primaryStage.show();
			
		}
		
		public static void main(String[] args) {
			launch(args);
		}


	}


```

VBox and HBox are a good way of handling images

```java

	@Override
	public void start(Stage primaryStage) throws Exception 
	{
		Image image = new Image("./CMU.png", 200, 200, true, true);
		ImageView imageView = new ImageView(image);
		
		Label[] courses = {
				new Label("CPS 190"),
				new Label(" CPS 191"),
				new Label(" CPS 240"),
				new Label(" CPS 245"),
				new Label(" CPS 353"),
				};
		
		HBox hBox = new HBox();
		
		for (Label course: courses)
		{

			hBox.getChildren().add(course);
			
		}
		
		hBox.setStyle("-fx-border-color: red;");
		hBox.setAlignment(Pos.CENTER);
		
		VBox vBox = new VBox();
		vBox.getChildren().addAll(imageView, hBox);
		vBox.setStyle("-fx-border-color: blue; -fx-background-color: #FFFFFF;");
		vBox.setAlignment(Pos.CENTER);
	    
        
		Scene scene = new Scene(vBox, 300, 300);
		
		
		primaryStage.setTitle("My GUI");
		primaryStage.setScene(scene);
		primaryStage.show();
		
	}

```

## BorderPane
BorderPane lays out children in top, left, right, bottom, and center positions.


MyGUI.java
```java
	
	package com.cmu;

	import javafx.application.Application;
	import javafx.scene.Scene;
	import javafx.scene.control.Label;
	import javafx.scene.layout.BorderPane;
	import javafx.scene.layout.StackPane;
	import javafx.stage.Stage;

	public class MyGUI extends Application
	{

		@Override
		public void start(Stage primaryStage) throws Exception 
		{
			BorderPane pane = new BorderPane();
			pane.setTop(new StackPane(new Label("Top Element")));
			pane.setLeft(new StackPane(new Label("Left Element")));
			pane.setRight(new StackPane(new Label("Right Element")));
			pane.setBottom(new StackPane(new Label("Bottom Element")));
			pane.setCenter(new StackPane(new Label("Center Element")));
			
			
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
HBox and BorderPane can be combined to provide a GUI which is efficient.


```Java
	@Override
	public void start(Stage primaryStage) throws Exception 
	{
		
		Image image = new Image("./CMU.png", 150, 150, true, true);
		ImageView imageView = new ImageView(image);
		imageView.setStyle("-fx-border-color: red;");
		
		GridPane gridPane = new GridPane();
		gridPane.add(new Label("User Name"), 0, 0);
		gridPane.add(new TextField(), 1, 0);
		gridPane.add(new Label("Password"), 0, 1);
		gridPane.add(new PasswordField(), 1, 1);

		Button btnLogin = new Button("Login");
		Button btnCancel = new Button("Cancel");
		
		HBox hBox = new HBox();
		hBox.getChildren().add(btnLogin);
		hBox.getChildren().add(btnCancel);
		hBox.setAlignment(Pos.CENTER);
		hBox.setMargin(btnLogin, new Insets(0, 10, 0, 0));
		
		gridPane.add(hBox, 1, 2);
		
		gridPane.setAlignment(Pos.TOP_CENTER);
		gridPane.setHgap(8);
		gridPane.setVgap(8);
		
		BorderPane pane = new BorderPane();
		pane.setTop(new StackPane(imageView));
		pane.setBottom(new StackPane(new Label("Copyright @ 2024. All rights reserved to CMU.")));
		pane.setCenter(new StackPane(gridPane));
		
		pane.setStyle("-fx-background: white;"); 
        
		Scene scene = new Scene(pane, 300, 300);

		primaryStage.setTitle("My GUI");
		primaryStage.setScene(scene);
		primaryStage.show();
		
	}


```