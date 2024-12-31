# Data Structure
## Linked List :
A **linked list** is a linear data structure similar to an array. However, unlike arrays, elements are not stored in a particular memory location or index. Rather each element is a separate object that contains a pointer or a link to the next object in that list.

Each element (commonly called nodes) contains two items: the data stored and a link to the next node. The data can be any valid data type. You can see this illustrated in the diagram below.

The entry point to a linked list is called the head. The head is a reference to the first node in the linked list. The last node on the list points to null. If a list is empty, the head is a null reference.

![image](./illustrations/W20D04/LinkedList.png)


### An advantage of Linked Lists
- **Insertion and Deletion**
Insertion and deletion of nodes are really easier. Unlike array here we don’t have to shift elements after insertion or deletion of an element. In linked list we just have to update the address present in next pointer of a node.

- **No Memory Wastage**
As size of linked list can increase or decrease at run time so there is no memory wastage. In case of array there is lot of memory wastage, like if we declare an array of size 10 and store only 6 elements in it then space of 4 elements are wasted. There is no such problem in linked list as memory is allocated only when required.

- **Implementation**
Data structures such as stack and queues can be easily implemented using linked list.

### Disadvantages of Linked Lists
- **Memory Usage**
More memory is required to store elements in linked list as compared to array. Because in linked list each node contains a pointer and it requires extra memory for itself.

- **Traversal**
Elements or nodes traversal is difficult in linked list. We can not randomly access any element as we do in array by index. For example if we want to access a node at position n then we have to traverse all the nodes before it. So, time required to access a node is large.

- **Reverse Traversing**
In linked list reverse traversing is really difficult. In case of doubly linked list its easier but extra memory is required for back pointer hence wastage of memory.

### Types of Linked Lists
There are three types of linked lists:

- **Singly Linked Lists**: Each node contains only one pointer to the next node. This is what we have been talking about so far.
- **Doubly Linked Lists**: Each node contains two pointers, a pointer to the next node and a pointer to the previous node.
- **Circular Linked Lists**: Circular linked lists are a variation of a linked list in which the last node points to the first node or any other node before it, thereby forming a loop.

### Some LinkedList methods
Next up, we will implement four helper methods for the linked list. They are:

- **size()**:This method returns the number of nodes present in the linked list.
- **clear()**:This method empties out the list.
- **getLast()**:This method returns the last node of the linked list.
- **getFirst()**:This method returns the first node of the linked list.