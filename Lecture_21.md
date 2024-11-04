# FX Collections

## Combobox
A combo box, also known as a choice list or drop-down list, contains a list of items from which the user can choose.

MyGUI.java
```java

	package com.cmu;

	import javafx.application.Application;
	import javafx.scene.Scene;
	import javafx.scene.control.ComboBox;
	import javafx.scene.layout.BorderPane;
	import javafx.stage.Stage;

	public class MyGUI extends Application
	{

		@Override
		public void start(Stage primaryStage) throws Exception 
		{
			
			BorderPane pane = new BorderPane();
			
			ComboBox<String> fruits = new ComboBox<String>();
			fruits.getItems().addAll("Apple", "Banana", "Grapes", "Orange");
			fruits.setValue("Apple");
			
			pane.setCenter(fruits);
			
			Scene scene = new Scene(pane, 250, 200); 

			primaryStage.setTitle("My GUI");
			primaryStage.setScene(scene);
			primaryStage.show();

		}



		public static void main(String[] args) 
		{
			launch(args);
			
		}

	}

```
A `String[]` can be passed to `addAll()` function of the ComboBox

```Java
	@Override
	public void start(Stage primaryStage) throws Exception 
	{
		
		BorderPane pane = new BorderPane();
		
		String[] fruitList = {"Apple", "Banana", "Grapes", "Orange"};
		
		ComboBox<String> fruits = new ComboBox<String>();
		fruits.getItems().addAll(fruitList);
		fruits.setValue(fruitList[0]);
		
		pane.setCenter(fruits);
	    
	    Scene scene = new Scene(pane, 250, 200); 

	    primaryStage.setTitle("My GUI");
	    primaryStage.setScene(scene);
	    primaryStage.show();

	}
```

An `ArrayList` can also be passed to the `addAll` function of the ComboBox

```java
	@Override
	public void start(Stage primaryStage) throws Exception 
	{
		
		BorderPane pane = new BorderPane();
		
		ArrayList<String> fruitList = new ArrayList<>();
		fruitList.add("Apple");
		fruitList.add("Banana");
		fruitList.add("Orange");
		fruitList.add("Melon");
		fruitList.add("Grapes");
		
		ComboBox<String> fruits = new ComboBox<String>();
		fruits.getItems().addAll(fruitList);
		fruits.setValue(fruitList.get(0));
		
		pane.setCenter(fruits);
	    
	    Scene scene = new Scene(pane, 250, 200); 

	    primaryStage.setTitle("My GUI");
	    primaryStage.setScene(scene);
	    primaryStage.show();

	}

```
An Action Event can be set on ComboxBox as below:
```java

	@Override
	public void start(Stage primaryStage) throws Exception 
	{
		
		BorderPane pane = new BorderPane();
		
		VBox vBox = new VBox();
		
		ArrayList<String> fruitList = new ArrayList<>();
		fruitList.add("Apple");
		fruitList.add("Banana");
		fruitList.add("Orange");
		fruitList.add("Melon");
		fruitList.add("Grapes");
		
		ComboBox<String> fruits = new ComboBox<String>();
		fruits.getItems().addAll(fruitList);
		fruits.setValue(fruitList.get(0));
		
		Label lblFruit = new Label("Select a Fruit from the List");
		
		vBox.getChildren().addAll(fruits, lblFruit);
		vBox.setAlignment(Pos.CENTER);
		VBox.setMargin(lblFruit, new Insets(20));
		
		pane.setCenter(vBox);
		
		fruits.setOnAction(e-> {
			lblFruit.setText(fruits.getValue());
		});
	    
	    Scene scene = new Scene(pane, 250, 200); 

	    primaryStage.setTitle("My GUI");
	    primaryStage.setScene(scene);
	    primaryStage.show();

	}


```

## ListView
A list view is a control that basically performs the same function as a combo box, but it enables the user to choose a single value or multiple values.


MyGUI.java
```java
	
	package com.cmu;

	import java.util.ArrayList;

	import javafx.application.Application;
	import javafx.geometry.Insets;
	import javafx.geometry.Pos;
	import javafx.scene.Scene;
	import javafx.scene.control.ComboBox;
	import javafx.scene.control.Label;
	import javafx.scene.control.ListView;
	import javafx.scene.layout.BorderPane;
	import javafx.scene.layout.VBox;
	import javafx.stage.Stage;

	public class MyGUI extends Application
	{

		@Override
		public void start(Stage primaryStage) throws Exception 
		{
			
			BorderPane pane = new BorderPane();
			
			ArrayList<String> fruitList = new ArrayList<>();
			fruitList.add("Apple");
			fruitList.add("Banana");
			fruitList.add("Orange");
			fruitList.add("Melon");
			fruitList.add("Grapes");
			
			ListView<String> fruits = new ListView<String>();
			fruits.getItems().addAll(fruitList);
			fruits.setPrefSize(100, 100);
			
			Label lblFruit = new Label("Select a fruit from the List");
					
			pane.setLeft(fruits);
			pane.setCenter(lblFruit);
			
			fruits.getSelectionModel().selectedItemProperty().addListener((observable, oldValue, newValue) -> {
				lblFruit.setText(newValue);
			});
			
			Scene scene = new Scene(pane, 300, 200); 

			primaryStage.setTitle("My GUI");
			primaryStage.setScene(scene);
			primaryStage.show();

		}



		public static void main(String[] args) 
		{
			launch(args);
			
		}

	}


```

The above can also be achieved using the following code for the listener:

```java
		fruits.getSelectionModel().selectedItemProperty().addListener(e -> {
			lblFruit.setText(fruits.getSelectionModel().getSelectedItem());
		});

```

Multiple Values can be selected from the ListView;

```Java
	@Override
	public void start(Stage primaryStage) throws Exception 
	{
		
		BorderPane pane = new BorderPane();
		
		ArrayList<String> fruitList = new ArrayList<>();
		fruitList.add("Apple");
		fruitList.add("Banana");
		fruitList.add("Orange");
		fruitList.add("Melon");
		fruitList.add("Grapes");
		
		ListView<String> fruits = new ListView<String>();
		fruits.getItems().addAll(fruitList);
		fruits.setPrefSize(100, 100);
		fruits.getSelectionModel().setSelectionMode(SelectionMode.MULTIPLE);
		
		Label lblFruit = new Label("Select a fruit from the List");
				
		pane.setLeft(fruits);
		pane.setCenter(lblFruit);
		
		
		fruits.getSelectionModel().selectedItemProperty().addListener(e -> {
			System.out.println(fruits.getSelectionModel().getSelectedItems());
		});
		
	    Scene scene = new Scene(pane, 300, 200); 

	    primaryStage.setTitle("My GUI");
	    primaryStage.setScene(scene);
	    primaryStage.show();

	}

```

Instead of showing these multiple items on the console, we can show those items on the Label

```Java
	@Override
	public void start(Stage primaryStage) throws Exception 
	{
		
		BorderPane pane = new BorderPane();
		
		ArrayList<String> fruitList = new ArrayList<>();
		fruitList.add("Apple");
		fruitList.add("Banana");
		fruitList.add("Orange");
		fruitList.add("Melon");
		fruitList.add("Grapes");
		
		ListView<String> fruits = new ListView<String>();
		fruits.getItems().addAll(fruitList);
		fruits.setPrefSize(100, 100);
		fruits.getSelectionModel().setSelectionMode(SelectionMode.MULTIPLE);
		
		Label lblFruit = new Label("Select a fruit from the List");
				
		pane.setLeft(fruits);
		pane.setCenter(lblFruit);
		
		
		fruits.getSelectionModel().selectedItemProperty().addListener(e -> {
			List<String> selectedItems = fruits.getSelectionModel().getSelectedItems(); 
			lblFruit.setText(String.join(", ", selectedItems));
			
		});
		
	    Scene scene = new Scene(pane, 300, 200); 

	    primaryStage.setTitle("My GUI");
	    primaryStage.setScene(scene);
	    primaryStage.show();

	}

```

ListCell can be customized based on need as below:

```Java
	fruits.setCellFactory(e -> new ListCell<String>() {
			protected void updateItem(String item, boolean empty)
			{
				setText(item);
				setTextFill(Color.RED);
				setFont(new Font("Ariel", 18));
			}
		});

```