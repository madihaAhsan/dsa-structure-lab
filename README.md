Exercise 2.1 
Consider a scenario where a library wants to manage its collection of books. Each book has a unique ISBN, title, author, and publication year. The data is maintained in a doubly linked list. 
Create the following functions for the book collection: 
1.	Insert: Insert a new book record into the collection. 
2.	Search: Search for a book record using ISBN or title. 
3.	Modify: Update the details of an existing book record. 
4. Display: Display all book records and the total number of books in the collection. 
Code
#include <iostream>
using namespace std;
struct Book {
    int id, year;
    string title, author;
    Book* prev;
    Book* next;
};
class Library {
private:
    Book* start;
public:
    Library() {
        start = NULL;
    }
    void insert() {
        Book* cur = new Book;
        cout << "Enter Book ID: ";
        cin >> cur->id;
        cout << "Enter Title: ";
        cin >> cur->title;
        cout << "Enter Author: ";
        cin >> cur->author;
        cout << "Enter Year: ";
        cin >> cur->year;

        cur->next = NULL;
        cur->prev = NULL;

        if (start == NULL) {
            start = cur;
        }
 else {
            Book* temp = start;
            while (temp->next != NULL)
                temp = temp->next;
            temp->next = cur;
            cur->prev = temp;
        }
        cout << "Book Inserted Successfully!\n";
    }
    void search() {
        if (start == NULL) {
            cout << "List Empty\n";
            return;
        }
        int key;
        cout << "Enter Book ID to Search: ";
        cin >> key;
        Book* temp = start;
        while (temp != NULL) {
            if (temp->id == key) {
                cout << "\nBook Found:\n";
                cout << "ID: " << temp->id
                     << "  Title: " << temp->title
                     << "  Author: " << temp->author
                     << "  Year: " << temp->year << endl;
                return;
            }
            temp = temp->next;
        }
        cout << "Book Not Found\n";
    }

    void modify() {
        if (start == NULL) {
            cout << "List Empty\n";
            return;
        }
        int key;
        cout << "Enter Book ID to Modify: ";
        cin >> key;
        Book* temp = start;
        while (temp != NULL) {
            if (temp->id == key) {
                cout << "Enter New Title: ";
                cin >> temp->title;
                cout << "Enter New Author: ";
                cin >> temp->author;
                cout << "Enter New Year: ";
                cin >> temp->year;
                cout << "Record Updated Successfully!\n";
                return;
            }
            temp = temp->next;
        }
        cout << "Book Not Found\n";
    }
    void display() {
        if (start == NULL) {
            cout << "No Records Available\n";
            return;
        }
        Book* temp = start;
        int count = 0;
        cout << "\nID   Title   Author   Year\n";
        while (temp != NULL) {
            cout << temp->id << "   "
                 << temp->title << "   "
                 << temp->author << "   "
                 << temp->year << endl;
            count++;
            temp = temp->next;
        }
        cout << "Total Books = " << count << endl;
    }
};
int main() {
    Library obj;
    int ch;
    do {
        cout << "\n1 Insert\n2 Search\n3 Modify\n4 Display\n0 Exit\nEnter Choice: ";
        cin >> ch;
        if (ch == 1) obj.insert();
        else if (ch == 2) obj.search();
        else if (ch == 3) obj.modify();
        else if (ch == 4) obj.display();

    } while (ch != 0);
    return 0;
}
 
 
 
Exercise 2.2 
Consider a scenario where a music app wants to manage its playlist of songs. Each song has a unique ID, title, artist name, and duration. The data is maintained in a doubly linked list, allowing for efficient traversal in both forward and backward directions. This is particularly useful for features like navigating through songs in a playlist and enabling users to easily move to the previous or next track. Create the following functions for the music playlist: 
1.	Insert: Add a new song record to the playlist. 
2.	Search: Find a song record using the title or artist name. 
3.	Modify: Update the details of an existing song record. 
4.	Display: Display all songs in the playlist, the total number of songs and total duration. 
5.	Play Next: Move to the next song in the playlist
6.	Play Previous: Move to the previous song in the playlist. 
Code
        
 #include <iostream>
using namespace std;
struct Song {
    int id, duration;
    string title, artist;
    Song* prev;
    Song* next;
};
class Playlist {
private:
    Song* start;
    Song* cur;
public:
    Playlist() {
        start = NULL;
        cur = NULL;
    }
    void insert() {
        Song* temp = new Song;

        cout << "Enter Song ID: ";
        cin >> temp->id;
        cout << "Enter Title: ";
        cin >> temp->title;
        cout << "Enter Artist: ";
        cin >> temp->artist;
        cout << "Enter Duration: ";
        cin >> temp->duration;

        temp->next = NULL;
        temp->prev = NULL;

        if (start == NULL) {
            start = cur = temp;
        } else {
            Song* p = start;
            while (p->next != NULL)
                p = p->next;

            p->next = temp;
            temp->prev = p;
        }

        cout << "Song Added\n";
    }
    void search() {
        string key;
        cout << "Enter Title or Artist: ";
        cin >> key;
        Song* temp = start;
        while (temp != NULL) {
            if (temp->title == key || temp->artist == key) {
                cout << "Found: " << temp->title << " " << temp->artist << endl;
                return;
            }
            temp = temp->next;
        }
        cout << "Song Not Found\n";
    }
    void modify() {
        int id;
        cout << "Enter Song ID: ";
        cin >> id;
        Song* temp = start;
        while (temp != NULL) {
            if (temp->id == id) {
                cout << "Enter New Title: ";
                cin >> temp->title;
                cout << "Enter New Artist: ";
                cin >> temp->artist;
                cout << "Enter New Duration: ";
                cin >> temp->duration;
                cout << "Updated Successfully\n";
                return;
            }
            temp = temp->next;
        }
        cout << "Song Not Found\n";
    }
    void display() {
        if (start == NULL) {
            cout << "Playlist Empty\n";
            return;
        }
        Song* temp = start;
        int total = 0, count = 0;
        cout << "\nID  Title  Artist  Duration\n";
        while (temp != NULL) {
            cout << temp->id << "   " << temp->title << "   "
                 << temp->artist << "   " << temp->duration << endl;
            total += temp->duration;
            count++;
            temp = temp->next;
        }
        cout << "Total Songs = " << count << endl;
        cout << "Total Duration = " << total << " sec\n";
    }
    void playNext() {
        if (cur != NULL && cur->next != NULL) {
            cur = cur->next;
            cout << "Now Playing: " << cur->title << endl;
        } else {
            cout << "No Next Song\n";
        }
    }
    void playPrevious() {
        if (cur != NULL && cur->prev != NULL) {
            cur = cur->prev;
            cout << "Now Playing: " << cur->title << endl;
        } else {
            cout << "No Previous Song\n";
        }
    }
};
int main() {
    Playlist obj;
    int ch;
    do {
        cout << "\n1 Insert\n2 Search\n3 Modify\n4 Display\n5 Next\n6 Previous\n0 Exit\nEnter Choice: ";
        cin >> ch;
        if (ch == 1) obj.insert();
        else if (ch == 2) obj.search();
        else if (ch == 3) obj.modify();
        else if (ch == 4) obj.display();
        else if (ch == 5) obj.playNext();
        else if (ch == 6) obj.playPrevious();
    } while (ch != 0);
    return 0;
}
 
