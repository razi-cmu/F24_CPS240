# Java Generic II

## Java Generic and JavaFX
Using Java Generics with JavaFX for creating GUIs can add a layer of flexibility and type safety to your JavaFX applications.

Item.java
```java
	package com.cmu;

	public class Item<T> 
	{
		private T data;
		
		public Item(T data)
		{
			this.data = data;
		}
		
		public T getData()
		{
			return this.data;
		}
		public void setData(T data)
		{
			this.data = data;
		}

		@Override
		public String toString() {
			return data.toString();
		}
	}


```

MyGUI.java
```java

	package com.cmu;

	import java.util.ArrayList;
	import java.util.List;

	import javafx.application.Application;
	import javafx.geometry.Insets;
	import javafx.geometry.Pos;
	import javafx.scene.Scene;
	import javafx.scene.control.Button;
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
			
			ListView<Item<String>> listView = new ListView<>();
			
			ArrayList<Item<String>> items = new ArrayList<>();
			items.add(new Item<>("Apple"));
			items.add(new Item<>("Orange"));
			items.add(new Item<>("Banana"));
			items.add(new Item<>("Grapes"));
			items.add(new Item<>("Melon"));
			
			listView.getItems().addAll(items);
			
			Button btnRemove = new Button("Remove Item");
			
			VBox vBox = new VBox(10);
			vBox.setAlignment(Pos.CENTER);
			VBox.setMargin(btnRemove, new Insets(5));
			vBox.getChildren().addAll(listView, btnRemove);
			
			pane.setCenter(vBox);
			Scene scene = new Scene(pane, 300, 250);
			primaryStage.setScene(scene);
			primaryStage.setTitle("My GUI");
			primaryStage.show();
		}
		public static void main(String[] args) 
		{
			launch(args);
			
		}

	}


```

Let's update the above code to remove the selected item from the ListView on the click of Remove Item button:
```java
	btnRemove.setOnAction(e -> 
		{    
            Item<String> selectedItem = listView.getSelectionModel().getSelectedItem();
            
            if (selectedItem != null) 
            {
                items.remove(selectedItem);
                listView.getItems().remove(selectedItem);
            }
        });

```

Since Item is a Generic class, it can technically hold any type of object.

For example, lets pass it a Fruit type as below:

Fruit.java
```java
	package com.cmu;

	public class Fruit 
	{
		private String name;
		private String color;
		private int quantity;
		
		Fruit(String name, String color, int quantity)
		{
			this.name = name;
			this.color = color;
			this.quantity = quantity;
		}

		public String getName() {
			return name;
		}

		public void setName(String name) {
			this.name = name;
		}

		public String getColor() {
			return color;
		}

		public void setColor(String color) {
			this.color = color;
		}

		public int getQuantity() {
			return quantity;
		}

		public void setQuantity(int quantity) 
		{
			this.quantity = quantity;
		}

		@Override
		public String toString() {
			return this.name + ", " + this.color + ", " + this.quantity;
		}
		

	}

```

Item.java
```java
	package com.cmu;

	public class Item<T> 
	{
		private T data;
		
		public Item(T data)
		{
			this.data = data;
		}
		
		public T getData()
		{
			return this.data;
		}
		public void setData(T data)
		{
			this.data = data;
		}

		@Override
		public String toString() {
			return data.toString();
		}
	}


```

MyGUI.java
```java
	package com.cmu;

	import java.util.ArrayList;
	import java.util.List;

	import javafx.application.Application;
	import javafx.geometry.Insets;
	import javafx.geometry.Pos;
	import javafx.scene.Scene;
	import javafx.scene.control.Button;
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
			
			ListView<Item<Fruit>> listView = new ListView<>();
			
			ArrayList<Item<Fruit>> items = new ArrayList<>();
			items.add(new Item<>(new Fruit("Apple", "Red", 2)));
			items.add(new Item<>(new Fruit("Banana", "Yellow", 5)));
			items.add(new Item<>(new Fruit("Orange", "Orange", 4)));
			items.add(new Item<>(new Fruit("Melon", "Green", 6)));
			items.add(new Item<>(new Fruit("Grape", "Green", 12)));
			
			listView.getItems().addAll(items);
			
			Button btnRemove = new Button("Remove Item");
			
			btnRemove.setOnAction(e -> 
			{    
				Item<Fruit> selectedItem = listView.getSelectionModel().getSelectedItem();
				
				if (selectedItem != null) 
				{
					items.remove(selectedItem);
					listView.getItems().remove(selectedItem);
				}
			});
			
			VBox vBox = new VBox(10);
			vBox.setAlignment(Pos.CENTER);
			VBox.setMargin(btnRemove, new Insets(5));
			vBox.getChildren().addAll(listView, btnRemove);
			
			pane.setCenter(vBox);
			Scene scene = new Scene(pane, 300, 250);
			primaryStage.setScene(scene);
			primaryStage.setTitle("My GUI");
			primaryStage.show();
		}
		public static void main(String[] args) 
		{
			launch(args);
			
		}

	}

```

Let's now update our code to work with TableView instead of ListView keeping the Fruit and Item classes as is.

MyGUI
```java
	package com.cmu;

	import java.util.ArrayList;
	import java.util.List;

	import javafx.application.Application;
	import javafx.beans.property.SimpleIntegerProperty;
	import javafx.beans.property.SimpleStringProperty;
	import javafx.geometry.Insets;
	import javafx.geometry.Pos;
	import javafx.scene.Scene;
	import javafx.scene.control.Button;
	import javafx.scene.control.Label;
	import javafx.scene.control.ListView;
	import javafx.scene.control.TableColumn;
	import javafx.scene.control.TableView;
	import javafx.scene.layout.BorderPane;
	import javafx.scene.layout.HBox;
	import javafx.scene.layout.VBox;
	import javafx.stage.Stage;
	import javafx.scene.control.ListCell;
	import javafx.scene.control.TableColumn;
	import javafx.scene.control.cell.PropertyValueFactory;

	public class MyGUI extends Application
	{

		@Override
		public void start(Stage primaryStage) throws Exception 
		{
			BorderPane pane = new BorderPane();
			
			TableView<Item<Fruit>> tableView = new TableView<>();
			
			TableColumn<Item<Fruit>, String> nameCol = new TableColumn<>("Name");
			nameCol.setCellValueFactory(cellData -> new SimpleStringProperty(cellData.getValue().getData().getName()));
			
			TableColumn<Item<Fruit>, String> colorCol = new TableColumn<>("Color");
			colorCol.setCellValueFactory(cellData -> new SimpleStringProperty(cellData.getValue().getData().getColor()));
			
			TableColumn<Item<Fruit>, Integer> quantityCol = new TableColumn<>("Quantity");
			quantityCol.setCellValueFactory(cellData -> new SimpleIntegerProperty(cellData.getValue().getData().getQuantity()).asObject());
			
			
			tableView.getColumns().addAll(nameCol, colorCol, quantityCol);
			
			ArrayList<Item<Fruit>> items = new ArrayList<>();
			items.add(new Item<>(new Fruit("Apple", "Red", 2)));
			items.add(new Item<>(new Fruit("Banana", "Yellow", 5)));
			items.add(new Item<>(new Fruit("Orange", "Orange", 4)));
			items.add(new Item<>(new Fruit("Melon", "Green", 6)));
			items.add(new Item<>(new Fruit("Grape", "Green", 12)));
			
			
			tableView.getItems().addAll(items);
			
			Button btnRemove = new Button("Remove Item");
			
			btnRemove.setOnAction(e -> 
			{    
				Item<Fruit> selectedItem = tableView.getSelectionModel().getSelectedItem();
				
				if (selectedItem != null) 
				{
					items.remove(selectedItem);
					tableView.getItems().remove(selectedItem);
				}
			});
			
			VBox vBox = new VBox(10);
			vBox.setAlignment(Pos.CENTER);
			VBox.setMargin(btnRemove, new Insets(5));
			vBox.getChildren().addAll(tableView, btnRemove);
			
			pane.setCenter(vBox);
			Scene scene = new Scene(pane, 300, 250);
			primaryStage.setScene(scene);
			primaryStage.setTitle("My GUI");
			primaryStage.show();
		}
		public static void main(String[] args) 
		{
			launch(args);
			
		}

	}

```

We can use Java reflections to dynamically get the names of the columns as below:

MyGUI.java
```java
	package com.cmu;

	import java.lang.reflect.Field;
	import java.util.ArrayList;

	import javafx.application.Application;
	import javafx.beans.property.SimpleStringProperty;
	import javafx.geometry.Insets;
	import javafx.geometry.Pos;
	import javafx.scene.Scene;
	import javafx.scene.control.Button;
	import javafx.scene.control.TableColumn;
	import javafx.scene.control.TableView;
	import javafx.scene.layout.BorderPane;
	import javafx.scene.layout.VBox;
	import javafx.stage.Stage;


	public class MyGUI extends Application
	{

		@Override
		public void start(Stage primaryStage) throws Exception 
		{
			BorderPane pane = new BorderPane();
			
			TableView<Item<?>> tableView = new TableView<>();
			
			createDynamicColumns(tableView, Fruit.class);

	//		ArrayList<Item<Student>> items = new ArrayList<>();
	//		items.add(new Item<>(new Student("John", 21)));
	//		items.add(new Item<>(new Student("Steve", 22)));
	//		items.add(new Item<>(new Student("Bill", 23)));
	//		items.add(new Item<>(new Student("Elon", 20)));
	//		items.add(new Item<>(new Student("Tina", 21)));
			
			ArrayList<Item<Fruit>> items = new ArrayList<>();
			items.add(new Item<>(new Fruit("Apple", "Red", 2)));
			items.add(new Item<>(new Fruit("Banana", "Yellow", 5)));
			items.add(new Item<>(new Fruit("Orange", "Orange", 4)));
			items.add(new Item<>(new Fruit("Melon", "Green", 6)));
			items.add(new Item<>(new Fruit("Grape", "Green", 12)));
			
			
			tableView.getItems().addAll(items);
			
			Button btnRemove = new Button("Remove Item");
			
			btnRemove.setOnAction(e -> 
			{    
				Item<?> selectedItem = tableView.getSelectionModel().getSelectedItem();
				
				if (selectedItem != null) 
				{
					items.remove(selectedItem);
					tableView.getItems().remove(selectedItem);
				}
			});
			
			VBox vBox = new VBox(10);
			vBox.setAlignment(Pos.CENTER);
			VBox.setMargin(btnRemove, new Insets(5));
			vBox.getChildren().addAll(tableView, btnRemove);
			
			pane.setCenter(vBox);
			Scene scene = new Scene(pane, 300, 250);
			primaryStage.setScene(scene);
			primaryStage.setTitle("My GUI");
			primaryStage.show();
		}
		
		private void createDynamicColumns(TableView<Item<?>> tableView, Class<?> itemType) 
		{
			Field[] fields = itemType.getDeclaredFields(); 

			for (Field field : fields) 
			{
				field.setAccessible(true); 
				
				TableColumn<Item<?>, String> column = new TableColumn<>(field.getName());

				column.setCellValueFactory(cellData -> 
				{
				
					try {
						Object data = cellData.getValue().getData();
						Object value = field.get(data);
						return new SimpleStringProperty(value.toString());
					} catch (IllegalAccessException e) {
						e.printStackTrace();
					}
					return null;
				});

				tableView.getColumns().add(column);
			}
		}
		
		public static void main(String[] args) 
		{
			launch(args);
			
		}

	}


```

The above code can take any `.class` to extract the column names and values using Field reflections in Java.