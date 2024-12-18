Класс Book

public class Book {
    private String title;
    private Author author;

    public Book(String title, Author author) {
        this.title = title;
        this.author = author;
    }

    public String getTitle() {
        return title;
    }

    public Author getAuthor() {
        return author;
    }

    @Override
    public String toString() {
        return "Book{" +
                "title='" + title + '\'' +
                ", author=" + author.getName() +
                '}';
    }
}

Класс Author

public class Author {
    private String name;

    public Author(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    @Override
    public String toString() {
        return "Author{" +
                "name='" + name + '\'' +
                '}';
    }
}

Класс Library

import java.util.*;

public class Library {
    private List<Book> books; // Список книг
    private Set<Author> authors; // Уникальные авторы
    private Map<String, List<Book>> booksByGenre; // Книги по жанрам

    public Library() {
        books = new ArrayList<>();
        authors = new HashSet<>();
        booksByGenre = new HashMap<>();
    }

    // Метод для добавления книги
    public void addBook(String title, Author author, String genre) {
        Book book = new Book(title, author);
        books.add(book);
        authors.add(author);

        booksByGenre.putIfAbsent(genre, new ArrayList<>());
        booksByGenre.get(genre).add(book);
    }

    // Метод для вывода всех книг
    public void displayBooks() {
        System.out.println("Books in Library:");
        books.forEach(System.out::println);
    }

    // Метод для вывода авторов
    public void displayAuthors() {
        System.out.println("Unique Authors:");
        authors.forEach(System.out::println);
    }

    // Метод для вывода книг по жанру
    public void displayBooksByGenre(String genre) {
        List<Book> genreBooks = booksByGenre.getOrDefault(genre, Collections.emptyList());
        System.out.println("Books in genre " + genre + ":");
        genreBooks.forEach(System.out::println);
    }
}


Main

public class Main {
    public static void main(String[] args) {
        Library library = new Library();

        // Добавление авторов
        Author author1 = new Author("J.K. Rowling");
        Author author2 = new Author("J.R.R. Tolkien");
        Author author3 = new Author("George Orwell");

        // Добавление книг
        library.addBook("Harry Potter and the Philosopher's Stone", author1, "Fantasy");
        library.addBook("The Hobbit", author2, "Fantasy");
        library.addBook("1984", author3, "Dystopian");
        library.addBook("The Lord of the Rings", author2, "Fantasy");
        library.addBook("Animal Farm", author3, "Dystopian");

        // Вывод всех книг
        library.displayBooks();

        // Вывод всех авторов
        library.displayAuthors();

        // Вывод книг по жанрам
        library.displayBooksByGenre("Fantasy");
        library.displayBooksByGenre("Dystopian");
        library.displayBooksByGenre("Science Fiction");
    }
}

