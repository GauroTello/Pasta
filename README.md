# Pasta
Shop
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class PastaProduct {
    private String name;
    private double price;

    public PastaProduct(String name, double price) {
        this.name = name;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }
}

class ShoppingCart {
    private List<PastaProduct> items;

    public ShoppingCart() {
        items = new ArrayList<>();
    }

    public void addItem(PastaProduct product) {
        items.add(product);
    }

    public List<PastaProduct> getItems() {
        return items;
    }

    public double calculateTotal() {
        double total = 0;
        for (PastaProduct item : items) {
            total += item.getPrice();
        }
        return total;
    }
}

public class InternetShopPasta {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        PastaProduct product1 = new PastaProduct("Spaghetti", 2.99);
        PastaProduct product2 = new PastaProduct("Fettuccine", 3.49);
        PastaProduct product3 = new PastaProduct("Penne", 2.49);

        List<PastaProduct> availableProducts = new ArrayList<>();
        availableProducts.add(product1);
        availableProducts.add(product2);
        availableProducts.add(product3);

        ShoppingCart cart = new ShoppingCart();

        System.out.println("Welcome to the Pasta Internet Shop!");
        System.out.println("Available Pasta Products:");
        
        for (int i = 0; i < availableProducts.size(); i++) {
            PastaProduct product = availableProducts.get(i);
            System.out.println((i + 1) + ". " + product.getName() + " - $" + product.getPrice());
        }

        boolean shopping = true;
        while (shopping) {
            System.out.print("Enter the number of the product you want to add to cart (0 to checkout): ");
            int choice = scanner.nextInt();
            
            if (choice >= 1 && choice <= availableProducts.size()) {
                PastaProduct selectedProduct = availableProducts.get(choice - 1);
                cart.addItem(selectedProduct);
                System.out.println(selectedProduct.getName() + " added to cart.");
            } else if (choice == 0) {
                shopping = false;
            } else {
                System.out.println("Invalid choice. Please enter a valid product number.");
            }
        }

        System.out.println("\nCart Contents:");
        for (PastaProduct item : cart.getItems()) {
            System.out.println(item.getName() + " - $" + item.getPrice());
        }
        
        double total = cart.calculateTotal();
        System.out.println("\nTotal: $" + total);

        System.out.println("\nThank you for shopping with us!");
    }
}
