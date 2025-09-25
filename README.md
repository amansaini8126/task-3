public class Book {
    private String title;
    private String author;
    private String isbn;
    private boolean isIssued;

    public Book(String title, String author, String isbn) {
        this.title = title;
        this.author = author;
        this.isbn = isbn;
        this.isIssued = false;
    }

    public String getTitle() {
        return title;
    }

    public String getIsbn() {
        return isbn;
    }

    public boolean isIssued() {
        return isIssued;
    }

    public void issueBook() {
        isIssued = true;
    }

    public void returnBook() {
        isIssued = false;
    }

    public void displayInfo() {
        System.out.println("Title: " + title + ", Author: " + author + ", ISBN: " + isbn + ", Issued: " + isIssued);
    }
}
public class User {
    private String name;
    private String userId;

    public User(String name, String userId) {
        this.name = name;
        this.userId = userId;
    }

    public String getName() {
        return name;
    }

    public String getUserId() {
        return userId;
    }
}
  import java.util.ArrayList;

public class Library {
    private ArrayList<Book> books;
    private ArrayList<User> users;

    public Library() {
        books = new ArrayList<>();
        users = new ArrayList<>();
    }

    public void addBook(Book book) {
        books.add(book);
        System.out.println("Book added: " + book.getTitle());
    }

    public void addUser(User user) {
        users.add(user);
        System.out.println("User added: " + user.getName());
    }

    public void issueBook(String isbn, String userId) {
        Book book = findBookByIsbn(isbn);
        User user = findUserById(userId);

        if (book == null) {
            System.out.println("Book not found.");
            return;
        }

        if (user == null) {
            System.out.println("User not found.");
            return;
        }

        if (book.isIssued()) {
            System.out.println("Book is already issued.");
        } else {
            book.issueBook();
            System.out.println("Book '" + book.getTitle() + "' issued to " + user.getName());
        }
    }

    public void returnBook(String isbn) {
        Book book = findBookByIsbn(isbn);
        if (book != null && book.isIssued()) {
            book.returnBook();
            System.out.println("Book '" + book.getTitle() + "' returned.");
        } else {
            System.out.println("Book is not issued or not found.");
        }
    }

    public void showAllBooks() {
        System.out.println("=== Book List ===");
        for (Book book : books) {
            book.displayInfo();
        }
    }

    private Book findBookByIsbn(String isbn) {
        for (Book b : books) {
            if (b.getIsbn().equals(isbn)) return b;
        }
        return null;
    }

    private User findUserById(String userId) {
        for (User u : users) {
            if (u.getUserId().equals(userId)) return u;
        }
        return null;
    }
}
public class Main {
    public static void main(String[] args) {
        Library library = new Library();

        // Add users
        User user1 = new User("Alice", "U001");
        User user2 = new User("Bob", "U002");
        library.addUser(user1);
        library.addUser(user2);

        // Add books
        Book book1 = new Book("The Alchemist", "Paulo Coelho", "B001");
        Book book2 = new Book("1984", "George Orwell", "B002");
        library.addBook(book1);
        library.addBook(book2);

        // Display books
        library.showAllBooks();

        // Issue book
        library.issueBook("B001", "U001");
        library.issueBook("B001", "U002"); // Already issued

        // Return book
        library.returnBook("B001");

        // Try returning again
        library.returnBook("B001");

        // Final state of books
        library.showAllBooks();
    }
}
