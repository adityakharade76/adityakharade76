#include <iostream>
using namespace std;

// Node class that holds data and the next pointer
template <typename T>
class Node {
public:
    T data;      // Data of the node
    Node* next;  // Pointer to the next node

    // Constructor to initialize a node
    Node(T val) : data(val), next(nullptr) {}
};

// LinkedList class for managing the list
template <typename T>
class LinkedList {
private:
    Node<T>* head;  // Head of the list

public:
    // Constructor to initialize the linked list
    LinkedList() : head(nullptr) {}

    // Destructor to free all allocated memory
    ~LinkedList() {
        while (head != nullptr) {
            Node<T>* temp = head;
            head = head->next;
            delete temp;
        }
    }

    // Method to add an element at the end of the list
    void add(T value) {
        Node<T>* newNode = new Node<T>(value);
        if (head == nullptr) {
            head = newNode;
        } else {
            Node<T>* temp = head;
            while (temp->next != nullptr) {
                temp = temp->next;
            }
            temp->next = newNode;
        }
    }

    // Method to display all elements in the list
    void display() {
        if (head == nullptr) {
            cout << "List is empty!" << endl;
            return;
        }
        Node<T>* temp = head;
        while (temp != nullptr) {
            cout << temp->data << " ";
            temp = temp->next;
        }
        cout << endl;
    }

    // Method to delete the first occurrence of a value
    void remove(T value) {
        if (head == nullptr) {
            cout << "List is empty!" << endl;
            return;
        }

        if (head->data == value) {
            Node<T>* temp = head;
            head = head->next;
            delete temp;
            return;
        }

        Node<T>* current = head;
        while (current->next != nullptr && current->next->data != value) {
            current = current->next;
        }

        if (current->next == nullptr) {
            cout << "Value not found!" << endl;
        } else {
            Node<T>* temp = current->next;
            current->next = current->next->next;
            delete temp;
        }
    }
};

// Main function to demonstrate the linked list operations
int main() {
    LinkedList<int> list;

    // Adding elements to the list
    list.add(10);
    list.add(20);
    list.add(30);
    list.add(40);

    cout << "Current List: ";
    list.display();

    // Removing an element
    cout << "Removing 20 from the list..." << endl;
    list.remove(20);
    
    cout << "List after removal: ";
    list.display();

    // Removing an element that does not exist
    cout << "Removing 50 from the list..." << endl;
    list.remove(50);
    
    return 0;
}
