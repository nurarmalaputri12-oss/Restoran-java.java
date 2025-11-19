import java.util.ArrayList;
import java.util.Scanner;

class MenuItem {
    String name;
    double price;
    String category;

    MenuItem(String name, double price, String category) {
        this.name = name;
        this.price = price;
        this.category = category;
    }
}

class OrderItem {
    MenuItem menuItem;
    int quantity;

    OrderItem(MenuItem menuItem, int quantity) {
        this.menuItem = menuItem;
        this.quantity = quantity;
    }

    double getTotalPrice() {
        return menuItem.price * quantity;
    }
}

public class RestoranApp {
    static Scanner input = new Scanner(System.in);
    static ArrayList<MenuItem> menuList = new ArrayList<>();

    public static void main(String[] args) {
        // Menu awal restoran
        menuList.add(new MenuItem("Nasi Goreng", 20000, "Makanan"));
        menuList.add(new MenuItem("Mie Ayam", 15000, "Makanan"));
        menuList.add(new MenuItem("Es Teh", 5000, "Minuman"));
        menuList.add(new MenuItem("Jus Jeruk", 10000, "Minuman"));

        while (true) {
            System.out.println("\n=== Selamat Datang di Restoran ===");
            System.out.println("1. Menu Pelanggan");
            System.out.println("2. Menu Pengelolaan (Pemilik)");
            System.out.println("3. Keluar");
            System.out.print("Pilih menu: ");
            String choice = input.nextLine();

            switch (choice) {
                case "1":
                    customerMenu();
                    break;
                case "2":
                    ownerMenu();
                    break;
                case "3":
                    System.out.println("Terima kasih, sampai jumpa!");
                    System.exit(0);
                default:
                    System.out.println("Input tidak valid, coba lagi.");
            }
        }
    }

    // Menu Pelanggan
    static void customerMenu() {
        ArrayList<OrderItem> orders = new ArrayList<>();
        while (true) {
            System.out.println("\n--- Daftar Menu ---");
            for (int i = 0; i < menuList.size(); i++) {
                MenuItem item = menuList.get(i);
                System.out.printf("%d. %s (%s) - Rp %.0f\n", i + 1, item.name, item.category, item.price);
            }
            System.out.println("Ketik 'selesai' untuk mengakhiri pemesanan.");
            System.out.print("Masukkan nomor menu yang ingin dipesan: ");
            String inputMenu = input.nextLine();

            if (inputMenu.equalsIgnoreCase("selesai")) {
                if (orders.isEmpty()) {
                    System.out.println("Belum ada pesanan.");
                    return;
                } else {
                    printReceipt(orders);
                    return;
                }
            }

            int menuIndex;
            try {
                menuIndex = Integer.parseInt(inputMenu) - 1;
                if (menuIndex < 0 || menuIndex >= menuList.size()) throw new Exception();
            } catch (Exception e) {
                System.out.println("Input tidak valid, pilih menu yang tersedia.");
                continue;
            }

            System.out.print("Masukkan jumlah: ");
            int qty;
            try {
                qty = Integer.parseInt(input.nextLine());
                if (qty <= 0) throw new Exception();
            } catch (Exception e) {
                System.out.println("Jumlah tidak valid, coba lagi.");
                continue;
            }

            orders.add(new OrderItem(menuList.get(menuIndex), qty));
            System.out.println("Item ditambahkan ke pesanan.");
        }
    }

    // Cetak struk pesanan
    static void printReceipt(ArrayList<OrderItem> orders) {
        double total = 0;
        double drinkDiscount = 0;

        System.out.println("\n=== STRUK PESANAN ===");
        for (OrderItem order : orders) {
            double itemTotal = order.getTotalPrice();
            System.out.printf("%s x%d - Rp %.0f\n", order.menuItem.name, order.quantity, itemTotal);
            total += itemTotal;
        }

        // Diskon Beli 1 Gratis 1 untuk minuman jika total > 50.000
        if (total > 50000) {
            for (OrderItem order : orders) {
                if (order.menuItem.category.equalsIgnoreCase("Minuman")) {
                    drinkDiscount += (order.quantity / 2) * order.menuItem.price;
                }
            }
            if (drinkDiscount > 0) {
                System.out.printf("Diskon Minuman B1G1: -Rp %.0f\n", drinkDiscount);
            }
        }

        double discount = 0;
        if (total > 100000) {
            discount = 0.1 * total;
            System.out.printf("Diskon 10%%: -Rp %.0f\n", discount);
        }

        double tax = 0.1 * total;
        double service = 20000;
        double finalTotal = total - discount - drinkDiscount + tax + service;

        System.out.printf("Subtotal: Rp %.0f\n", total);
        System.out.printf("Pajak 10%%: Rp %.0f\n", tax);
        System.out.printf("Biaya pelayanan: Rp %.0f\n", service);
        System.out.printf("Total yang harus dibayar: Rp %.0f\n", finalTotal);
        System.out.println("====================\n");
    }

    // Menu Pengelolaan Pemilik
    static void ownerMenu() {
        while (true) {
            System.out.println("\n--- Menu Pengelolaan ---");
            System.out.println("1. Tambah Menu");
            System.out.println("2. Ubah Harga Menu");
            System.out.println("3. Hapus Menu");
            System.out.println("4. Kembali");
            System.out.print("Pilih menu: ");
            String choice = input.nextLine();

            switch (choice) {
                case "1":
                    addMenu();
                    break;
                case "2":
                    editMenu();
                    break;
                case "3":
                    deleteMenu();
                    break;
                case "4":
                    return;
                default:
                    System.out.println("Input tidak valid.");
            }
        }
    }

    static void addMenu() {
        System.out.print("Nama Menu: ");
        String name = input.nextLine();
        System.out.print("Harga: ");
        double price = Double.parseDouble(input.nextLine());
        System.out.print("Kategori (Makanan/Minuman): ");
        String category = input.nextLine();
        menuList.add(new MenuItem(name, price, category));
        System.out.println("Menu berhasil ditambahkan.");
    }

    static void editMenu() {
        for (int i = 0; i < menuList.size(); i++) {
            MenuItem item = menuList.get(i);
            System.out.printf("%d. %s - Rp %.0f\n", i + 1, item.name, item.price);
        }
        System.out.print("Pilih nomor menu yang ingin diubah: ");
        int index = Integer.parseInt(input.nextLine()) - 1;
        if (index < 0 || index >= menuList.size()) {
            System.out.println("Nomor menu tidak valid.");
            return;
        }

        System.out.print("Konfirmasi ubah menu? (Ya/Tidak): ");
        String confirm = input.nextLine();
        if (confirm.equalsIgnoreCase("Ya")) {
            System.out.print("Masukkan harga baru: ");
            double newPrice = Double.parseDouble(input.nextLine());
            menuList.get(index).price = newPrice;
            System.out.println("Harga berhasil diubah.");
        } else {
            System.out.println("Perubahan dibatalkan.");
        }
    }

    static void deleteMenu() {
        for (int i = 0; i < menuList.size(); i++) {
            MenuItem item = menuList.get(i);
            System.out.printf("%d. %s - Rp %.0f\n", i + 1, item.name, item.price);
        }
        System.out.print("Pilih nomor menu yang ingin dihapus: ");
        int index = Integer.parseInt(input.nextLine()) - 1;
        if (index < 0 || index >= menuList.size()) {
            System.out.println("Nomor menu tidak valid.");
            return;
        }

        System.out.print("Konfirmasi hapus menu? (Ya/Tidak): ");
        String confirm = input.nextLine();
        if (confirm.equalsIgnoreCase("Ya")) {
            menuList.remove(index);
            System.out.println("Menu berhasil dihapus.");
        } else {
            System.out.println("Penghapusan dibatalkan.");
        }
    }
}
