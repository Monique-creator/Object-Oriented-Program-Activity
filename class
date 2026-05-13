import json
import os
import uuid
from datetime import datetime


class LibraryItem:
    def __init__(self, filename):
        self.id = str(uuid.uuid4())
        self.created_at = datetime.now().isoformat()
        self.updated_at = datetime.now().isoformat()
        self._filename = f"{filename}.json"

    def save(self):
        if os.path.exists(self._filename):
            with open(self._filename) as f:
                old = json.load(f)
            self.id = old["id"]
            self.created_at = old["created_at"]
            self.updated_at = datetime.now().isoformat()

        data = {k: v for k, v in self.__dict__.items() if k != "_filename"}
        with open(self._filename, "w") as f:
            json.dump(data, f, indent=2)
        print(f"Saved {self._filename}")


class Book(LibraryItem):
    def __init__(self, title, author, year, genre):
        super().__init__(title)
        self.title = title
        self.author = author
        self.year = year
        self.genre = genre
        self.is_borrowed = False


class User(LibraryItem):
    def __init__(self, name):
        super().__init__(name)
        self.name = name

    def borrow_book(self, book):
        if not book.is_borrowed:
            book.is_borrowed = True
            print(f"{self.name} has borrowed '{book.title}'")
        else:
            print(f"Sorry, '{book.title}' is unavailable at the moment.")


bookOne = Book("I was never broken", "Harper Lee", 1960, "Fiction")
bookTwo = Book("1988", "George Orwell", 1949, "Dystopian")
bookThree = Book("The Great Gatsby", "F. Scott Fitzgerald", 1925, "Classic")

userOne = User("Emma")
userOne.borrow_book(bookOne)

userOne.borrow_book(bookTwo)

bookOne.save()
bookTwo.save()
bookThree.save()
userOne.save()