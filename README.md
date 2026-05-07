# C

1. Largest and Smallest in Array
#include <stdio.h>
int main() {
    int n;
    printf("Enter the array size: ");
    scanf("%d", &n);
    int arr[n];
    printf("Enter the number to be inserted in the array:");
    for (int i = 0; i < n; i++)
    scanf("%d", &arr[i]);
    
    int max = arr[0], min = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] > max) max = arr[i];
        if (arr[i] < min) min = arr[i];
    }
    printf("Largest = %d, Smallest = %d\n", max, min);
}


---------------------------------------------------------



2. Factorial using Recursion
#include <stdio.h>
int fact(int n){
    return(n==0)?1: n*fact(n-1);
}
int main(){
    int n;
    printf("Enter a number: ");
    scanf("%d", &n);
    printf("Factorial of %d is %d", n, fact(n));
}


---------------------------------------------------------


3. Nth Fibonacci using Recursion
#include <stdio.h>
int fib(int n) {
    return(n<=1) ? n : fib(n-1)+fib(n-2);
    }
int main(){
    int n;
    printf("Enter a non negative number: ");
    scanf("%d", &n);
    if (n<0){
        printf("Invalid input");
    }else{
        printf("Fibb of %d is %d", n, fib(n));
}}



---------------------------------------------------------
---------------------------------------------------------
---------------------------------------------------------



4. Singly Linked List (Insert, Delete, Traverse)
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

struct Node* head = NULL;

void traverse() {
    struct Node* temp = head;
    printf("List: ");
    while (temp != NULL) {
        printf("%d ", temp->data);
        temp = temp->next;
    }
    printf("\n");
}

void insert_at_beginning(int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
        if (newNode == NULL) {
        printf("Memory allocation failed\n");
        return;
    }
    newNode->data = data;
    newNode->next = head;
    head = newNode;

    traverse();
}

void delete_at_beginning() {
    struct Node* temp;

    if (head == NULL) {
        printf("List is empty, nothing to delete\n");
        return;
    }
    temp = head;
    head = head->next;
    free(temp);

    traverse();
}
int main() {
    insert_at_beginning(30);
    insert_at_beginning(20);
    insert_at_beginning(10);
    delete_at_beginning();
    return 0;
}

---------------------------------------------------------


5. Stack using Linked List
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

struct Node* head = NULL;

void print() {
    struct Node* temp = head;
    while (temp != NULL) {
        printf("%d ", temp->data);
        temp = temp->next;
    }
    printf("NULL\n");
}

void push(int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
        if (newNode == NULL) {
        printf("Memory allocation failed\n");
        return;
    }
    newNode->data = data;
    newNode->next = head;
    head = newNode;
    print();
}

void pop() {
    struct Node* temp;

    if (head == NULL) {
        printf("Stack is empty, nothing to delete\n");
        return;
    }
else{
printf("Poped element = %d\n", head->data);
    temp = head;
    head = head->next;
    free(temp);
    pop();
}
int main() {
    push(30);
    push(20);
    push(10);
    pop();
    return 0;
}


---------------------------------------------------------




6. Queue using Linked List
#include<stdio.h>
#include<stdlib.h>
struct node
{
    int data;
    struct node *next;
};
struct node *front = NULL, *rear = NULL;
void enqueue(int val)
{
    struct node *newNode = malloc(sizeof(struct node));
    newNode->data = val;
    newNode->next = NULL;
    if(front == NULL && rear == NULL)
              front = rear = newNode;
    else
    {
                rear->next = newNode;
        rear = newNode;
    }
}

void dequeue()
{
       struct node *temp;
    if(front == NULL)
         printf("Queue is Empty. Unable to perform dequeue\n");
    else
    {
                temp = front;
               front = front->next;
              if(front == NULL)
            rear = NULL;
         free(temp);
    }

}

void printList()
{
    struct node *temp = front;
    while(temp)
    {
        printf("%d->",temp->data);
        temp = temp->next;
    }
    printf("NULL\n");
}
int main()
{
    enqueue(10);
    enqueue(20);
    enqueue(30);
    printf("Queue :");
    printList();
    dequeue();
    printf("After dequeue the new Queue :");
    printList();
    dequeue();
    printf("After dequeue the new Queue :");
    printList();
    return 0;
}


---------------------------------------------------------





7. Doubly Linked List
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node *prev;
    struct Node *next;
};

struct Node *head = NULL;

void insertBegin(int data) {
    struct Node *newNode = (struct Node *)malloc(sizeof(struct Node));

    newNode->data = data;
    newNode->prev = NULL;
    newNode->next = head;

    if (head != NULL)
        head->prev = newNode;

    head = newNode;
}

void deleteBegin() {
    struct Node *temp;

    if (head == NULL) {
        printf("List is empty. Deletion not possible.\n");
        return;
    }

    temp = head;
    head = head->next;

    if (head != NULL)
        head->prev = NULL;

    free(temp);
}

void display() {
    struct Node *temp = head;

    if (head == NULL) {
        printf("List is empty.\n");
        return;
    }

    while (temp != NULL) {
        printf("%d <-> ", temp->data);
        temp = temp->next;
    }

    printf("NULL\n");
}

int main() {
    insertBegin(10);
    insertBegin(20);
    insertBegin(30);

    printf("After insertion:\n");
    display();

    deleteBegin();

    printf("After deletion:\n");
    display();

    return 0;
}


---------------------------------------------------------



8. Binary Tree (Insert + 3 Traversals)
#include <stdio.h>
#include <stdlib.h>

struct node
{
    int data;
    struct node *left;
    struct node *right;
};

struct node* createNode(int value)
{
    struct node* newnode = (struct node*)malloc(sizeof(struct node));
    newnode->data = value;
    newnode->left = NULL;
    newnode->right = NULL;
    return newnode;
}

struct node* insert(struct node* root, int value)
{
    if(root == NULL)
        return createNode(value);

    if(value < root->data)
        root->left = insert(root->left, value);
    else
        root->right = insert(root->right, value);

    return root;
}


void inorder(struct node* root)
{
    if(root != NULL)
    {
        inorder(root->left);
        printf("%d ", root->data);
        inorder(root->right);
    }
}
void preorder(struct node* root)
{
    if(root != NULL)
    {
        printf("%d ", root->data);
        preorder(root->left);
        preorder(root->right);
    }
}
void postorder(struct node* root)
{
    if(root != NULL)
    {
        postorder(root->left);
        postorder(root->right);
        printf("%d ", root->data);
    }
}
int main()
{
    struct node* root = NULL;
    int n, value, i;

    printf("Enter number of nodes: ");
    scanf("%d", &n);

    for(i=0; i<n; i++)
    {
        printf("Enter value: ");
        scanf("%d", &value);
        root = insert(root, value);
    }
    printf("\nInorder Traversal: ");
    inorder(root);
    printf("\nPreorder Traversal: ");
    preorder(root);
    printf("\nPostorder Traversal: ");
    postorder(root);
    return 0;
}


---------------------------------------------------------



9. Graph DFS
#include <stdio.h>
#include <stdlib.h>

#define MAX 10

// Node structure for adjacency list
struct Node {
    int vertex;
    struct Node* next;
};

struct Node* adjList[MAX];
int visited[MAX];
int n;

// Create new node
struct Node* createNode(int v) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->vertex = v;
    newNode->next = NULL;
    return newNode;
}

// Add edge (undirected graph)
void addEdge(int src, int dest) {
    struct Node* newNode = createNode(dest);
    newNode->next = adjList[src];
    adjList[src] = newNode;

    newNode = createNode(src);
    newNode->next = adjList[dest];
    adjList[dest] = newNode;
}

// DFS function
void dfs(int v) {
    printf("%d ", v);
    visited[v] = 1;

    struct Node* temp = adjList[v];
    while (temp != NULL) {
        int adjVertex = temp->vertex;
        if (visited[adjVertex] == 0) {
            dfs(adjVertex);
        }
        temp = temp->next;
    }
}

int main() {
    int edges, u, v, start;

    printf("Enter number of vertices: ");
    scanf("%d", &n);

    // Initialize
    for (int i = 0; i < n; i++) {
        adjList[i] = NULL;
        visited[i] = 0;
    }

    printf("Enter number of edges: ");
    scanf("%d", &edges);

    printf("Enter edges (u v):\n");
    for (int i = 0; i < edges; i++) {
        scanf("%d %d", &u, &v);
        addEdge(u, v);
    }

    printf("Enter starting vertex: ");
    scanf("%d", &start);

    printf("DFS Traversal: ");
    dfs(start);

    return 0;
} 



---------------------------------------------------------



10. Social Network — BFS (Degrees of Separation)
#include <stdio.h>
#include <stdlib.h>

#define MAX 10

// Node structure
struct Node {
    int vertex;
    struct Node* next;
};

struct Node* adjList[MAX];
int visited[MAX];
int queue[MAX];
int front = -1, rear = -1;
int n;

// Create node
struct Node* createNode(int v) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->vertex = v;
    newNode->next = NULL;
    return newNode;
}

// Add edge (undirected)
void addEdge(int src, int dest) {
    struct Node* newNode = createNode(dest);
    newNode->next = adjList[src];
    adjList[src] = newNode;

    newNode = createNode(src);
    newNode->next = adjList[dest];
    adjList[dest] = newNode;
}

// Queue operations
void enqueue(int v) {
    if (rear == MAX - 1) return;
    if (front == -1) front = 0;
    queue[++rear] = v;
}

int dequeue() {
    if (front == -1 || front > rear) return -1;
    return queue[front++];
}

// BFS function
void bfs(int start) {
    enqueue(start);
    visited[start] = 1;

    while (front <= rear) {
        int v = dequeue();
        printf("%d ", v);

        struct Node* temp = adjList[v];
        while (temp != NULL) {
            int adjVertex = temp->vertex;

            if (visited[adjVertex] == 0) {
                enqueue(adjVertex);
                visited[adjVertex] = 1;
            }
            temp = temp->next;
        }
    }
}

int main() {
    int edges, u, v, start;

    printf("Enter number of vertices: ");
    scanf("%d", &n);

    // Initialize
    for (int i = 0; i < n; i++) {
        adjList[i] = NULL;
        visited[i] = 0;
    }

    printf("Enter number of edges: ");
    scanf("%d", &edges);

    printf("Enter edges (u v):\n");
    for (int i = 0; i < edges; i++) {
        scanf("%d %d", &u, &v);
        addEdge(u, v);
    }

    printf("Enter starting vertex: ");
    scanf("%d", &start);

    printf("BFS Traversal: ");
    bfs(start);

    return 0;
}
