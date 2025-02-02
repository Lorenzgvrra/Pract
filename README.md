# Pract
#include <iostream>
#include <iomanip> // For formatting output
using namespace std;

// Define a struct to store book details
struct Book {
    string title;
    string author;
    string ISBN;
    int availableCopies;
};

// Function to add a new book
void addBook(Book books[], int &count, int maxBooks) {
    if (count >= maxBooks) {
        cout << "Library is full! Cannot add more books.\n";
        return;
    }

    cout << "Enter book title: ";
    cin.ignore(); // Ignore any leftover newline characters
    getline(cin, books[count].title);

    cout << "Enter author: ";
    getline(cin, books[count].author);

    cout << "Enter ISBN: ";
    cin >> books[count].ISBN;

    cout << "Enter number of copies: ";
    cin >> books[count].availableCopies;

    count++; // Increase book count
    cout << "Book added successfully!\n";
}

// Function to display all books
void displayBooks(const Book books[], int count) {
    if (count == 0) {
        cout << "No books available in the library.\n";
        return;
    }

    cout << "\nList of Books:\n";
    cout << "------------------------------------------------\n";
    cout << "ISBN           | Title              | Author             | Copies Available\n";
    cout << "------------------------------------------------\n";
    
    for (int i = 0; i < count; i++) {
        cout << setw(15) << books[i].ISBN << " | "
             << setw(18) << books[i].title << " | "
             << setw(18) << books[i].author << " | "
             << setw(16) << books[i].availableCopies << endl;
    }
    cout << "------------------------------------------------\n";
}

// Function to search for a book by ISBN
int searchBook(const Book books[], int count, string isbn) {
    for (int i = 0; i < count; i++) {
        if (books[i].ISBN == isbn) {
            return i; // Return the index of the found book
        }
    }
    return -1; // Return -1 if not found
}

// Function to borrow a book
void borrowBook(Book books[], int count) {
    string isbn;
    cout << "Enter ISBN of the book to borrow: ";
    cin >> isbn;

    int index = searchBook(books, count, isbn);
    if (index == -1) {
        cout << "Book not found!\n";
        return;
    }

    if (books[index].availableCopies > 0) {
        books[index].availableCopies--;
        cout << "Book borrowed successfully!\n";
    } else {
        cout << "No copies available for borrowing.\n";
    }
}

// Function to return a book
void returnBook(Book books[], int count) {
    string isbn;
    cout << "Enter ISBN of the book to return: ";
    cin >> isbn;

    int index = searchBook(books, count, isbn);
    if (index == -1) {
        cout << "Book not found!\n";
        return;
    }

    books[index].availableCopies++;
    cout << "Book returned successfully!\n";
}

// Main function
int main() {
    const int maxBooks = 100; // Maximum number of books
    Book books[maxBooks]; // Array to store books
    int bookCount = 0; // Keeps track of the number of books

    while (true) {
        cout << "\nLibrary Management System\n";
        cout << "1. Add a Book\n";
        cout << "2. Display Books\n";
        cout << "3. Borrow a Book\n";
        cout << "4. Return a Book\n";
        cout << "5. Exit\n";
        cout << "Enter your choice: ";
        
        int choice;
        cin >> choice;

        switch (choice) {
            case 1:
                addBook(books, bookCount, maxBooks);
                break;
            case 2:
                displayBooks(books, bookCount);
                break;
            case 3:
                borrowBook(books, bookCount);
                break;
            case 4:
                returnBook(books, bookCount);
                break;
            case 5:
                cout << "Exiting program...\n";
                return 0;
            default:
                cout << "Invalid choice! Please try again.\n";
        }
    }

    return 0;
}
