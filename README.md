class Contact {
    private String name;
    private String phoneNumber;

    // Constructor
    public Contact(String name, String phoneNumber) {
        this.name = name;
        this.phoneNumber = phoneNumber;
    }

    // Search and display
    public String getName() {
        return name;
    }

    public String getPhoneNumber() {
        return phoneNumber;
    }

    @Override
    public String toString() {
        return "Name: " + name + " | Phone: " + phoneNumber;
    }
}

// Define Directory Class
class Directory {
    private Contact[] contacts;
    private int count;

    public Directory(int capacity) {
        contacts = new Contact[capacity];
        count = 0;
    }

    // Implement addContact()
    public void addContact(String name, String phone) {
        if (count < contacts.length) {
            contacts[count++] = new Contact(name, phone);
            System.out.println("Contact added successfully.");
        } else {
            System.out.println("Error: Directory is full.");
        }
    }

    // Implement searchContact()
    public void searchContact(String name) {
        System.out.println("\nSearching for: " + name);
        boolean found = false;
        for (int i = 0; i < count; i++) {
            if (contacts[i].getName().equalsIgnoreCase(name)) {
                System.out.println("Found -> " + contacts[i]);
                found = true;
                break;
            }
        }
        if (!found) {
            System.out.println("Contact not found.");
        }
    }

    // Implement deleteContact()
    public void deleteContact(String name) {
        boolean found = false;
        for (int i = 0; i < count; i++) {
            if (contacts[i].getName().equalsIgnoreCase(name)) {
                System.out.println("\nDeleting " + name + "...");
               
                // Shift elements to the left
                for (int j = i; j < count - 1; j++) {
                    contacts[j] = contacts[j + 1];
                }
                contacts[count - 1] = null; // Clean up the last reference
                count--;
                found = true;
                System.out.println("Contact deleted successfully.");
                break;
            }
        }
        if (!found) {
            System.out.println("Delete failed: Contact '" + name + "' not found.");
        }
    }

    //  Display All Contacts
    public void displayAll() {
        System.out.println("\n--- Contact List (" + count + ") ---");
        if (count == 0) {
            System.out.println("No contacts stored.");
        } else {
            for (int i = 0; i < count; i++) {
                System.out.println((i + 1) + ". " + contacts[i]);
            }
        }
        System.out.println("------------------------");
    }
}

// Testing the Contact Management System
public class ContactManagementSystem {
    public static void main(String[] args) {
        // Initialize directory 
        Directory myDirectory = new Directory(5);

        
        // Add contacts
        myDirectory.addContact("Sanu", "9688930300");
        myDirectory.addContact("Riya", "9297974753");
        myDirectory.addContact("Deepak", "9179660257");
        
        myDirectory.displayAll();

        // Search 
        myDirectory.searchContact("sanu");

        // Delete
        myDirectory.deleteContact("Sanu");

        // Search again
        System.out.println("\nSearching again...");
        myDirectory.searchContact("Sanu");

        myDirectory.displayAll();
    }
}# Contact-Management-System-
