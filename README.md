import java.util.ArrayList;
import java.util.Scanner;

class Item {
    String name;
    double price;
    int quantity;

    Item(String name, double price, int quantity) {
        this.name = name;
        this.price = price;
        this.quantity = quantity;
    }

    double getTotalPrice() {
        return price * quantity;
    }
}

public class SimpleCashierSystem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        ArrayList<Item> items = new ArrayList<>();
        String addMore;

        System.out.println("=== Sistem Kasir Sederhana ===");

        // Input items
        do {
            System.out.print("Masukkan nama item: ");
            String name = scanner.nextLine();

            System.out.print("Masukkan harga item: ");
            double price = scanner.nextDouble();

            System.out.print("Masukkan jumlah item: ");
            int quantity = scanner.nextInt();

            items.add(new Item(name, price, quantity));

            System.out.print("Apakah ingin menambah item lagi? (ya/tidak): ");
            addMore = scanner.next();
            scanner.nextLine(); // clear the buffer
        } while (addMore.equalsIgnoreCase("ya"));

        // Calculate total
        double totalAmount = 0;
        System.out.println("\n=== Daftar Pembelian ===");
        for (Item item : items) {
            System.out.printf("%-10s: %d x %.2f = %.2f\n", item.name, item.quantity, item.price, item.getTotalPrice());
            totalAmount += item.getTotalPrice();
        }

        // Display total
        System.out.printf("\nTotal Harga: %.2f\n", totalAmount);

        System.out.print("Masukkan jumlah uang yang dibayarkan: ");
        double payment = scanner.nextDouble();

        if (payment >= totalAmount) {
            System.out.printf("Kembalian: %.2f\n", payment - totalAmount);
        } else {
            System.out.printf("Uang tidak cukup. Kurang: %.2f\n", totalAmount - payment);
        }

        System.out.println("Terima kasih telah berbelanja!");
        scanner.close();
    }
}
