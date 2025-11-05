# FX Collections II

## TableView
A TableView is a UI component in JavaFX that displays data in a tabular format.

Fruit.java
	
```java
	
	package com.cmu;

	public class Fruit
	{
		private String name;
		private String color;
		private int quantity;
		private boolean selected;
		
		public Fruit(String name, String color, int quantity) 
		{
			this.name = name;
			this.color = color;
			this.quantity = quantity;
			this.selected = false;
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
		public void setQuantity(int quantity) {
			this.quantity = quantity;
		}
		
		public boolean isSelected() {
			return selected;
		}

		public void setSelected(boolean selected) {
			this.selected = selected;
		}
	}
	
```


MyGUI.java
```java

	package com.cmu;

	import java.util.ArrayList;

	import javafx.application.Application;
	import javafx.collections.FXCollections;
	import javafx.collections.ObservableList;
	import javafx.scene.Scene;
	import javafx.scene.control.TableColumn;
	import javafx.scene.control.TableView;
	import javafx.scene.control.cell.PropertyValueFactory;
	import javafx.scene.layout.BorderPane;
	import javafx.stage.Stage;


	public class MyGUI extends Application 
	{

		@Override
		public void start(Stage primaryStage) throws Exception 
		{

			BorderPane pane = new BorderPane();
			
			TableView<Fruit> tableView = new TableView<>();
			
			TableColumn<Fruit, String> colName = new TableColumn<>("Name");
			colName.setCellValueFactory(new PropertyValueFactory<>("name"));
			
			TableColumn<Fruit, String> colColor = new TableColumn<>("Color");
			colColor.setCellValueFactory(new PropertyValueFactory<>("color"));
			
			TableColumn<Fruit, Integer> colQuantity = new TableColumn<>("Quantity");
			colQuantity.setCellValueFactory(new PropertyValueFactory<>("quantity"));
			
			colName.setPrefWidth(100);
			colColor.setPrefWidth(100);
			colQuantity.setPrefWidth(100);
			
			tableView.getColumns().addAll(colName, colColor, colQuantity);
			
			ObservableList<Fruit> fruits = FXCollections.observableArrayList(
					new Fruit("Apple", "Red", 2),
					new Fruit("Banana", "Yellow", 6),
					new Fruit("Grape", "Green", 10)
					);
			
			tableView.setItems(fruits);
			
			pane.setCenter(tableView);

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
`TableView` are very handy as they allow editing of its rows as well. We need to set the `setEditable` to `true` and then set the column for editing

```java
	@Override
	public void start(Stage primaryStage) throws Exception 
	{

		BorderPane pane = new BorderPane();
		
		TableView<Fruit> tableView = new TableView<>();
		tableView.setEditable(true);
		
		TableColumn<Fruit, String> colName = new TableColumn<>("Name");
		colName.setCellValueFactory(new PropertyValueFactory<>("name"));
		colName.setCellFactory(TextFieldTableCell.forTableColumn());
		colName.setOnEditCommit(e -> {
			Fruit fruit = e.getRowValue();
			fruit.setName(e.getNewValue());
		});
		
		TableColumn<Fruit, String> colColor = new TableColumn<>("Color");
		colColor.setCellValueFactory(new PropertyValueFactory<>("color"));
		
		TableColumn<Fruit, Integer> colQuantity = new TableColumn<>("Quantity");
		colQuantity.setCellValueFactory(new PropertyValueFactory<>("quantity"));
		
		colName.setPrefWidth(100);
        colColor.setPrefWidth(100);
        colQuantity.setPrefWidth(100);
        	
		tableView.getColumns().addAll(colName, colColor, colQuantity);
		
		ObservableList<Fruit> fruits = FXCollections.observableArrayList(
				new Fruit("Apple", "Red", 2),
				new Fruit("Banana", "Yellow", 6),
				new Fruit("Grape", "Green", 10)
				);
		
		tableView.setItems(fruits);
		
		pane.setCenter(tableView);

		Scene scene = new Scene(pane, 305, 200);

		primaryStage.setTitle("My GUI");
		primaryStage.setScene(scene);
		primaryStage.show();

	}

```
Let's perform some more operations on the button clicks on TableView

```Java
	@Override
	public void start(Stage primaryStage) throws Exception 
	{

		BorderPane pane = new BorderPane();
		
		TableView<Fruit> tableView = new TableView<>();
		tableView.setEditable(true);
		
		TableColumn<Fruit, String> colName = new TableColumn<>("Name");
		colName.setCellValueFactory(new PropertyValueFactory<>("name"));
		colName.setCellFactory(TextFieldTableCell.forTableColumn());
		colName.setOnEditCommit(e -> {
            Fruit fruit = e.getRowValue();
            String newName = e.getNewValue();
            fruit.setName(newName);
        });
		
		TableColumn<Fruit, String> colColor = new TableColumn<>("Color");
		colColor.setCellValueFactory(new PropertyValueFactory<>("color"));
		colColor.setCellFactory(TextFieldTableCell.forTableColumn());
		colColor.setOnEditCommit(e -> {
            Fruit fruit = e.getRowValue();
            String newColor = e.getNewValue();
            fruit.setColor(newColor);
        });
		
		TableColumn<Fruit, Integer> colQuantity = new TableColumn<>("Quantity");
		colQuantity.setCellValueFactory(new PropertyValueFactory<>("quantity"));
		colQuantity.setCellFactory(TextFieldTableCell.forTableColumn(new IntegerStringConverter()));
		colQuantity.setOnEditCommit(e -> {
            Fruit fruit = e.getRowValue();
            int newQuantity= e.getNewValue();
            fruit.setQuantity(newQuantity);
        });
		
		colName.setPrefWidth(100);
        colColor.setPrefWidth(100);
        colQuantity.setPrefWidth(100);
        	
		tableView.getColumns().addAll(colName, colColor, colQuantity);
		
		ObservableList<Fruit> fruits = FXCollections.observableArrayList(
				new Fruit("Apple", "Red", 2),
				new Fruit("Banana", "Yellow", 6),
				new Fruit("Grape", "Green", 10)
				);
		
		tableView.setItems(fruits);
		
		Button btnAdd = new Button("Add Record");
		Button btnDelete = new Button("Delete Record");
		
		btnAdd.setOnAction(e->{
			if (fruits.size() == 0 || !fruits.get(fruits.size() - 1).getName().isEmpty())
			{
				fruits.add(new Fruit("", "", 0));
			}
			
			tableView.scrollTo(fruits.size() - 1);
			tableView.edit(fruits.size() - 1, colName);
		});
		
		btnDelete.setOnAction(e -> {
			Fruit selectedFruit = tableView.getSelectionModel().getSelectedItem();
			if (selectedFruit != null)
			{
				fruits.remove(selectedFruit);
			}
		});
		
		
		
		HBox buttonPane = new HBox(10);
        buttonPane.getChildren().addAll(btnAdd, btnDelete);
        buttonPane.setAlignment(Pos.CENTER);
		
		pane.setCenter(tableView);
		pane.setBottom(buttonPane);

		Scene scene = new Scene(pane, 305, 300);

		primaryStage.setTitle("My GUI");
		primaryStage.setScene(scene);
		primaryStage.show();

	}
```

Individual Cell properties can be changed by setting CellFactory

```java

	colName.setCellFactory(new Callback<TableColumn<Fruit,String>, TableCell<Fruit,String>>() {
				
				@Override
				public TableCell<Fruit, String> call(TableColumn<Fruit, String> param) {
					// TODO Auto-generated method stub
					return new TableCell<Fruit, String>() {
						protected void updateItem(String item, boolean empty)
						{
							super.updateItem(item, empty);
							setText(item);
							setTextFill(Color.RED);
							setAlignment(Pos.CENTER);
						}
					};
				}
			});

```

`TableView` is pretty flexible when it comes to adding other UI controls to it. 

Let's add a checkbox to one of the columns of the TableView:

Fruit.java
	
```java
	
	package com.cmu;

	public class Fruit
	{
		private String name;
		private String color;
		private int quantity;
		private boolean selected;
		
		public Fruit(String name, String color, int quantity) 
		{
			this.name = name;
			this.color = color;
			this.quantity = quantity;
			this.selected = false;
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
		public void setQuantity(int quantity) {
			this.quantity = quantity;
		}
		
		public boolean isSelected() {
			return selected;
		}

		public void setSelected(boolean selected) {
			this.selected = selected;
		}
	}
	
```

MyGUI.java
	
```java
	package com.cmu;

	import java.awt.Checkbox;

	import javafx.application.Application;
	import javafx.collections.FXCollections;
	import javafx.collections.ObservableList;
	import javafx.geometry.Pos;
	import javafx.scene.Scene;
	import javafx.scene.control.Button;
	import javafx.scene.control.CheckBox;
	import javafx.scene.control.TableCell;
	import javafx.scene.control.TableColumn;
	import javafx.scene.control.TableView;
	import javafx.scene.control.cell.PropertyValueFactory;
	import javafx.scene.control.cell.TextFieldTableCell;
	import javafx.scene.layout.BorderPane;
	import javafx.scene.layout.HBox;
	import javafx.scene.paint.Color;
	import javafx.stage.Stage;
	import javafx.util.Callback;
	import javafx.util.converter.IntegerStringConverter;


	public class MyGUI extends Application 
	{
		
		@Override
		public void start(Stage primaryStage) throws Exception 
		{

			BorderPane pane = new BorderPane();
			
			TableView<Fruit> tableView = new TableView<>();
			tableView.setEditable(true);
			
			TableColumn<Fruit, String> colName = new TableColumn<>("Name");
			colName.setCellValueFactory(new PropertyValueFactory<>("name"));
			colName.setCellFactory(TextFieldTableCell.forTableColumn());
			colName.setOnEditCommit(e -> {
				Fruit fruit = e.getRowValue();
				String newName = e.getNewValue();
				fruit.setName(newName);
			});
			colName.setCellFactory(new Callback<TableColumn<Fruit,String>, TableCell<Fruit,String>>() {
				
				@Override
				public TableCell<Fruit, String> call(TableColumn<Fruit, String> param) {
					// TODO Auto-generated method stub
					return new TableCell<Fruit, String>() {
						protected void updateItem(String item, boolean empty)
						{
							super.updateItem(item, empty);
							setText(item);
							setTextFill(Color.RED);
							setAlignment(Pos.CENTER);
						}
					};
				}
			});
			
			TableColumn<Fruit, String> colColor = new TableColumn<>("Color");
			colColor.setCellValueFactory(new PropertyValueFactory<>("color"));
			colColor.setCellFactory(TextFieldTableCell.forTableColumn());
			colColor.setOnEditCommit(e -> {
				Fruit fruit = e.getRowValue();
				String newColor = e.getNewValue();
				fruit.setColor(newColor);
			});
			
			TableColumn<Fruit, Integer> colQuantity = new TableColumn<>("Quantity");
			colQuantity.setCellValueFactory(new PropertyValueFactory<>("quantity"));
			colQuantity.setCellFactory(TextFieldTableCell.forTableColumn(new IntegerStringConverter()));
			colQuantity.setOnEditCommit(e -> {
				Fruit fruit = e.getRowValue();
				int newQuantity= e.getNewValue();
				fruit.setQuantity(newQuantity);
			});
			
			TableColumn<Fruit, Boolean> colSelect = new TableColumn<>("Select");
			colSelect.setCellValueFactory(new PropertyValueFactory<>("selected"));
			colSelect.setCellFactory(new Callback<TableColumn<Fruit,Boolean>, TableCell<Fruit,Boolean>>() {
				
				@Override
				public TableCell<Fruit, Boolean> call(TableColumn<Fruit, Boolean> param) {
					// TODO Auto-generated method stub
					return new TableCell<Fruit, Boolean>() {
						private CheckBox checkBox = new CheckBox();
						
						protected void updateItem(Boolean item, boolean empty)
						{
							if (empty || item == null) {
								setGraphic(null);
							} else {
								checkBox.setSelected(item);
								checkBox.setOnAction(event -> {
									Fruit fruit = getTableView().getItems().get(getIndex());
									fruit.setSelected(checkBox.isSelected());
								});
								setGraphic(checkBox);
							}
						}
					};
				}
			});
			
			colName.setPrefWidth(100);
			colColor.setPrefWidth(100);
			colQuantity.setPrefWidth(100);
				
			tableView.getColumns().addAll(colName, colColor, colQuantity, colSelect);
			
			ObservableList<Fruit> fruits = FXCollections.observableArrayList(
					new Fruit("Apple", "Red", 2),
					new Fruit("Banana", "Yellow", 6),
					new Fruit("Grape", "Green", 10)
					);
			
			tableView.setItems(fruits);
			
			Button btnAdd = new Button("Add Record");
			Button btnDelete = new Button("Delete Record");
			
			btnAdd.setOnAction(e->{
				if (fruits.size() == 0 || !fruits.get(fruits.size() - 1).getName().isEmpty())
				{
					fruits.add(new Fruit("", "", 0));
				}
				
				tableView.scrollTo(fruits.size() - 1);
				tableView.edit(fruits.size() - 1, colName);
			});
			
			btnDelete.setOnAction(e -> {
				Fruit selectedFruit = tableView.getSelectionModel().getSelectedItem();
				if (selectedFruit != null)
				{
					fruits.remove(selectedFruit);
				}
			});
				
			HBox buttonPane = new HBox(10);
			buttonPane.getChildren().addAll(btnAdd, btnDelete);
			buttonPane.setAlignment(Pos.CENTER);
			
			pane.setCenter(tableView);
			pane.setBottom(buttonPane);

			Scene scene = new Scene(pane, 305, 300);

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

