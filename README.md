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

struct Node { int data; struct Node* next; };
struct Node* head = NULL;

void traverse() {
    for (struct Node* t = head; t != NULL; t = t->next)
        printf("%d ", t->data);
    printf("\n");
}

void insert(int data) {
    struct Node* n = malloc(sizeof(struct Node));
    n->data = data; n->next = head; head = n;
}

void delete(int data) {
    struct Node *t = head, *prev = NULL;
    while (t && t->data != data) { prev = t; t = t->next; }
    if (!t) return;
    if (!prev) head = t->next;
    else prev->next = t->next;
    free(t);
}

int main() {
    insert(10); insert(20); insert(30);
    traverse();
    delete(20);
    traverse();
}

---------------------------------------------------------



5. Stack using Linked List
#include <stdio.h>
#include <stdlib.h>

struct Node { int data; struct Node* next; };
struct Node* top = NULL;

void push(int data) {
    struct Node* n = malloc(sizeof(struct Node));
    n->data = data; n->next = top; top = n;
    printf("Pushed: %d\n", data);
}

int pop() {
    if (!top) { printf("Stack empty\n"); return -1; }
    struct Node* t = top;
    int val = t->data;
    top = top->next; free(t);
    return val;
}

int peek() { return top ? top->data : -1; }
int isEmpty() { return top == NULL; }

int main() {
    push(10); push(20); push(30);
    printf("Peek: %d\n", peek());
    printf("Pop: %d\n", pop());
    printf("Empty: %s\n", isEmpty() ? "Yes" : "No");
}


---------------------------------------------------------




6. Queue using Linked List
#include <stdio.h>
#include <stdlib.h>

struct Node { int data; struct Node* next; };
struct Node *front = NULL, *rear = NULL;

void enqueue(int data) {
    struct Node* n = malloc(sizeof(struct Node));
    n->data = data; n->next = NULL;
    if (!rear) { front = rear = n; return; }
    rear->next = n; rear = n;
}

void dequeue() {
    if (!front) { printf("Queue empty\n"); return; }
    struct Node* t = front;
    printf("Dequeued: %d\n", t->data);
    front = front->next;
    if (!front) rear = NULL;
    free(t);
}

int frontVal() { return front ? front->data : -1; }
int isEmpty() { return front == NULL; }

int main() {
    enqueue(10); enqueue(20); enqueue(30);
    printf("Front: %d\n", frontVal());
    dequeue(); dequeue();
    printf("Empty: %s\n", isEmpty() ? "Yes" : "No");
}



---------------------------------------------------------





7. Doubly Linked List
#include <stdio.h>
#include <stdlib.h>

struct Node { int data; struct Node *prev, *next; };
struct Node* head = NULL;

void insertBegin(int data) {
    struct Node* n = malloc(sizeof(struct Node));
    n->data = data; n->prev = NULL; n->next = head;
    if (head) head->prev = n;
    head = n;
}

void deleteBegin() {
    if (!head) { printf("Empty\n"); return; }
    struct Node* t = head;
    head = head->next;
    if (head) head->prev = NULL;
    free(t);
}

void display() {
    for (struct Node* t = head; t != NULL; t = t->next)
        printf("%d <-> ", t->data);
    printf("NULL\n");
}

int main() {
    insertBegin(10); insertBegin(20); insertBegin(30);
    display();
    deleteBegin();
    display();
}



---------------------------------------------------------



8. Binary Tree (Insert + 3 Traversals)
#include <stdio.h>
#include <stdlib.h>

struct Node { int data; struct Node *left, *right; };

struct Node* insert(struct Node* root, int val) {
    if (!root) {
        struct Node* n = malloc(sizeof(struct Node));
        n->data = val; n->left = n->right = NULL;
        return n;
    }
    if (val < root->data) root->left  = insert(root->left,  val);
    else                  root->right = insert(root->right, val);
    return root;
}

void inorder(struct Node* r)   { if(r) { inorder(r->left);   printf("%d ", r->data); inorder(r->right);  } }
void preorder(struct Node* r)  { if(r) { printf("%d ", r->data); preorder(r->left);  preorder(r->right); } }
void postorder(struct Node* r) { if(r) { postorder(r->left); postorder(r->right); printf("%d ", r->data); } }

int main() {
    struct Node* root = NULL;
    int n, val;
    scanf("%d", &n);
    for (int i = 0; i < n; i++) { scanf("%d", &val); root = insert(root, val); }
    printf("Inorder:   "); inorder(root);
    printf("\nPreorder:  "); preorder(root);
    printf("\nPostorder: "); postorder(root);
}



---------------------------------------------------------



9. Graph DFS
#include <stdio.h>
#include <stdlib.h>
#define MAX 10

struct Node { int v; struct Node* next; };
struct Node* adj[MAX];
int visited[MAX];

void addEdge(int u, int v) {
    struct Node* n = malloc(sizeof(struct Node));
    n->v = v; n->next = adj[u]; adj[u] = n;
    n = malloc(sizeof(struct Node));
    n->v = u; n->next = adj[v]; adj[v] = n;
}

void dfs(int v) {
    printf("%d ", v); visited[v] = 1;
    for (struct Node* t = adj[v]; t; t = t->next)
        if (!visited[t->v]) dfs(t->v);
}

int main() {
    int n, e, u, v, start;
    scanf("%d %d", &n, &e);
    for (int i = 0; i < e; i++) { scanf("%d %d", &u, &v); addEdge(u, v); }
    scanf("%d", &start);
    printf("DFS: "); dfs(start);
}


---------------------------------------------------------



10. Social Network — BFS (Degrees of Separation)
#include <stdio.h>
#include <stdlib.h>
#define MAX 10

struct Node { int v; struct Node* next; };
struct Node* adj[MAX];
int dist[MAX];

void addEdge(int u, int v) {
    struct Node* n = malloc(sizeof(struct Node));
    n->v = v; n->next = adj[u]; adj[u] = n;
    n = malloc(sizeof(struct Node));
    n->v = u; n->next = adj[v]; adj[v] = n;
}

int bfs(int src, int dest) {
    int queue[MAX], front = 0, rear = 0;
    for (int i = 0; i < MAX; i++) dist[i] = -1;
    dist[src] = 0; queue[rear++] = src;
    while (front < rear) {
        int v = queue[front++];
        for (struct Node* t = adj[v]; t; t = t->next)
            if (dist[t->v] == -1) { dist[t->v] = dist[v] + 1; queue[rear++] = t->v; }
    }
    return dist[dest];
}

int main() {
    int n, e, u, v;
    scanf("%d %d", &n, &e);
    for (int i = 0; i < e; i++) { scanf("%d %d", &u, &v); addEdge(u, v); }
    int src, dest;
    scanf("%d %d", &src, &dest);
    int d = bfs(src, dest);
    if (d == -1) printf("No connection\n");
    else printf("Degrees of separation: %d\n", d);
}
