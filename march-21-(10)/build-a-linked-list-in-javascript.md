In this post , I will be showing how we can build a singly linked list data structure using javascript language.We will also learn all operations on it.
![linked-lists.png](https://res.cloudinary.com/dh1srz69c/image/upload/v1614713918/linked_lists_ca0b13a95f.png)
# 🧐Overview
In a singly linked list each item points to its successor.Each item in a linked list is called as a node.There is a head node in each linked list which points to its first node.The last node of linked list points to null.

# Node Class
First we will create a blue print for our node of linked list.We will create a Node Class in javascript which will have two properties-
- data  - which will store data of node
- next  - which will points to next node 


```js
class Node {
	constructor(data, next = null) {
		this.data = data;
		this.next = next;
	}
}

```

# Linked List Class
Now we will create a actual linked list class which will have two properties - 
- head -which will points to the first node of linked list
- size  -which represents the number of nodes present in the list

```js
class LinkedList {
	constructor() {
		this.head = null;
		this.size = 0;
	}
}

```
# Operations
Now , we will create some member functions in LinkedList class to perform various operations on linked list.
### (1) insertFirst() 
 To insert a  node at first position of list.\
Here we will simply point the head to new node and next of new node to previous head node . At the end , we will increment the size of list by 1. 
```js
	// Insert Node at first position
	insertFirst(data) {
		this.head = new Node(data, this.head);
		this.size++;
	}
```

### (2) insertLast() 
 To insert a  node at last position of list.\
Here we will have 2 case\
1.If list is empty - then we will simply point the head of node to new node.\
2. if list is not empty - then we will traverse the whole list and then point the next of last node to new node.\
```js
	// Insert Node at last position
	insertLast(data) {
		const newLast = new Node(data);

		// Check if list is empty then last node is first node which will be head
		if (!this.head) {
			this.head = newLast;
		}
		else {
			// if list is not empty traverse to last node
			let last = this.head;
			while (last.next) {
				last = last.next;
			}
			last.next = newLast;
		}
		this.size++;
	}
```

### (3) insertAt() 
 To insert a  node at given index.\
Here also we will have 2 case\
1.If index is 0 - then we will simply point the head of node to new node.\
2. if index is not 0 - then we will create two variables to track previous and current node and will traverse the list upto given index and and then point the next of previous node to new node and next of new node to current node.
```js
// insert a node at a particular index
	insertAt(data, index) {
		// check if index is valid
		if (index >= 0 && index < this.size) {
			// if first index
			if (index === 0) {
				this.head = new Node(data, this.head);
				return;
			}

			const node = new Node(data);
			let current, previous;

			current = this.head;
			let count = 0;

			while (count < index) {
				previous = current;
				count++;
				current = current.next;
			}

			node.next = current;
			previous.next = node;

			this.size++;
		}
		else {
			console.log('You have entered an invalid index!!');
		}
	}

```

### (4) removeAt() 
 To remove a node at given index.\
Here also we will have 2 cases as in (3)\
1.If index is 0 - then we will simply point the head to next of previous head node.\
2. if index is not 0 - then we will create two variables to track previous and current node and will traverse the list upto given index and and then point the next of previous node to  next  current node.
```js
	// remove a  node at a particular index

	removeAt(index) {
		let current = this.head;
		let previous;
		let count = 0;
		// check if index is valid
		if (index >= 0 && index < this.size) {
			// if first index
			if (index === 0) {
				this.head = current.next;
			}
			else {
				while (count < index) {
					previous = current;
					current = current.next;
					count++;
				}
				previous.next = current.next;
			}
			this.size--;
		}
		else {
			console.log('You have entered an invalid index!!');
		}
	}

```

### (5) getAt() 
 To get  data of a node at given index.\
Here also we will have 2 cases as in (3)\
1.If index is 0 - then we will simply return the data of head node.\
2. if index is not 0 - traverse upto given index in linked list and then return the data of current node.
```js
	getAt(index) {
		let current = this.head;
		let count = 0;
		// check if index is valid
		if (index >= 0 && index < this.size) {
			// if first index
			if (index === 0) {
				// console.log(this.data);
				return this.head.data;
			}

			while (count != index) {
				current = current.next;
				count++;
			}

			// console.log(current.data);
			return current.data;
		}
		else {
			console.log('You have entered an invalid index!!');
		}
	}
```

### (6) clearList() 
 To clear (empty) a whole list.\
Here we will simply point head of list to null and size to zero then list will become empty
```js
	// clear a whole list
	clearList() {
		this.head = null;
		this.size = 0;
	}
```

### (7) printListData() 
 To print data of all nodes in list.\
Here we will simply traverse to whole list and print data of each node.
```js
// print all data in list
	printListData() {
		let current = this.head;

		if (!this.head) {
			console.log('The list is empty!!');
			return;
		}

		while (current != null) {
			console.log(current.data);
			current = current.next;
		}
	}
```

# Driver Code
Now we will see code for how we can create an instance of this linked list and perform various operations onto it.By running below code with node or in browser
```js
// index.js
const li = new LinkedList();
li.insertLast(200);
li.insertFirst(100);
li.insertAt(300, 1);
li.insertLast(400);
li.printListData();
console.log(`The size of list is ${li.size}`);
console.log(li.getAt(2));
li.removeAt(1);
console.log(`The size of list is ${li.size}`);
li.clearList();
console.log(`The size of list is ${li.size}`);
```
we will get output as:
> 100\
300\
200\
400\
The size of list is 4\
200\
The size of list is 3\
The size of list is 0



I hope 😇 all of you understand how to build linked list with javascript. Thank you for reading.