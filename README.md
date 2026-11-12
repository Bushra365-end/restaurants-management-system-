# restaurants-management-system-

1. Introduction
Small restaurants often keep track of their menu, customer orders, stock and staff on paper or in scattered spreadsheets. This makes it slow to find information and easy to make mistakes. The Restaurant Management System is a desktop application written in Java using the Swing GUI toolkit. It brings four everyday restaurant tasks into one tabbed window: menu management, order management, inventory management and staff management.
The project is also an exercise in object-oriented programming. It uses an abstract base class, an interface, inheritance, polymorphism and encapsulation, and separates the code into model, logic and user-interface layers.
2. Objectives
• Provide one application where restaurant staff can add, view, update, delete and search records.
• Calculate order totals automatically from menu prices and quantities.
• Prevent common input mistakes through validation and clear error messages.
• Demonstrate core OOP principles in a realistic, working project.
3. Scope
Included
• Four modules: Menu, Order, Inventory and Staff.
• Create, read, update, delete (CRUD) and search for each module.
• Input validation, confirmation before delete, and pre-loaded sample data.
Not included (in the current version)
• Permanent storage (database or files).
• User login and roles.
• Printing of bills or reports.
• Automatic link between orders and stock levels.
4. Tools and Technologies
Item
Details
Programming language
Java (JDK 8 or later)
GUI library
Swing (javax.swing, java.awt)
Look and feel
Nimbus, with custom fonts and colours
Data storage
In-memory ArrayList collections
Development environment
IntelliJ IDEA
5. System Design
5.1 Architecture
The application is split into three layers.
Layer
Classes
Responsibility
Model
RestaurantEntity, MenuItem, Order, InventoryItem, Staff
Hold the data of one record and expose it through getters and setters.
Logic / data access
MenuManager, OrderManager, InventoryManager, StaffManager, RestaurantData
Add, update, delete and search records in the shared lists.
User interface
Main, MenuPanel, OrderPanel, InventoryPanel, StaffPanel
Draw the forms and tables, read user input, validate it and call the managers.
Main creates the main window, applies the Nimbus look and feel, and places the four panels in tabs. RestaurantData holds one static list per record type, and every manager works on those shared lists.
5.2 Class Descriptions
Class
Description
RestaurantEntity
Abstract base class. Stores the record id and declares the abstract method getDetails().
Manageable
Interface with addRecord(), updateRecord(), deleteRecord() and searchRecord().
MenuItem
Name, category, price and availability.
Order
Customer, item summary, total quantity and total price.
InventoryItem
Name, category, quantity, unit and stock status.
Staff
Name, role, phone number and shift.
*Manager classes
Provide add, getAll, update, delete and a search method (by name, or by customer for orders).
*Panel classes
Swing panels that implement Manageable and build the module screen.
RestaurantData
Static store of all lists, filled with sample records when the program starts.
5.3 Class Relationships
• MenuItem, Order, InventoryItem and Staff each extend RestaurantEntity.
• MenuPanel, OrderPanel, InventoryPanel and StaffPanel each implement Manageable.
• Each panel uses its own manager, and each manager works on lists inside RestaurantData.
• OrderPanel also reads RestaurantData.menuItems directly to fill its menu drop-down.
5.4 OOP Concepts Applied
Concept
How it is applied
Abstraction
RestaurantEntity and Manageable define what a record and a manageable screen must provide, without saying how.
Inheritance
The four model classes reuse the id field and its getter and setter from RestaurantEntity.
Polymorphism
Every model overrides getDetails(), and every panel gives its own implementation of the Manageable methods.
Encapsulation
All fields are private and accessed through public getters and setters.
Constructor chaining
Default constructors call the full constructors with this(...), and subclasses call super(id).
6. Module Description
Every module screen has the same layout: a coloured header, a form card on the left with Add, Update, Delete and Clear buttons, and a table card on the right with a search box. Clicking a row loads it into the form. The Enter key moves the cursor to the next field.
6.1 Menu Management
Field
Input type
Rules
Menu ID
Text
Required, whole number greater than 0
Item Name
Text
Required
Category
Drop-down
Main Course, Drinks, Dessert, Snacks
Price
Text
Required, number greater than 0 (shown in BDT)
Availability
Check box
Items marked unavailable cannot be ordered
Search is by item name (case-insensitive, exact match). The found row is selected and scrolled into view.
6.2 Order Management
An order is built from one or more menu lines:
1. Enter the Order ID and customer name.
2. Pick an available menu item and a quantity from 1 to 100.
3. Click Add Item. The line (for example Chicken Burger x 2 = BDT 700.00) is added to the order list and the Total Bill is updated.
4. Select a line and click Remove Item to take it out. The total is reduced accordingly.
5. Click Add Order to save the order.
The drop-down lists only menu items that are marked available. The Refresh Menu button reloads it after changes in the Menu tab. Search is by customer name.
6.3 Inventory Management
Field
Input type
Rules
Inventory ID
Text
Required, whole number greater than 0
Item Name
Text
Required
Category
Drop-down
Dry Goods, Meat, Vegetables, Drinks, Other
Quantity
Text
Required, whole number, cannot be negative
Unit
Radio buttons
pcs, kg, L, bottles
Stock Status
Radio buttons
In Stock, Low Stock, Out of Stock
Search is by item name.
6.4 Staff Management
Field
Input type
Rules
Staff ID
Text
Required, whole number greater than 0
Staff Name
Text
Required
Role
Drop-down
Manager, Chef, Waiter, Cashier
Phone Number
Text
Required (format is not checked)
Shift
Drop-down
Morning, Evening, Night
Search is by staff name.
7. Implementation Highlights
7.1 Validation
Before saving, each panel checks that the required fields are filled. It then converts the numeric fields and checks their values (for example, price greater than 0 or quantity not negative). A NumberFormatException is caught and shown as a friendly error dialog, so the program does not crash on wrong input.
7.2 Order Total Calculation
When a line is added, its total is price × quantity. The panel keeps a running total and a running quantity. When a line is removed, its values are read back from the line text and subtracted. The total is shown with two decimal places.
7.3 Table and Data Synchronisation
Each panel keeps a DefaultTableModel (what the user sees) and a list in RestaurantData (the actual data). Add, update and delete change both, using the selected table row as the list index. Cells are not directly editable, so all changes go through the form.
7.4 User Experience
The interface uses colour-coded headers (green for Menu, blue for Orders, orange for Inventory, purple for Staff), a consistent layout, confirmation before deleting, and a success message after updates.
8. Sample Data
The program starts with sample records so every table has content on first launch.
Module
Records
Menu
Chicken Burger (350.00), Lemonade (120.00, unavailable), Chocolate Cake (220.00), Chicken Fry (180.00), Hazelnut Latte (500.00)
Orders
1001 Ayesha (700.00), 1002 Rahim (220.00), 1003 Karim (500.00)
Inventory
Chicken Breast (40 kg), Rice (25 kg), Cola (6 bottles, Low Stock)
Staff
Nusrat Jahan (Manager, Morning), Rakib Hasan (Chef, Evening), Sadia Akter (Cashier, Night)
9. How to Run
Requirement: JDK 8 or later.
javac *.java
java Main
Alternatively, open the project in IntelliJ IDEA, mark the RestaurantManagementSystem folder as the source root, and run the Main class.
10. Test Scenarios
The table below lists scenarios to verify the program. Expected results are taken from the program code; fill in the last column after running them.
No.
Scenario
Expected result
Actual result
1
Add a menu item with empty name
Validation dialog: ID, Name and Price are required

2
Add a menu item with price abc
Error dialog: ID and Price must be valid numbers

3
Add a menu item with price 0
Dialog: ID and Price must be greater than zero

4
Mark a menu item unavailable, click Refresh Menu in Orders
Item no longer appears in the drop-down

5
Add 2 × Chicken Burger and 1 × Hazelnut Latte to an order
Total shows BDT 1200.00

6
Remove the Hazelnut Latte line
Total drops to BDT 700.00

7
Add an order with no items
Dialog: add at least one menu item

8
Add an inventory item with quantity -5
Dialog: quantity cannot be negative

9
Select a staff row and click Delete, then confirm
Row removed from table and list

10
Search for a name that does not exist
"not found" dialog

11
Search for an existing name in a different letter case
Matching row is selected

11. Limitations
• No permanent storage. All changes are lost when the program is closed.
• No duplicate-ID check. The same ID can be used twice in a module.
• Stock status is manual and not linked to quantity or to orders.
• Order lines are stored as text in one string, so item names containing x or ; could cause problems when an order is edited.
• The Order menu list needs manual refresh after menu changes.
• Search shows only the first exact match, with no partial search or filter.
• Phone numbers are not checked for format.
12. Future Work
• Store data in files (CSV or JSON) or a database through JDBC.
• Reject duplicate IDs or generate IDs automatically.
• Replace the order text string with a proper OrderLine class.
• Reduce stock automatically when an order is placed, and set stock status from quantity.
• Add partial-match search, sorting and filtering.
• Add reports such as daily sales, low-stock list and staff schedule.
• Add login with roles, and print or export bills.
• Organise the code into packages (model, manager, ui) and add unit tests.
13. Conclusion
The Restaurant Management System meets its main goal of putting menu, order, inventory and staff records into one easy-to-use desktop application. Its consistent interface, input validation and automatic order totals make routine work simpler. The code also shows how abstraction, inheritance, polymorphism and encapsulation can be combined in a practical project. The main next steps are permanent storage and links between modules, which would turn the current prototype into a more complete tool for a real restaurant.
