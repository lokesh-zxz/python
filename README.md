

class Book:
    def __init__(self, title, author, isbn):
        self.title = title
        self.author = author
        self.isbn = isbn
        self.is_available = True

class Library:
    def __init__(self):
        self.books = []

    def add_book(self, book):
        self.books.append(book)

    def remove_book(self, isbn):
        self.books = [book for book in self.books if book.isbn != isbn]

    def find_book(self, isbn):
        for book in self.books:
            if book.isbn == isbn:
                return book
        return None

    def list_books(self):
        return [(book.title, book.author, book.isbn, book.is_available) for book in self.books]

class User:
    def __init__(self, name):
        self.name = name
        self.borrowed_books = []

    def borrow_book(self, book):
        if book.is_available:
            book.is_available = False
            self.borrowed_books.append(book)
            return True
        return False

    def return_book(self, book):
        if book in self.borrowed_books:
            book.is_available = True
            self.borrowed_books.remove(book)
            return True
        return False

# Deployment
if __name__ == "__main__":
    library = Library()
    user = User("John Doe")

    # Adding books to the library
    library.add_book(Book("1984", "George Orwell", "1234567890"))
    library.add_book(Book("To Kill a Mockingbird", "Harper Lee", "0987654321"))

    # Listing available books
    print("Available books:", library.list_books())

    # User borrowing a book
    book_to_borrow = library.find_book("1234567890")
    if user.borrow_book(book_to_borrow):
        print(f"{user.name} borrowed {book_to_borrow.title}")

    # Listing available books after borrowing
    print("Available books after borrowing:", library.list_books())

    # User returning a book
    if user.return_book(book_to_borrow):
        print(f"{user.name} returned {book_to_borrow.title}")

    # Listing available books after returning
    print("Available books after returning:", library.list_books())
