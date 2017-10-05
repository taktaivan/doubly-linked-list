# structures

// Doublylinkedlist

#include "stdafx.h"
#include "iostream"

using namespace std;

struct node_s {
	int data;
	node_s*prev = nullptr;
	node_s*next = nullptr;
};

struct list_s {
	int size = 0;
	node_s*first = nullptr;
	node_s*last = nullptr;
};

void add_start(int new_data, list_s* list);
void add_end(int new_data, list_s* list);
void del(int value, list_s* list);
void insert(int useful_data, int num, list_s* list);
void sort_1();

int main()
{
	list_s* list = new list_s;
	int n;
	cout << "Enter the size of the list." << endl;
	cin >> n;
	for (int i = 0; i < n; i++) {
		int new_data;
		cin >> new_data;
		add_start(new_data, list);
	}
	int m;
	cout << "How many items need to be removed from the end of the list?" << endl;
	cin >> m;
	for (int i = 0; i < m; i++) {
		int new_data;
		cin >> new_data;
		add_end(new_data, list);
	}
	cout << "Size of list: ";
	cout << list->size << endl;
	cout << "Enter the number of the list item, after which the new element will be inserted." << endl;
	int num, new_data; //номер не должен превышать размера списка
	cin >> num >> new_data;
	insert(new_data, num, list);
	cout << list->size << endl;
	int value;
	cout << "Enter the value of the number that is stored in the item you want to delete." << endl;
	cin >> value;
	del(value, list);
	cout << list->size << endl;
	system("pause");
	return 0;
}

void add_start(int new_data, list_s* list) {
	node_s* node = new node_s;
	node->data = new_data;
	if (list->size == 0) 
	{
		list->first = node;
		list->last = list->first;
	}
	else
	{
		node->next = list->first;
		list->first = node;
		node->next->prev = node; 
	}
	list->size++;
}

void add_end(int new_data, list_s* list) {
	node_s* node = new node_s;
	node->data = new_data;
	if (list->size == 0) {
		list->first = node;
		list->last = list->first;
	}
	else
	{
		node->prev = list->last;
		list->last->next = node;
		list->last = node;
	}
	list->size++;
}

void del(int value, list_s* list) {
	node_s* cell = list->first;
	int counter = 1;
	while (counter <= list->size) {
		if (cell->data == value) {
			if (cell == list->last)
				cell->prev->next = nullptr;
			else {
				cell->prev->next = cell->next;
				cell->next->prev = cell->prev;
			}
			delete cell;
			list->size--;
			break;
		}
		counter++;
		cell = cell->next;
	}
}

void insert(int new_data, int number, list_s* list) {
	node_s* it = list->first;
	int counter = 1;
	while (counter < list->size) {
		if (counter == number) {
			node_s* node = new node_s;
			node->data = new_data;
			node->prev = it;
			node->next = it->next;
			it->next->prev = node;
			it->next = node;
			list->size++;
			break;
		}
		counter++;
		it = it->next;
	}
}

void sort_1(list_s* list) {
	node_s* it = list->first;
}
