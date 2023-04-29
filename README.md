# Library-Management-System
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_BOOKS 100

struct Book {
    char title[100];
    char author[50];
    int book_id;
};

struct Library {
    struct Book books[MAX_BOOKS];
    int num_books;
};
void add_book(struct Library* lib, char title[], char author[], int book_id) {
    if (lib->num_books >= MAX_BOOKS) {
        printf("Library is full\n");
        return;
    }
    strcpy(lib->books[lib->num_books].title, title);
    strcpy(lib->books[lib->num_books].author, author);
    lib->books[lib->num_books].book_id = book_id;
    lib->num_books++;
    printf("Book added successfully\n");
}

void search_book(struct Library* lib, int book_id) {
    int found = 0;
    for (int i = 0; i < lib->num_books; i++) {
        if (lib->books[i].book_id == book_id) {
            printf("Book found!\n");
            printf("Title: %s\n", lib->books[i].title);
            printf("Author: %s\n", lib->books[i].author);
            printf("Book ID: %d\n", lib->books[i].book_id);
            found = 1;
            break;
        }
    }
    if (!found) {
        printf("Book not found\n");
    }
}

void display_books(struct Library* lib) {
    printf("Library Books:\n");
    for (int i = 0; i < lib->num_books; i++) {
        printf("%d) Title: %s, Author: %s, Book ID: %d\n", i+1, lib->books[i].title, lib->books[i].author, lib->books[i].book_id);
    }
}

int main() {
    struct Library lib;
    lib.num_books = 0;

    int choice;
    char title[100], author[50];
    int book_id;

    while (1) {
        printf("\nLibrary Management System\n");
        printf("1. Add Book\n");
        printf("2. Search Book\n");
        printf("3. Display Books\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter Book Title: ");
                scanf("%s", title);
                printf("Enter Book Author: ");
                scanf("%s", author);
                printf("Enter Book ID: ");
                scanf("%d", &book_id);
                add_book(&lib, title, author, book_id);
                break;
            case 2:
                printf("Enter Book ID: ");
                scanf("%d", &book_id);
                search_book(&lib, book_id);
                break;
            case 3:
                display_books(&lib);
                break;
            case 4:
                printf("Exiting Library Management System\n");
                exit(0);
            default:
                printf("Enter a valid choice!\n");
        }
    }

    return 0;
}
