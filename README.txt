RESTAURANT MANAGEMENT SYSTEM

A simple Java Swing desktop application with four main entities:
1. Menu Management
2. Order Management
3. Inventory Management
4. Staff Management

MAIN FEATURES
- Modern card-style Swing layout with color-coded sections and tables
- JTabbedPane with one tab for each entity
- JTable in every entity tab
- Add, Update, Delete, Search and Clear controls in every entity tab
- JOptionPane validation warnings and delete confirmation
- Existing sample records are loaded when the application starts
- Inventory stock status shows "In Stock", "Low Stock" or "Out of Stock"
- Staff Management stores staff name, role, phone number and shift
- Order total is calculated from the selected menu item and quantity
- Enter-key auto-tabbing for data-entry fields only
- Add, Update, Delete, Search and Clear buttons are not part of auto-tabbing

OOP / JAVA CONCEPTS USED
- Encapsulation: private fields with getters/setters
- Inheritance: MenuItem, Order, InventoryItem and Staff extend RestaurantEntity
- Polymorphism: getDetails() is overridden by the child classes
- Abstraction: RestaurantEntity is abstract and Manageable is an interface
- this, super, static, final
- Default and parameterized constructors
- public, private and protected access modifiers
- ArrayList collections
- String formatting and manipulation
- Swing event listeners

HOW TO COMPILE
Open a terminal in the folder that contains the .java files and run:

javac *.java

HOW TO RUN
After compiling, run:

java Main

INTELLIJ IDEA
1. Open the RestaurantManagementSystem project folder.
2. Make sure a Java JDK is selected for the project.
3. Open Main.java.
4. Run Main.main().

CLASS / FILE DESCRIPTION
- Main.java: Creates the JFrame, menu bar and JTabbedPane.
- RestaurantEntity.java: Abstract parent class with the common ID field.
- Manageable.java: Interface for Add, Update, Delete and Search operations.
- RestaurantData.java: Shared ArrayLists and sample starting data.
- MenuItem.java: Model for a menu item.
- MenuManager.java: Menu ArrayList CRUD and search logic.
- MenuPanel.java: Swing form and JTable for Menu Management.
- Order.java: Model for an order.
- OrderManager.java: Order ArrayList CRUD and search logic.
- OrderPanel.java: Swing form and JTable for Order Management.
- InventoryItem.java: Model for an inventory item and stock status.
- InventoryManager.java: Inventory ArrayList CRUD and search logic.
- InventoryPanel.java: Swing form and JTable for Inventory Management.
- Staff.java: Model for a staff member.
- StaffManager.java: Staff ArrayList CRUD and search logic.
- StaffPanel.java: Swing form and JTable for Staff Management.

AUTO-TABBING
Press Enter while filling a record to move to the next required input field.
The last data field does not move focus to a button. Search and CRUD buttons keep their normal behavior.

GROUP MEMBERS AND CONTRIBUTIONS
Replace the placeholders below with the real group member names before submission.
- [Member Name 1]: Menu Management / project integration
- [Member Name 2]: Order Management
- [Member Name 3]: Inventory Management / testing
- [Member Name 4]: Staff Management

Before submission, make sure every member can explain every class and feature.
