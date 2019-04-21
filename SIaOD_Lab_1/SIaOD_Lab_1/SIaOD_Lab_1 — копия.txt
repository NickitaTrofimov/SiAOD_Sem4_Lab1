#include "pch.h"
#include <iostream>
#include <stdlib.h>
#include <math.h>

using namespace std;

template<typename T>
class List
{
public:
	List();
	~List();

	void push_back(T data);
	int GetSize()
	{
		return Size;
	}
	T& operator[](const int index);

private:

	template<typename T>
	class Node
	{
	public:
		Node *pNext;
		T data;

		Node(T data=T(), Node *pNext=nullptr)
		{
			this->data = data;
			this->pNext = pNext;
		}

	};
	int Size;
	Node<T> *head; //Динамическая память
};

template<typename T>
List<T>::List()
{
	Size = 0;
	head = nullptr;
}

template<typename T>
List<T>::~List()
{

}

template<typename T>
void List<T>::push_back(T data)
{
	if (head == nullptr)
	{
		head = new Node<T>(data);
	}
	else
	{
		Node<T> *current = this->head;
		while (current->pNext != nullptr)
		{
			current = current->pNext;
		}
		current->pNext = new Node<T>(data);
	}
	Size++;
}

template<typename T>
T & List<T>::operator[](const int index)
{

	int counter = 0;
	Node<T> *current = this->head;
	while (current != nullptr)
	{
		if (counter == index)
		{
			return current->data;
		}
		current = current->pNext;
		counter++;
	}
}

int main()
{
	List<int> lst1;
	List<int> lst2;

	cout << "Enter number of elements in first and second lists: " << endl;
	int numbersCount;
	cin >> numbersCount;

	int var;

	for (int i = 0; i < numbersCount; i++)
	{
		var = rand() % 100 + 1;
		lst1.push_back(var);
	}

	int cup = 0;
	for (int k = 0; k < numbersCount; k++) {
		for (int j = 0; j < numbersCount- 1; j++) {
			if (lst1[j] <= lst1[j + 1]) {
				cup = lst1[j];
				lst1[j] = lst1[j + 1];
				lst1[j + 1] = cup;
			}
		}
	}

	for (int i = 0; i < numbersCount; i++)
	{
		var = rand() % 100 + 1;
		lst2.push_back(var);
	}

	cup = 0;
	for (int k = 0; k < numbersCount; k++) {
		for (int j = 0; j < numbersCount - 1; j++) {
			if (lst2[j] <= lst2[j + 1]) {
				cup = lst2[j];
				lst2[j] = lst2[j + 1];
				lst2[j + 1] = cup;
			}
		}
	}

	List<int> lst3;

	for (int i = 0; i < numbersCount; i++)
	{
		lst3.push_back(lst1[i]);
	}
	for (int i = 0; i < numbersCount; i++)
	{
		lst3.push_back(lst2[i]);
	}

	cup = 0;
	for (int k = 0; k < numbersCount * 2; k++) {
		for (int j = 0; j < numbersCount * 2 - 1; j++) {
			if (lst3[j] <= lst3[j + 1]) {
				cup = lst3[j];
				lst3[j] = lst3[j + 1];
				lst3[j + 1] = cup;
			}
		}
	}

	for (int i = 0; i < lst1.GetSize(); i++)
	{
		cout << lst1[i] << " ";
	}
	cout << endl;

	for (int i = 0; i < lst2.GetSize(); i++)
	{
		cout << lst2[i] << " ";
	}
	cout << endl;

	cout << "United lists: " << endl;

	for (int i = 0; i < lst3.GetSize(); i++)
	{
		cout << lst3[i] << " ";
	}
	cout << endl;

	return(0);
}