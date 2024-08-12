# ds-mini-project
Mini Project : Online Grocery Shopping App 
Feature Implemented : 
• Adding Products to the cart 
• Removing Products from the cart 
• Checkout and total Bill 

Source Code : 
import java.util.*; 
 
class Item { 
    public String name; 
    public double price; 
    public int quantity; 
 
    public Item(String name, double price) { 
        this.name = name; 
        this.price = price; 
        this.quantity = 1; 
    } 
 
    public void incrementQuantity() { 
        quantity++; 
    } 
 
    public void decrementQuantity() { 
        if(quantity == 1) { 
 
        } 
        if (quantity > 1) { 
            quantity--; 
        } 
    } 
 
    public String toString() { 
        return name + " - Rs " + price + " x " + quantity + " 
= " + price * quantity + " Rs "; 
    } 
} 
 
class GroceryCategory { 
    private String categoryName; 
 
    //list of existing items 
    LinkedList<Item> items = new LinkedList<>(); 
 
    public GroceryCategory(String categoryName) { 
        this.categoryName = categoryName; 
    } 
 
    public void addItem(Item item) { 
        for (Item existingItem : items) { 
            if (existingItem.name.equals(item.name)) { 
                existingItem.incrementQuantity(); 
                return; 
            } 
        } 
        items.add(item); 
    } 
 
    public void removeItem(Item item) { 
        items.remove(item); 
    } 
 
    public LinkedList<Item> getItems() { 
        return items; 
    } 
 
    public String getCategoryName() { 
        return categoryName; 
    } 
} 
 
class ShoppingCart { 
    //items in the cart 
    private LinkedList<Item> cartItems = new LinkedList<>(); 
 
    public void addItem(Item item) { 
        for (Item cartItem : cartItems) { 
            if (cartItem.name.equals(item.name)) { 
                cartItem.incrementQuantity(); 
                return; 
            } 
        } 
        cartItems.add(item); 
    } 
 
    public void removeItem(Item item) { 
        cartItems.remove(item); 
    } 
 
    public double calculateTotal() { 
        double total = 0.0; 
        for (Item item : cartItems) { 
            total += item.price * item.quantity; 
        } 
        return total; 
    } 
 
    public void displayCart() { 
        for (Item item : cartItems) { 
            System.out.println(item); 
        } 
    } 
 
    public LinkedList<Item> getCart(){ 
        return cartItems; 
    } 
} 
 
public class GroceryShoppingApp { 
    public static Scanner scanner = new Scanner(System.in); 
    public static void main(String[] args) { 
 
        GroceryCategory fruits = new 
GroceryCategory("Fruits"); 
        GroceryCategory vegetables = new 
GroceryCategory("Vegetables"); 
        GroceryCategory grains = new 
GroceryCategory("Grains"); 
        GroceryCategory bakeryProducts = new 
GroceryCategory("Bakery Products"); 
        GroceryCategory snacks = new 
GroceryCategory("Snacks"); 
 
 
        Item apple = new Item("Apple", 20); 
        Item banana = new Item("Banana", 10); 
        Item orange = new Item("Orange", 15); 
        Item brinjal = new Item("Brinjal", 40); 
        Item ladyFinger = new Item("Lady Finger", 35); 
        Item potato = new Item("Potato", 50); 
        Item wheat = new Item("Wheat", 30); 
        Item jawar = new Item("Jawar", 40); 
        Item bajra = new Item("Bajra", 35); 
        Item donuts = new Item("Donuts", 60); 
        Item khari = new Item("Khari", 80); 
        Item pastry = new Item("Pastry", 30); 
        Item kurkure = new Item("Kurkure", 30); 
        Item bourbon = new Item("Bourbon", 40); 
        Item bananaChips = new Item("Banana Chips", 30); 
 
        fruits.addItem(apple); 
        fruits.addItem(banana); 
        fruits.addItem(orange); 
        vegetables.addItem(brinjal); 
        vegetables.addItem(potato); 
        vegetables.addItem(ladyFinger); 
        grains.addItem(wheat); 
        grains.addItem(bajra); 
        grains.addItem(jawar); 
        snacks.addItem(bourbon); 
        snacks.addItem(kurkure); 
        snacks.addItem(bananaChips); 
        bakeryProducts.addItem(khari); 
        bakeryProducts.addItem(pastry); 
        bakeryProducts.addItem(donuts); 
 
        ShoppingCart cart = new ShoppingCart(); 
        int n = 1; 
        while (n==1) { 
            System.out.println("Select a category to view 
items (1-5):"); 
            System.out.println("1. Fruits"); 
            System.out.println("2. Vegetables"); 
            System.out.println("3. Grains"); 
            System.out.println("4. Bakery Products"); 
            System.out.println("5. Snacks"); 
            System.out.println("6. Remove item"); 
            System.out.println("7. View Cart"); 
            System.out.println("8. Checkout"); 
 
            int choice = scanner.nextInt(); 
 
            switch (choice) { 
                case 1: 
                    displayCategory(fruits, cart); 
                    break; 
 
                case 2: 
                    displayCategory(vegetables, cart); 
                    break; 
 
                case 3: 
                    displayCategory(grains, cart); 
                    break; 
 
                case 4: 
                    displayCategory(bakeryProducts, cart); 
                    break; 
 
                case 5: 
                    displayCategory(snacks, cart); 
                    break; 
 
                case 6: 
                    remove(cart); 
                    break; 
 
                case 7: 
                    System.out.println("Items in the cart:"); 
                    cart.displayCart(); 
                    break; 
 
                case 8: 
                    double total = cart.calculateTotal(); 
                    System.out.println("Total amount: Rs " + 
total); 
                    n = 0; 
                    break; 
 
                default: 
                    System.out.println("Please enter valid 
choice !!!"); 
                    break; 
            } 
        } 
    } 
 
    public static void displayCategory(GroceryCategory 
category, ShoppingCart cart) { 
        System.out.println("Category: " + 
category.getCategoryName()); 
        LinkedList<Item> items = category.getItems(); 
        for (int i = 0; i < items.size(); i++) { 
            System.out.println((i + 1) + ". " + items.get(i)); 
        } 
 
        System.out.println("Select an item to add to the cart 
(1-" + items.size() + "):"); 
        int choice = scanner.nextInt(); 
 
        if (choice >= 1 && choice <= items.size()) { 
            Item selectedItem = items.get(choice - 1); 
            cart.addItem(selectedItem); 
            System.out.println("Added " + selectedItem.name + 
" to the cart."); 
        } 
    } 
 
    public static void remove(ShoppingCart cart) { 
        cart.displayCart(); 
        System.out.print("Which Product do you want to remove 
: "); 
        String str = scanner.nextLine(); 
        String productName = scanner.nextLine(); 
 
        for (Item cartItem : cart.getCart()) { 
            if (productName.equals(cartItem.name)) { 
 
                if(cartItem.quantity == 1){ 
                    cart.removeItem(cartItem); 
                } else { 
                    cartItem.decrementQuantity(); 
                } 
 
                System.out.println(productName+" is removed 
successfully !!!"); 
                return;  // Exit the loop once the item is 
removed 
            } 
        } 
        System.out.println("Product not found in the cart."); 
    } 
} 
 
/* 
OUTPUT 
Select a category to view items (1-5): 
1. Fruits 
2. Vegetables 
3. Grains 
4. Bakery Products 
5. Snacks 
6. Remove item 
7. View Cart 
8. Checkout 
1 
Category: Fruits 
1. Apple - Rs 20.0 x 1 = 20.0 Rs 
2. Banana - Rs 10.0 x 1 = 10.0 Rs 
3. Orange - Rs 15.0 x 1 = 15.0 Rs 
Select an item to add to the cart (1-3): 
1 
Added Apple to the cart. 
Select a category to view items (1-5): 
1. Fruits 
2. Vegetables 
3. Grains 
4. Bakery Products 
5. Snacks 
6. Remove item 
7. View Cart 
8. Checkout 
2 
Category: Vegetables 
1. Brinjal - Rs 40.0 x 1 = 40.0 Rs 
2. Potato - Rs 50.0 x 1 = 50.0 Rs 
3. Lady Finger - Rs 35.0 x 1 = 35.0 Rs 
Select an item to add to the cart (1-3): 
3 
Added Lady Finger to the cart. 
Select a category to view items (1-5): 
1. Fruits 
2. Vegetables 
3. Grains 
4. Bakery Products 
5. Snacks 
6. Remove item 
7. View Cart 
8. Checkout 
3 
Category: Grains 
1. Wheat - Rs 30.0 x 1 = 30.0 Rs 
2. Bajra - Rs 35.0 x 1 = 35.0 Rs 
3. Jawar - Rs 40.0 x 1 = 40.0 Rs 
Select an item to add to the cart (1-3): 
1 
Added Wheat to the cart. 
Select a category to view items (1-5): 
1. Fruits 
2. Vegetables 
3. Grains 
4. Bakery Products 
5. Snacks 
6. Remove item 
7. View Cart 
8. Checkout 
4 
Category: Bakery Products 
1. Khari - Rs 80.0 x 1 = 80.0 Rs 
2. Pastry - Rs 30.0 x 1 = 30.0 Rs 
3. Donuts - Rs 60.0 x 1 = 60.0 Rs 
Select an item to add to the cart (1-3): 
3 
Added Donuts to the cart. 
Select a category to view items (1-5): 
1. Fruits 
2. Vegetables 
3. Grains 
4. Bakery Products 
5. Snacks 
6. Remove item 
7. View Cart 
8. Checkout 
5 
Category: Snacks 
1. Bourbon - Rs 40.0 x 1 = 40.0 Rs 
2. Kurkure - Rs 30.0 x 1 = 30.0 Rs 
3. Banana Chips - Rs 30.0 x 1 = 30.0 Rs 
Select an item to add to the cart (1-3): 
2 
Added Kurkure to the cart. 
Select a category to view items (1-5): 
1. Fruits 
2. Vegetables 
3. Grains 
4. Bakery Products 
5. Snacks 
6. Remove item 
7. View Cart 
8. Checkout 
4 
Category: Bakery Products 
1. Khari - Rs 80.0 x 1 = 80.0 Rs 
2. Pastry - Rs 30.0 x 1 = 30.0 Rs 
3. Donuts - Rs 60.0 x 1 = 60.0 Rs 
Select an item to add to the cart (1-3): 
3 
Added Donuts to the cart. 
Select a category to view items (1-5): 
1. Fruits 
2. Vegetables 
3. Grains 
4. Bakery Products 
5. Snacks 
6. Remove item 
7. View Cart 
8. Checkout 
6 
Apple - Rs 20.0 x 1 = 20.0 Rs 
Lady Finger - Rs 35.0 x 1 = 35.0 Rs 
Wheat - Rs 30.0 x 1 = 30.0 Rs 
Donuts - Rs 60.0 x 2 = 120.0 Rs 
Kurkure - Rs 30.0 x 1 = 30.0 Rs 
Which product do you want to remove : Donuts 
Donuts is removed successfully !!! 
Select a category to view items (1-5): 
1. Fruits 
2. Vegetables 
3. Grains 
4. Bakery Products 
5. Snacks 
6. Remove item 
7. View Cart 
8. Checkout 
7 
Items in the cart: 
Apple - Rs 20.0 x 1 = 20.0 Rs 
Lady Finger - Rs 35.0 x 1 = 35.0 Rs 
Wheat - Rs 30.0 x 1 = 30.0 Rs 
Donuts - Rs 60.0 x 1 = 60.0 Rs 
Kurkure - Rs 30.0 x 1 = 30.0 Rs 
Select a category to view items (1-5): 
1. Fruits 
2. Vegetables 
3. Grains 
4. Bakery Products 
5. Snacks 
6. Remove item 
7. View Cart 
8. Checkout 
8 
Total amount: Rs 175.0 
Process finished with exit code 0 
*/ 
