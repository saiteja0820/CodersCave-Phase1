import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.Scanner;

public class LibraryManagementSystemInteractive {

    public static void main(String[] args) {
        Lib library = new Lib();
        Scanner scanner = new Scanner(System.in);

        System.out.println("Welcome to the Library Management System!");

        while (true) {
            System.out.println("\nChoose an option:");
            System.out.println("1. Add Book");
            System.out.println("2. Add User");
            System.out.println("3. Borrow Book");
            System.out.println("4. Return Book");
            System.out.println("5. Display Books and Users");
            System.out.println("6. Exit");

            int choice = scanner.nextInt();
            scanner.nextLine();

            switch (choice) {
                case 1:
                    addBook(scanner, library);
                    break;
                case 2:
                    addUser(scanner, library);
                    break;
                case 3:
                    borrowBook(scanner, library);
                    break;
                case 4:
                    returnBook(scanner, library);
                    break;
                case 5:
                    library.displayBooksAndUsers();
                    break;
                case 6:
                    System.out.println("Exiting Library Management System. Goodbye!");
                    scanner.close();
                    System.exit(0);
                default:
                    System.out.println("Invalid choice. Please enter a number between 1 and 6.");
            }
        }
    }

    static class Book {
        private String title;
        private String author;
        private String ISBN;
        private boolean available;

        public Book(String title, String author, String ISBN, boolean available) {
            this.title = title;
            this.author = author;
            this.ISBN = ISBN;
            this.available = available;
        }

        public String getTitle() {
            return title;
        }

        public String getAuthor() {
            return author;
        }

        public String getISBN() {
            return ISBN;
        }

        public boolean isAvailable() {
            return available;
        }

        public void setAvailable(boolean available) {
            this.available = available;
        }
    }

    static class User {
        private String username;
        private String password;
        private String name;
        private int borrowedBooksCount;

        public User(String username, String password, String name, int borrowedBooksCount) {
            this.username = username;
            this.password = password;
            this.name = name;
            this.borrowedBooksCount = borrowedBooksCount;
        }

        public String getUsername() {
            return username;
        }

        public String getPassword() {
            return password;
        }

        public String getName() {
            return name;
        }

        public int getBorrowedBooksCount() {
            return borrowedBooksCount;
        }

        public void setBorrowedBooksCount(int borrowedBooksCount) {
            this.borrowedBooksCount = borrowedBooksCount;
        }
    }

    static class Lib {
        private List<Book> books;
        private List<User> users;
        private Map<Book, User> borrowedBooks;

        public Lib() {
            books = new ArrayList<>();
            users = new ArrayList<>();
            borrowedBooks = new HashMap<>();
        }

        public void addBook(Book book) {
            books.add(book);
        }

        public void addUser(User user) {
            users.add(user);
        }

        public void borrowBook(Book book, User user) {
            if (book.isAvailable()) {
                book.setAvailable(false);
                borrowedBooks.put(book, user);
                user.setBorrowedBooksCount(user.getBorrowedBooksCount() + 1);
                System.out.println(user.getName() + " borrowed " + book.getTitle());
            } else {
                System.out.println("Sorry, " + book.getTitle() + " is not available for borrowing.");
            }
        }

        public void returnBook(Book book, User user) {
            if (borrowedBooks.containsKey(book) && borrowedBooks.get(book) == user) {
                book.setAvailable(true);
                borrowedBooks.remove(book);
                user.setBorrowedBooksCount(user.getBorrowedBooksCount() - 1);
                System.out.println(user.getName() + " returned " + book.getTitle());
            } else {
                System.out.println("Invalid return. This book wasn't borrowed by " + user.getName());
            }
        }

        public void displayBooksAndUsers() {
            System.out.println("\nBooks in the library:");
            for (Book book : books) {
                System.out.println(
                        book.getTitle() + " by " + book.getAuthor() + " (Available: " + book.isAvailable() + ")");
            }

            System.out.println("\nUsers in the library:");
            for (User user : users) {
                System.out.println(user.getName() + " (Username: " + user.getUsername() +
                        ", Borrowed Books: " + user.getBorrowedBooksCount() + ")");
            }
        }

        public List<Book> getBooks() {
            return books;
        }

        public List<User> getUsers() {
            return users;
        }
    }

    private static void addBook(Scanner scanner, Lib library) {
        System.out.println("Enter book details:");
        System.out.print("Title: ");
        String title = scanner.nextLine();
        System.out.print("Author: ");
        String author = scanner.nextLine();
        System.out.print("ISBN: ");
        String ISBN = scanner.nextLine();
        System.out.print("Is Available? (true/false): ");
        boolean available = scanner.nextBoolean();

        Book book = new Book(title, author, ISBN, available);
        library.addBook(book);
        System.out.println("Book added: " + title);
    }

    private static void addUser(Scanner scanner, Lib library) {
        System.out.println("Enter user details:");
        System.out.print("Username: ");
        String username = scanner.nextLine();
        System.out.print("Password: ");
        String password = scanner.nextLine();
        System.out.print("Name: ");
        String name = scanner.nextLine();

        User user = new User(username, password, name, 0);
        library.addUser(user);
        System.out.println("User added: " + name);
    }

    private static void borrowBook(Scanner scanner, Lib library) {
        System.out.println("Enter user details:");
        System.out.print("Username: ");
        String username = scanner.nextLine();
        User user = findUserByUsername(username, library.getUsers());

        if (user != null) {
            System.out.println("Enter book details:");
            System.out.print("Title: ");
            String title = scanner.nextLine();
            Book book = findBookByTitle(title, library.getBooks());

            if (book != null) {
                library.borrowBook(book, user);
            } else {
                System.out.println("Book not found: " + title);
            }
        } else {
            System.out.println("User not found: " + username);
        }
    }

    private static void returnBook(Scanner scanner, Lib library) {
        System.out.println("Enter user details:");
        System.out.print("Username: ");
        String username = scanner.nextLine();
        User user = findUserByUsername(username, library.getUsers());

        if (user != null) {
            System.out.println("Enter book details:");
            System.out.print("Title: ");
            String title = scanner.nextLine();
            Book book = findBookByTitle(title, library.getBooks());

            if (book != null) {
                library.returnBook(book, user);
            } else {
                System.out.println("Book not found: " + title);
            }
        } else {
            System.out.println("User not found: " + username);
        }
    }

    private static User findUserByUsername(String username, List<User> users) {
        for (User user : users) {
            if (user.getUsername().equals(username)) {
                return user;
            }
        }
        return null;
    }

    private static Book findBookByTitle(String title, List<Book> books) {
        for (Book book : books) {
            if (book.getTitle().equals(title)) {
                return book;
            }
        }
        return null;
    }
}
