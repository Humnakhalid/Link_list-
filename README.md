# Link_list-
#include <iostream>
using namespace std ;
// Node structure for the linked list
struct Node {
    int data;
    Node* next;
    
    // Constructor to initialize node
    Node(int value) : data(value), next(nullptr) {}
};

// Linked list class
class LinkedList {
private:
    Node* head;

public:
    // Constructor to initialize an empty linked list
    LinkedList() : head(nullptr) {}

    // Function to search for a value in the linked list
    bool search(int value) {
        Node* current = head;
        while (current != nullptr) {
            if (current->data == value) {
                return true; // Value found
            }
            current = current->next;
        }
        return false; // Value not found
    }

    // Function to update the value at position n
    void updateAtPosition(int n, int newValue) {
        Node* current = head;
        for (int i = 1; i < n && current != nullptr; ++i) {
            current = current->next;
        }

        if (current != nullptr) {
            current->data = newValue;
            cout << "Updated value at position " << n << " to " << newValue << endl;
        } else {
            cout << "Position " << n << " not found." << endl;
        }
    }

    // Function to insert a value at position n
    void insertAtPosition(int n, int value) {
        Node* newNode = new Node(value);

        if (n == 1) {
            newNode->next = head;
            head = newNode;
        } else {
            Node* current = head;
            for (int i = 1; i < n - 1 && current != nullptr; ++i) {
                current = current->next;
            }

            if (current != nullptr) {
                newNode->next = current->next;
                current->next = newNode;
            } else {
                cout << "Position " << n << " not found. Insertion failed." << endl;
                delete newNode;
            }
        }

        cout << "Inserted value " << value << " at position " << n << endl;
    }

    // Function to delete the first node in the linked list
    void deleteFromBeginning() {
        if (head != nullptr) {
            Node* temp = head;
            head = head->next;
            delete temp;
            cout << "Deleted from the beginning." << endl;
        } else {
            cout << "List is empty. Deletion failed." << endl;
        }
    }

    // Function to delete the last node in the linked list
    void deleteFromEnd() {
        if (head != nullptr) {
            if (head->next == nullptr) {
                delete head;
                head = nullptr;
            } else {
                Node* current = head;
                while (current->next->next != nullptr) {
                    current = current->next;
                }
                delete current->next;
                current->next = nullptr;
            }
            cout << "Deleted from the end." << endl;
        } else {
            cout << "List is empty. Deletion failed." << endl;
        }
    }

    // Function to delete the node at position n
    void deleteAtPosition(int n) {
        if (n == 1) {
            deleteFromBeginning();
        } else {
            Node* current = head;
            for (int i = 1; i < n - 1 && current != nullptr; ++i) {
                current = current->next;
            }

            if (current != nullptr && current->next != nullptr) {
                Node* temp = current->next;
                current->next = current->next->next;
                delete temp;
                cout << "Deleted from position " << n << endl;
            } else {
                cout << "Position " << n << " not found. Deletion failed." << endl;
            }
        }
    }

    // Function to display the linked list
    void display() {
        Node* current = head;
        while (current != nullptr) {
            std::cout << current->data << " ";
            current = current->next;
        }
        cout << endl;
    }
};

// Main function
int main() {
    LinkedList list;

    // Inserting values into the linked list
    list.insertAtPosition(1, 70);
    list.insertAtPosition(2, 26);
    list.insertAtPosition(3, 39);

    // Displaying the initial linked list
    cout << "Initial Linked List: ";
    list.display();

    // Searching for a value
    if (list.search(20)) {
    cout << "Value 20 found in the list." << endl;
    } else {
        cout << "Value 20 not found in the list." << endl;
    }

    // Updating a value at position 2
    list.updateAtPosition(2, 25);

    // Displaying the updated linked list
    cout << "Updated Linked List: ";
    list.display();

    // Deleting from the beginning
    list.deleteFromBeginning();

    // Displaying the linked list after deletion
    cout << "Linked List after deleting from the beginning: ";
    list.display();

    // Deleting from the end
    list.deleteFromEnd();

    // Displaying the linked list after deletion
    cout << "Linked List after deleting from the end: ";
    list.display();

    // Deleting from position 2
    list.deleteAtPosition(2);

    // Displaying the final linked list
    cout << "Final Linked List: ";
    list.display();

    return 0;
}

