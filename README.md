#include<bits/stdc++.h>
using namespace std;

#define endl             '\n'
#define int              long long


struct book {
	string title;
	string author;
	string genre;
	int id;
	struct book* next;
};

struct book* head = nullptr;


void insertBook() {

	int idd;
	string name, writer, cat;
	cin >> name >> writer >> cat >> idd;

	struct book* newNode = new book;

	newNode->title = name;
	newNode->author = writer;
	newNode->genre = cat;
	newNode->id = idd;
	newNode->next = nullptr;

	if(head == nullptr) {
		head = newNode;
		return;
	}

	struct book* temp = head;
	while(temp->next != nullptr) {
		temp = temp->next;
	}
	temp->next = new book;
	temp->next = newNode;

}

void printBookAll() {
	struct book* temp  = head;
	while(temp != nullptr) {
		cout << temp->title << " " << temp->author << " " << temp->genre << " " << temp->id << endl;

		temp = temp -> next;
	}
}


void del(int idd) {

    if(head->id == idd) {
            struct book* por = head->next;
            free(head);
            head = por;
            return;
    }


    struct book* temp  = head;
    struct book* prv = head;
	while(temp != nullptr) {
        if(temp->id == idd) {
            struct book* por = temp->next;
            free(temp);
            prv->next = por;
            return;
        }
        prv = temp;
		temp = temp -> next;
	}

	cout << "Book not delete operation is not possible" << idd << endl;
	return;
}


void search(int idd) {
    struct book* temp  = head;
	while(temp != nullptr) {
        if(temp->id == idd) {
            cout << "Book found : Book id = " << idd << endl;
            cout << "Book info : " << endl;
            cout << "name = " << temp->title << endl;
            return;
        }
		temp = temp -> next;
	}

	cout << "Book not found of id " << idd << endl;
	return;
}

int32_t main(){

    cout << "Enter total book you want to insert " << endl;
    int n; cin >> n;

    for(int i = 0; i < n; i++) {
        cout << "Enter book title author genre and id : ";
        insertBook();
        cout << endl;
    }


    printBookAll();


    cout << "Which book you want to search enter book id : ";
    cin >> n;
    search(n);

    cout << "Which book you want to delete enter book id : ";
    cin >> n;
    del(n);

    cout << "After all the operation full book list : " << endl;
    printBookAll();

}
