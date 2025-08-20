#include <iostream>
#include <string>
#include <algorithm>
#include <cctype>
using namespace std;

// to match lower and upper case similarly.
string toLowerCase(string str)
{
    transform(str.begin(), str.end(), str.begin(),
              [](unsigned char c)
              { return tolower(c); });
    return str;
}

// for partially matching of searched string.
bool containsIgnoreCase(const string &str, const string &sub)
{
    string lowerStr = toLowerCase(str);
    string lowerSub = toLowerCase(sub);
    return lowerStr.find(lowerSub) != string::npos;
}

// confirmation for deletion or exiting
bool confirmAction(const string &action)
{
    string input;
    cout << "Are you sure you want to " << action << "? (y/n): ";
    cin >> input;
    return (tolower(input[0]) == 'y' && !input.empty());
}

const int maxBook = 100;

struct Book
{
    int bookID;
    string title;
    string author;
    int quantity;
};

void addBook(Book library[], int &count);
void displayBook(Book library[], int count);
void updateBook(Book library[], int count);
void deleteBook(Book library[], int &count);
void searchBookByID(Book library[], int count);
void searchBookByAuthor(Book library[], int count);
void searchBookByTitle(Book library[], int count);
void borrowBook(Book library[], int count);
void returnBook(Book library[], int count);

int main()
{

    Book library[maxBook];
    int count = 0;
    int choice;

    cout << " ===== Welcome to Libray Management System ===== \n ";

    do
    {

        cout << "\n Main Menu \n";
        cout << "1. Add New Book. \n";
        cout << "2. Display All Books. \n";
        cout << "3. Search Any Book. \n";
        cout << "4. Update Book Information. \n";
        cout << "5. Borrow Book\n";
        cout << "6. Return Book\n";
        cout << "7. Delete Book. \n";
        cout << "8. Exit. \n";

        cout << "Enter Your Choice:  ";
        cin >> choice;

        switch (choice)
        {
        case 1:
            addBook(library, count);
            break;

        case 2:
            displayBook(library, count);
            break;

        case 3:
        {
            int searchChoice;
            cout << "\nSearch Menu:\n";
            cout << "1.Search by ID\n";
            cout << "2.Search by Author Name\n";
            cout << "3.Search by Book Title\n";
            cout << "Enter choice: ";
            cin >> searchChoice;

            switch (searchChoice)
            {
            case 1:
                searchBookByID(library, count);
                break;
            case 2:
                searchBookByAuthor(library, count);
                break;
            case 3:
                searchBookByTitle(library, count);
                break;
            default:
                cout << "Invalid choice!\n";
            }
            break;
        }
        case 4:
            updateBook(library, count);
            break;

        case 5:
            borrowBook(library, count);
            break;

        case 6:
            returnBook(library, count);
            break;

        case 7:
            deleteBook(library, count);
            break;

        case 8:
            if (confirmAction("exit the program"))
            {
                cout << "Exiting... Goodbye!\n";
                return 0;
            }
            break;

        default:
            cout << "Invalid Choice. Please enter a number between 1 and 6.\n";
            break;
        }
    } while (choice != 8);

    return 0;
}

// Function Definitions

void addBook(Book library[], int &count)
{
    int id;
    bool duplicate = false;

    do
    {
        duplicate = false;
        cout << "Enter Book ID (+ve int.): ";
        cin >> id;

        if (cin.fail() || id <= 0) // detects input type errors(e.g text instead of number.)
        {
            cout << "Invalid Input. Book ID must be a positive number.\n";
            cin.clear();            // clear error state
            cin.ignore(1000, '\n'); // Ignore up to 1000 characters or until a newline (\n) is found — whichever comes first.
            continue;
        }

        for (int i = 0; i < count; i++)
        {
            if (library[i].bookID == id)
            {
                cout << "Book ID already exists. Please enter a unique ID.\n";
                duplicate = true;
                break;
            }
        }
    } while (id <= 0 || duplicate);

    library[count].bookID = id;
    cin.ignore(); // To prevent getline() from reading leftover input

    cout << "Enter Book Title: ";
    getline(cin, library[count].title);

    cout << "Enter Author Name: ";
    getline(cin, library[count].author);

    do
    {
        cout << "Enter Book Quantity (Non-Negative): ";
        cin >> library[count].quantity;

        if (cin.fail() || library[count].quantity < 0)
        {
            cout << "Invalid quantity. Please enter a non-negative number.\n";
            cin.clear();
            cin.ignore(1000, '\n');
        }

    } while (library[count].quantity < 0);

    cout << "Book Added Successfully!\n";
    count++;

    if (count >= maxBook)
    {
        cout << "Library is Full! Cannot add more books.\n";
        return;
    }
}

// Display function
void displayBook(Book library[], int count)
{
    if (count == 0)
    {
        cout << "\nNo Books Available. \n";
        return;
    }

    cout << "\nList of Books: \n";
    for (int i = 0; i < count; i++)
    {
        cout << "-------------------------------------------------\n";
        cout << "Book ID: " << library[i].bookID << endl;
        cout << "Title: " << library[i].title << endl;
        cout << "Author: " << library[i].author << endl;
        cout << "Quantity: " << library[i].quantity << endl;
        cout << "-------------------------------------------------\n";
    }
}

// search functions
void searchBookByID(Book library[], int count)
{
    int id;
    cout << "\nEnter Book ID to Search: ";
    bool found = false;

    while (true)
    {
        cin >> id;
        if (cin.fail() || id <= 0)
        {
            cout << "Invalid Input. Enter positive Book ID: ";
            cin.clear();
            cin.ignore(1000, '\n');
        }
        else
        {
            break;
        }
    }

    for (int i = 0; i < count; i++)
    {
        if (library[i].bookID == id)
        {
            cout << "-------------------------------------------------\n";
            cout << "Book ID: " << library[i].bookID << endl;
            cout << "Title: " << library[i].title << endl;
            cout << "Author: " << library[i].author << endl;
            cout << "Quantity: " << library[i].quantity << endl;
            cout << "-------------------------------------------------\n";
            found = true;
            break;
        }
    }
    if (!found)
    {
        cout << "Book Not Found!\n";
    }
}

void searchBookByAuthor(Book library[], int count)
{
    string author;
    cout << "\nEnter Author Name to Search: ";
    cin.ignore();
    getline(cin, author);

    bool found = false;
    for (int i = 0; i < count; i++)
    {
        if (containsIgnoreCase(library[i].author, author))
        {
            cout << "-------------------------------------------------\n";
            cout << "Book ID: " << library[i].bookID << endl;
            cout << "Title: " << library[i].title << endl;
            cout << "Author: " << library[i].author << endl;
            cout << "Quantity: " << library[i].quantity << endl;
            cout << "-------------------------------------------------\n";
            found = true;
        }
    }

    if (!found)
        cout << "No books found for author: " << author << "\n";
}

void searchBookByTitle(Book library[], int count)
{
    string title;
    cout << "\nEnter Book Title to Search: ";
    cin.ignore();
    getline(cin, title);

    bool found = false;

    for (int i = 0; i < count; i++)
    {
        if (containsIgnoreCase(library[i].title, title))
        {
            cout << "-------------------------------------------------\n";
            cout << "Book ID: " << library[i].bookID << endl;
            cout << "Title: " << library[i].title << endl;
            cout << "Author: " << library[i].author << endl;
            cout << "Quantity: " << library[i].quantity << endl;
            cout << "-------------------------------------------------\n";
            found = true;
        }
    }

    if (!found)
        cout << "No books found with title: " << title << "\n";
}

// Update function
void updateBook(Book library[], int count)
{
    int id;
    cout << "Enter Book ID to Update: ";

    while (true)
    {
        cin >> id;
        if (cin.fail() || id <= 0)
        {
            cout << "Invalid Input. Enter positive Book ID: ";
            cin.clear();
            cin.ignore(1000, '\n');
        }
        else
        {
            break;
        }
    }

    for (int i = 0; i < count; i++)
    {
        if (library[i].bookID == id)
        {
            cin.ignore();

            cout << "Enter Book Title: ";
            getline(cin, library[i].title);

            cout << "Enter Author Name: ";
            getline(cin, library[i].author);

            do
            {
                cout << "Enter New Quantity(non-negative): ";
                cin >> library[i].quantity;
                if (cin.fail() || library[i].quantity < 0)
                {
                    cout << "Invalid input. Please enter a non-negative quantity.\n";
                    cin.clear();
                    cin.ignore(1000, '\n');
                }
            } while (library[i].quantity < 0);

            cout << "Book Information Updated! \n";
            return;
        }
    }

    cout << "Book Not Found!\n";
}

// borrow book function
void borrowBook(Book library[], int count) {
    int id;
    cout << "\nEnter Book ID to Borrow: ";
    cin >> id;
    for (int i = 0; i < count; i++) {
        if (library[i].bookID == id) {
            if (library[i].quantity > 0) {
                library[i].quantity--;
                cout << "You borrowed \"" << library[i].title << "\" successfully.\n";
            } else {
                cout << "No copies available.\n";
            }
            return;
        }
    }
    cout << "Book ID not found.\n";
}

// return book function
void returnBook(Book library[], int count) {
    int id;
    cout << "\nEnter Book ID to Return: ";
    cin >> id;
    for (int i = 0; i < count; i++) {
        if (library[i].bookID == id) {
            library[i].quantity++;
            cout << "You returned \"" << library[i].title << "\" successfully.\n";
            return;
        }
    }
    cout << "Book ID not found.\n";
}

// Delete Function
void deleteBook(Book library[], int &count)
{
    int id;
    cout << "Enter Book ID to Delete: ";

    while (true)
    {
        cin >> id;
        if (cin.fail() || id <= 0)
        {
            cout << "Invalid input. Please enter a valid positive Book ID: ";
            cin.clear();
            cin.ignore(1000, '\n');
        }
        else
        {
            break;
        }
    }

    for (int i = 0; i < count; i++)
    {
        if (library[i].bookID == id)
        {
            for (int j = i; j < count - 1; j++)
            {
                library[j] = library[j + 1];
            }
            count--;
            cout << "Book Deleted Successfully!";
            return;
        }
    }

    cout << "Book Not Found! ";
}
 
