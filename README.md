# LMS
Library Management System(Enroll_Number: EBEON0723823456,EDUBRIDGE)

Source Code:
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.Scanner;

class Book {
    private String title;
    private String author;
    private int year;

    public Book(String title, String author, int year) {
        this.title = title;
        this.author = author;
        this.year = year;
    }

    public String getTitle() {
        return title;
    }

    public String getAuthor() {
        return author;
    }

    public int getYear() {
        return year;
    }
}

class User {
    private String name;
    private String phoneNo;

    public User(String name, String phoneNo) {
        this.name = name;
        this.phoneNo = phoneNo;
    }

    public String getName() {
        return name;
    }

    public String getPhoneNo() {
        return phoneNo;
    }
}

class Library {
    private ArrayList<Book> books;
    private Map<Book, User> borrowedBooks;

    public Library() {
        books = new ArrayList<>();
        borrowedBooks = new HashMap<>();
    }

    public void addBook(Book book) {
        books.add(book);
    }

    public void removeBook(Book book) {
        books.remove(book);
        borrowedBooks.remove(book);
    }

    public void displayBooks() {
        for (Book book : books) {
            System.out.println(book.getTitle() + " by " + book.getAuthor() + " (" + book.getYear() + ")");
        }
    }

    public void registerUser(User user) {
        System.out.println("__[" + user.getName() + " is registered with phone number " + user.getPhoneNo() + "]__");
    }

    public void borrowBook(Book book, User user) {
        if (books.contains(book)) {
            borrowedBooks.put(book, user);
            System.out.println("__[" + user.getName() + " has borrowed " + book.getTitle() + "]__");
        } else {
            System.out.println("__Book not found in the library.__");
        }
    }

    public void returnBook(Book book, User user) {
        if (borrowedBooks.containsKey(book) && borrowedBooks.get(book).equals(user)) {
            borrowedBooks.remove(book);
            System.out.println("__[" + user.getName() + " has returned " + book.getTitle() + "]__");
        } else {
            System.out.println("__"+user.getName()+"Book returned Successfully!...__");
        }
    }

    public ArrayList<Book> getBooks() {
        return books;
    }
}

public class LibraryManagementSystem {
    public static void main(String[] args) {
        Library library = new Library();
        Scanner scanner = new Scanner(System.in);
        Book initialBook1 = new Book("Ponniyin Selvan", "kalki KrishnaMurthy", 1954);
        Book initialBook2 = new Book("Beyond the Story 10-yr Record of BTS","Myeongseok Kang", 2023);
        Book initialBook3 = new Book("Ikigai","Francesc Miralles", 2016);
        Book initialBook4 = new Book("Effective java", "John", 2001);
        library.addBook(initialBook1);
        library.addBook(initialBook2);
        library.addBook(initialBook3);
        library.addBook(initialBook4);

        boolean running = true;
        while (running) {
            System.out.println("1. Register a user");
            System.out.println("2. Display all books");
            System.out.println("3. Add a book");
            System.out.println("4. Remove a book");
            System.out.println("5. Borrow a book");
            System.out.println("6. Return a book");
            System.out.println("7. Exit");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();
            scanner.nextLine();

            switch (choice) {
                case 1:
                    System.out.print("Enter the user's name: ");
                    String userName = scanner.nextLine();
                    System.out.print("Enter the user's phone number: ");
                    String userPhoneNo = scanner.nextLine();
                    User user = new User(userName, userPhoneNo);
                    library.registerUser(user);
                    break;

                case 2:
                    library.displayBooks();
                    break;

                case 3:
                    System.out.print("Enter the title of the book: ");
                    String title = scanner.nextLine();
                    System.out.print("Enter the author of the book: ");
                    String author = scanner.nextLine();
                    System.out.print("Enter the year of publication: ");
                    int year = scanner.nextInt();
                    scanner.nextLine();

                    Book book = new Book(title, author, year);
                    library.addBook(book);
                    System.out.println("__Book added successfully!...__");
                    break;

                case 4:
                    System.out.print("Enter the title of the book to remove: ");
                    String removeTitle = scanner.nextLine();

                    boolean bookRemoved = false;
                    for (Book b : library.getBooks()) {
                        if (b.getTitle().equalsIgnoreCase(removeTitle)) {
                            library.removeBook(b);
                            bookRemoved = true;
                            System.out.println("__Book removed successfully!...__");
                            break;
                        }
                    }

                    if (!bookRemoved) {
                        System.out.println("Book not found in the library.");
                    }
                    break;
                case 5:
                    System.out.print("Enter the title of the book to borrow: ");
                    String borrowTitle = scanner.nextLine();
                    boolean bookFoundToBorrow = false;
                    for (Book b : library.getBooks()) {
                        if (b.getTitle().equalsIgnoreCase(borrowTitle)) {
                            bookFoundToBorrow = true;
                            System.out.println("Enter the user name: ");
                            String borrowName = scanner.nextLine();
                            User borrower = new User(borrowName, "");
                            library.borrowBook(b, borrower);
                            break;
                        }
                    }
                    if (!bookFoundToBorrow) {
                        System.out.println("Book not found in the library");
                    }
                    break;

                case 6:
                    System.out.print("Enter the title of the book to return: ");
                    String returnTitle = scanner.nextLine();
                    boolean bookFoundToReturn = false;

                    for (Book b : library.getBooks()) {
                        if (b.getTitle().equalsIgnoreCase(returnTitle)) {
                            bookFoundToReturn = true;
                            System.out.print("Enter the user's name: ");
                            String returnerName = scanner.nextLine();
                            User returner = new User(returnerName, "");
                            library.returnBook(b, returner);
                            break;
                        }
                    }

                    if (!bookFoundToReturn) {
                        System.out.println("Book not found in the library.");
                    }
                    break;

                case 7:
                    running = false;
                    System.out.println("__Exiting the Library Management System.__");
                    break;

                default:
                    System.out.println("__Invalid choice. Please choose a valid option.__");
            }
        }

        scanner.close();
    }
}


