# Mycrudproject
import java.util.ArrayList;
import java.util.Scanner;

class Person {
    String name;
    int age;
    Person(String name, int age) { this.name = name; this.age = age; }
}

public class Main {
    private static ArrayList<Person> people = new ArrayList<>();
    private static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        int choice;
        do {
            System.out.println("\n=== SIMPLE CRUD APP ===");
            System.out.println("1. Create (Add Person)");
            System.out.println("2. Read (View All People)");
            System.out.println("3. Update (Edit Person)");
            System.out.println("4. Delete (Remove Person)");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");

            while (!scanner.hasNextInt()) {
                System.out.print("Please enter a number: ");
                scanner.next();
            }
            choice = scanner.nextInt();
            scanner.nextLine(); // clear buffer

            switch (choice) {
                case 1: createPerson(); break;
                case 2: readPeople(); break;
                case 3: updatePerson(); break;
                case 4: deletePerson(); break;
                case 5: System.out.println("Exiting... Goodbye!"); break;
                default: System.out.println("Invalid choice. Try again!");
            }
        } while (choice != 5);
    }

    private static void createPerson() {
        System.out.print("Enter name: ");
        String name = scanner.nextLine().trim();
        System.out.print("Enter age: ");
        while (!scanner.hasNextInt()) {
            System.out.print("Please enter a valid age: ");
            scanner.next();
        }
        int age = scanner.nextInt();
        scanner.nextLine();
        people.add(new Person(name, age));
        System.out.println("✅ Person added successfully!");
    }

    private static void readPeople() {
        if (people.isEmpty()) {
            System.out.println("No records found.");
        } else {
            System.out.println("\n--- People List ---");
            for (int i = 0; i < people.size(); i++) {
                Person p = people.get(i);
                System.out.println((i + 1) + ". Name: " + p.name + ", Age: " + p.age);
            }
        }
    }

    private static void updatePerson() {
        readPeople();
        if (people.isEmpty()) return;
        System.out.print("Enter record number to update: ");
        while (!scanner.hasNextInt()) {
            System.out.print("Please enter a number: ");
            scanner.next();
        }
        int index = scanner.nextInt() - 1;
        scanner.nextLine();
        if (index >= 0 && index < people.size()) {
            System.out.print("Enter new name: ");
            String newName = scanner.nextLine().trim();
            System.out.print("Enter new age: ");
            while (!scanner.hasNextInt()) {
                System.out.print("Please enter a valid age: ");
                scanner.next();
            }
            int newAge = scanner.nextInt();
            scanner.nextLine();
            people.get(index).name = newName;
            people.get(index).age = newAge;
            System.out.println("✅ Record updated successfully!");
        } else {
            System.out.println("❌ Invalid record number.");
        }
    }

    private static void deletePerson() {
        readPeople();
        if (people.isEmpty()) return;
        System.out.print("Enter record number to delete: ");
        while (!scanner.hasNextInt()) {
            System.out.print("Please enter a number: ");
            scanner.next();
        }
        int index = scanner.nextInt() - 1;
        scanner.nextLine();
        if (index >= 0 && index < people.size()) {
            people.remove(index);
            System.out.println("✅ Record deleted successfully!");
        } else {
            System.out.println("❌ Invalid record number.");
        }
    }
}
