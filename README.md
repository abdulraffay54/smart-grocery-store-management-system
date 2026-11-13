# Smart Grocery Store Management System

A menu-driven Python application that runs in the terminal. It lets a grocery store
employee add products, browse and search the catalog, update stock, record customer sales, view sales
history, and generate a store report — all from a single interactive menu.

The project demonstrates core Python basics: variables, lists, dictionaries, functions, loops,
conditionals, string handling, and input validation. It does not use files or a database, so all data
lives in memory and is cleared when the program exits.

---

## 1. Project Title and Overview

**Smart Grocery Store Management System**

The program simulates the basic operations of a small grocery store. Products are stored as
dictionaries inside a list, and completed sales are stored in a separate list. A `while` loop keeps
showing the main menu until the user chooses to exit.

Main capabilities:

- Add new products with a unique ID, name, category, price, and stock quantity.
- View all products in the catalog.
- Search for a product by ID or by name (case-insensitive).
- Add to existing stock or replace the current stock quantity.
- Process a sale, calculate the total amount, and reduce stock.
- View all completed sales records.
- Generate a report with totals, low-stock items, and highest/lowest priced products.

---

## 2. Description of the Python Program

The repository contains a single Python program: [`smart_store_management.py`](smart_store_management.py).

The file has three logical parts:

### 2.1 Setup

```python
products = []
sales_records = []
```

- `products` holds one dictionary per product with the keys `id`, `name`, `category`, `price`, and `stock`.
- `sales_records` holds one dictionary per sale with the keys `id`, `name`, `quantity`, and `total`.

### 2.2 Functions

| Function | Purpose |
| --- | --- |
| `add_product()` | Prompts for product details, rejects duplicate IDs, validates price and stock, and appends a new product dictionary. |
| `view_products()` | Prints every product, or a message if the catalog is empty. |
| `search_product()` | Finds products by exact ID or case-insensitive name and prints the matches. |
| `update_stock()` | Finds a product by ID and either adds stock or sets a new stock quantity. |
| `process_sale()` | Finds a product, validates the quantity against available stock, calculates the total, reduces stock, and saves a sales record. |
| `view_sales()` | Prints every completed sale, or a message if there are none. |
| `generate_report()` | Displays total products, total stock, number of transactions, total revenue, low-stock products (below 5 units), and the highest/lowest priced products. |

### 2.3 Main Menu Loop

After the functions are defined, a `while True` loop displays the menu:

```text
1. Add New Product
2. View All Products
3. Search Product
4. Update Product Stock
5. Process Customer Sale
6. View Sales Records
7. Generate Store Report
8. Exit
```

The user's choice is read with `input()` and compared against strings `"1"` through `"8"` using
`if`/`elif`/`else`. Option `8` prints a farewell message and exits the loop with `break`. Any other
value prints an invalid-choice message and shows the menu again.

---

## 3. Python Concepts and Functions Used

**Data structures**

- **Lists** — `products` and `sales_records` store multiple records; `.append()` adds new items.
- **Dictionaries** — each product and sale is a dictionary accessed with keys such as `product["price"]`.
- **List of dictionaries** — the main pattern used to model records.
- **`len()`** — checks whether the lists are empty and counts products/transactions.

**Functions**

- Defining functions with `def`, calling them from the menu, and using `return` to exit early
  (for example, when a duplicate product ID is found).

**Control flow**

- `if` / `elif` / `else` for menu choices and validation.
- `while True` with `break` for the main menu and for repeated validation prompts.
- `for` loops to iterate over products and sales records.
- `max()` and `min()` with a generator expression to find the highest and lowest prices.

**Input and output**

- `input()` to read user input and `print()` to display output.
- `int()` and `float()` to convert text input into numbers.
- `print("=" * 45)` to repeat a string and create a visual separator.

**String methods**

- `.isdigit()` — confirms that stock and quantity are whole numbers.
- `.replace(".", "", 1)` — allows a single decimal point when validating prices.
- `.strip()` — removes extra spaces from search input.
- `.lower()` — makes product-name searches case-insensitive.

**Validation and business logic**

- Duplicate product ID detection.
- Price and stock validation with retry loops.
- Stock availability check before a sale.
- Revenue calculation: `quantity * product["price"]`.
- Stock deduction: `product["stock"] - quantity`.
- Low-stock detection: `product["stock"] < 5`.

---

## 4. Instructions for Running the Program

### Requirements

- Python 3.x installed (`python --version` should work).
- No third-party packages are required.

### Steps

1. Open a terminal in the project folder:

   ```bash
   cd smart-grocery-store-management-system
   ```

2. Run the program:

   ```bash
   python smart_store_management.py
   ```

   On some systems use:

   ```bash
   python3 smart_store_management.py
   ```

3. Type a menu number (`1`–`8`) and press **Enter**.
4. Follow the prompts. Enter `8` to exit.

> **Note:** Data is stored in memory only. Closing the program discards all products and sales.

---

## 5. Sample Input and Output

The menu is reprinted after every action. The transcript below is shortened by removing repeated menu
blocks for readability.

**Input sequence used:** add product → view products → search → sell 3 units → view sales → report → exit.

```text
=============================================
       SMART GROCERY STORE SYSTEM
=============================================

========== MAIN MENU ==========
1. Add New Product
2. View All Products
3. Search Product
4. Update Product Stock
5. Process Customer Sale
6. View Sales Records
7. Generate Store Report
8. Exit

Enter your choice: 1

----- Add New Product -----
Enter product ID: 101
Enter product name: Rice
Enter product category: Grains
Enter product price: 250.50
Enter available stock: 20

Product added successfully!

Enter your choice: 2

----- Available Products -----

Product ID: 101
Product Name: Rice
Category: Grains
Price: Rs. 250.5
Available Stock: 20

Enter your choice: 3

----- Search Product -----
Enter product name or ID: rice

Product Found!
Product ID: 101
Product Name: Rice
Category: Grains
Price: Rs. 250.5
Available Stock: 20

Enter your choice: 5

----- Process Customer Sale -----
Enter product ID: 101
Product Name: Rice
Available Stock: 20
Price: Rs. 250.5
Enter purchase quantity: 3

Sale completed successfully!
Product: Rice
Quantity Sold: 3
Total Amount: Rs. 751.5
Remaining Stock: 17

Enter your choice: 6

----- Sales Records -----

Product ID: 101
Product Name: Rice
Quantity Sold: 3
Total Amount: Rs. 751.5

Enter your choice: 7

========== STORE REPORT ==========
Total Products: 1
Total Available Stock: 17
Total Sales Transactions: 1
Total Revenue: Rs. 751.5

Products with Low Stock:
No products with low stock.

Product with Highest Price:
Rice - Rs. 250.5

Product with Lowest Price:
Rice - Rs. 250.5
==================================

Enter your choice: 8

Thank you for using Smart Grocery Store System!
```

---

## 6. Test Cases

| # | Scenario | Input | Expected Output |
| --- | --- | --- | --- |
| 1 | Add a valid product | ID `101`, name `Rice`, category `Grains`, price `250.50`, stock `20` | `Product added successfully!` and the product appears in **View All Products**. |
| 2 | Add a duplicate product ID | Add `101` again | `Product ID already exists!` and the catalog is unchanged. |
| 3 | Invalid price | Price `abc` or `12.5.5` | `Invalid price! Enter a valid number.` and the prompt repeats. |
| 4 | Invalid stock | Stock `-5` or `ten` | `Invalid stock! Enter a whole number.` and the prompt repeats. |
| 5 | View an empty catalog | Choose `2` before adding anything | `No products available.` |
| 6 | Search by exact ID | Search `101` | Product details are printed. |
| 7 | Search by name, different case | Search `RICE` | Product details are printed (case-insensitive match). |
| 8 | Search for a missing product | Search `Sugar` | `Product not found.` |
| 9 | Add stock | Choose `4`, ID `101`, option `1`, quantity `5` | Stock increases by 5 and `Updated Stock:` is shown. |
| 10 | Set new stock | Choose `4`, ID `101`, option `2`, quantity `50` | Stock becomes 50. |
| 11 | Invalid update option | Choose `4`, ID `101`, option `9` | `Invalid choice!` |
| 12 | Update a missing product | Choose `4`, ID `999` | `Product not found.` |
| 13 | Successful sale | Choose `5`, ID `101`, quantity `3` | Total is calculated, stock is reduced, and the sale is saved. |
| 14 | Sale with insufficient stock | Quantity greater than available stock | `Insufficient stock!` plus the available stock; no sale is recorded. |
| 15 | Invalid sale quantity | Quantity `abc` | `Invalid quantity! Enter numbers only.` |
| 16 | Sale of a missing product | ID `999` | `Product not found.` |
| 17 | View sales with no records | Choose `6` before any sale | `No sales records available.` |
| 18 | Report totals | Add products and make sales, then choose `7` | Correct product count, total stock, transaction count, and revenue. |
| 19 | Low-stock detection | Product stock below `5` | Product is listed under `Products with Low Stock`. |
| 20 | Highest/lowest price | Add products with different prices, then choose `7` | Correct highest and lowest priced products are shown (all ties are listed). |
| 21 | Empty report | Choose `7` without products | Totals are `0`, low stock says none, and price comparison says no products are available. |
| 22 | Invalid menu choice | Enter `0` or `abc` | `Invalid choice! Please select between 1 and 8.` |
| 23 | Exit the program | Enter `8` | `Thank you for using Smart Grocery Store System!` and the program ends. |
