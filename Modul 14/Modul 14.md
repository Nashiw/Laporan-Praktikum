# <h1 align="center">Laporan Praktikum Modul 14 <br>GRAPH</h1>
<p align="center">Nashir Khoirul Huda - 103112400168</p>

## Dasar Teori
Graph adalah struktur data non-linear yang merepresentasikan himpunan objek (disebut vertex atau node) yang terhubung oleh sisi (edge) yang dapat memiliki arah (pada directed graph) maupun tidak (pada undirected graph). Dalam implementasinya, graph dapat direpresentasikan menggunakan adjacency matrix atau adjacency list (multilist), dengan adjacency list sering dipilih karena efisiensi memorinya untuk graph yang sparse. Algoritma dasar pada graph meliputi penelusuran seperti Breadth-First Search (BFS) yang menjelajahi graph per level dan Depth-First Search (DFS) yang menjelajahi secara mendalam, serta topological sort untuk mengurutkan vertex pada directed acyclic graph berdasarkan dependensi antar node.

## Guided
#### graf.h
```c++
#ifndef GRAF_H_INCLUDED
#define GRAF_H_INCLUDED

#include <iostream>
using namespace std;

typedef char infoGraph;

struct ElmNode;
struct ElmEdge;

typedef ElmNode *adrNode;
typedef ElmEdge *adrEdge;

struct ElmNode
{
    infoGraph info;
    int visited;
    adrEdge firstEdge;
    adrNode next;
};

struct ElmEdge
{
    adrNode node;
    adrEdge next;
};

struct Graph
{
    adrNode first;
};

// PRIMITIF GRAPH
void CreateGraph(Graph &G);
adrNode AllocateNode(infoGraph X);
adrEdge AllocateEdge(adrNode N);

void InsertNode(Graph &G, infoGraph X);
adrNode FindNode(Graph G, infoGraph X);

void ConnectNode(Graph &G, infoGraph A, infoGraph B);

void PrintInfoGraph(Graph G);

// Traversal
void ResetVisited(Graph &G);
void PrintDFS(Graph &G, adrNode N);
void PrintBFS(Graph &G, adrNode N);

#endif
```
#### graf.cpp
```c++
#include "graf.h"
#include <queue>
#include <stack>

void CreateGraph(Graph &G)
{
    G.first = NULL;
}

adrNode AllocateNode(infoGraph X)
{
    adrNode P = new ElmNode;
    P->info = X;
    P->visited = 0;
    P->firstEdge = NULL;
    P->next = NULL;
    return P;
}

adrEdge AllocateEdge(adrNode N)
{
    adrEdge P = new ElmEdge;
    P->node = N;
    P->next = NULL;
    return P;
}

void InsertNode(Graph &G, infoGraph X)
{
    adrNode P = AllocateNode(X);
    P->next = G.first;
    G.first = P;
}

adrNode FindNode(Graph G, infoGraph X)
{
    adrNode P = G.first;
    while (P != NULL)
    {
        if (P->info == X)
            return P;
        P = P->next;
    }
    return NULL;
}

void ConnectNode(Graph &G, infoGraph A, infoGraph B)
{
    adrNode N1 = FindNode(G, A);
    adrNode N2 = FindNode(G, B);

    if (N1 == NULL || N2 == NULL)
    {
        cout << "Node tidak ditemukan!\n";
        return;
    }

    // Buat edge dari N1 ke N2
    adrEdge E1 = AllocateEdge(N2);
    E1->next = N1->firstEdge;
    N1->firstEdge = E1;

    // Karena undirected → buat edge balik
    adrEdge E2 = AllocateEdge(N1);
    E2->next = N2->firstEdge;
    N2->firstEdge = E2;
}

void PrintInfoGraph(Graph G)
{
    adrNode P = G.first;
    while (P != NULL)
    {
        cout << P->info << " -> ";
        adrEdge E = P->firstEdge;
        while (E != NULL)
        {
            cout << E->node->info << " ";
            E = E->next;
        }
        cout << endl;
        P = P->next;
    }
}

void ResetVisited(Graph &G)
{
    adrNode P = G.first;
    while (P != NULL)
    {
        P->visited = 0;
        P = P->next;
    }
}

void PrintDFS(Graph &G, adrNode N)
{
    if (N == NULL)
        return;

    N->visited = 1;
    cout << N->info << " ";

    adrEdge E = N->firstEdge;
    while (E != NULL)
    {
        if (E->node->visited == 0)
        {
            PrintDFS(G, E->node);
        }
        E = E->next;
    }
}

void PrintBFS(Graph &G, adrNode N)
{
    if (N == NULL)
        return;

    queue<adrNode> Q;
    Q.push(N);

    while (!Q.empty())
    {
        adrNode curr = Q.front();
        Q.pop();

        if (curr->visited == 0)
        {
            curr->visited = 1;
            cout << curr->info << " ";

            adrEdge E = curr->firstEdge;
            while (E != NULL)
            {
                if (E->node->visited == 0)
                {
                    Q.push(E->node);
                }
                E = E->next;
            }
        }
    }
}

```
#### main.cpp
```c++
#include "graf.h"
#include "graf.cpp"
#include <iostream>
using namespace std;

int main()
{
    Graph G;
    CreateGraph(G);

    // Tambah node
    InsertNode(G, 'A');
    InsertNode(G, 'B');
    InsertNode(G, 'C');
    InsertNode(G, 'D');
    InsertNode(G, 'E');

    // Hubungkan node (graph tidak berarah)
    ConnectNode(G, 'A', 'B');
    ConnectNode(G, 'A', 'C');
    ConnectNode(G, 'B', 'D');
    ConnectNode(G, 'C', 'E');

    cout << "=== Struktur Graph ===\n";
    PrintInfoGraph(G);

    cout << "\n=== DFS dari Node A ===\n";
    ResetVisited(G);
    PrintDFS(G, FindNode(G, 'A'));

    cout << "\n\n=== BFS dari Node A ===\n";
    ResetVisited(G);
    PrintBFS(G, FindNode(G, 'A'));

    cout << endl;
    return 0;
}

```

## UNGUIDED 1,2,3


#### code
#### graph.h
```c++
#ifndef GRAPH_H
#define GRAPH_H

typedef char infoGraph;
typedef struct ElmNode *adrNode;
typedef struct ElmEdge *adrEdge;

struct ElmNode {
    infoGraph info;
    int visited;
    adrEdge firstEdge;
    adrNode Next;
};

struct ElmEdge {
    adrNode Node;
    adrEdge Next;
};

struct Graph {
    adrNode first;
};

adrNode findNode(Graph G, infoGraph X);

void CreateGraph(Graph &G);
adrNode InsertNode(Graph &G, infoGraph X);
void ConnectNode(Graph &G, infoGraph X1, infoGraph X2);
void PrintInfoGraph(Graph G);

void PrintDFS(Graph G, adrNode N);
void PrintBFS(Graph G, adrNode N);

void resetVisited(Graph &G);

#endif
```
#### graph.cpp
```c++
#include <iostream>
#include "graph.h"
using namespace std;

void CreateGraph(Graph &G) {
    G.first = NULL;
}

adrNode findNode(Graph G, infoGraph X) {
    adrNode P = G.first;
    while (P != NULL) {
        if (P->info == X) {
            return P;
        }
        P = P->Next;
    }
    return NULL;
}

adrNode InsertNode(Graph &G, infoGraph X) {
    adrNode newNode = new ElmNode;
    newNode->info = X;
    newNode->visited = 0;
    newNode->firstEdge = NULL;
    newNode->Next = NULL;
    
    if (G.first == NULL) {
        G.first = newNode;
    } else {
        adrNode P = G.first;
        while (P->Next != NULL) {
            P = P->Next;
        }
        P->Next = newNode;
    }
    return newNode;
}

void ConnectNode(Graph &G, infoGraph X1, infoGraph X2) {
    adrNode node1 = findNode(G, X1);
    adrNode node2 = findNode(G, X2);
    
    if (node1 != NULL && node2 != NULL) {
    
        adrEdge edge1 = new ElmEdge;
        edge1->Node = node2;
        edge1->Next = NULL;
        
        if (node1->firstEdge == NULL) {
            node1->firstEdge = edge1;
        } else {
            adrEdge P = node1->firstEdge;
            while (P->Next != NULL) {
                P = P->Next;
            }
            P->Next = edge1;
        }
        
        adrEdge edge2 = new ElmEdge;
        edge2->Node = node1;
        edge2->Next = NULL;
        
        if (node2->firstEdge == NULL) {
            node2->firstEdge = edge2;
        } else {
            adrEdge P = node2->firstEdge;
            while (P->Next != NULL) {
                P = P->Next;
            }
            P->Next = edge2;
        }
    }
}

void PrintInfoGraph(Graph G) {
    adrNode P = G.first;
    
    cout << "Graph Representation:" << endl;
    while (P != NULL) {
        cout << "Node " << P->info << " -> ";
        
        adrEdge E = P->firstEdge;
        while (E != NULL) {
            cout << E->Node->info << " ";
            E = E->Next;
        }
        cout << endl;
        P = P->Next;
    }
    cout << endl;
}

void resetVisited(Graph &G) {
    adrNode P = G.first;
    while (P != NULL) {
        P->visited = 0;
        P = P->Next;
    }
}

void DFS(adrNode N) {
    if (N == NULL || N->visited == 1) {
        return;
    }
    
    cout << N->info << " ";
    N->visited = 1;
    
    adrEdge E = N->firstEdge;
    while (E != NULL) {
        if (E->Node->visited == 0) {
            DFS(E->Node);
        }
        E = E->Next;
    }
}

void PrintDFS(Graph G, adrNode N) {
    cout << "DFS Traversal from node " << N->info << ": ";
    resetVisited(G);
    DFS(N);
    cout << endl;
}

#include <queue>
void PrintBFS(Graph G, adrNode N) {
    cout << "BFS Traversal from node " << N->info << ": ";
    resetVisited(G);
    
    queue<adrNode> q;
    q.push(N);
    N->visited = 1;
    
    while (!q.empty()) {
        adrNode current = q.front();
        q.pop();
        cout << current->info << " ";
        
        adrEdge E = current->firstEdge;
        while (E != NULL) {
            if (E->Node->visited == 0) {
                E->Node->visited = 1;
                q.push(E->Node);
            }
            E = E->Next;
        }
    }
    cout << endl;
}
```
#### main.cpp
```c++
#include <iostream>
#include "graph.h"
using namespace std;

int main() {
    Graph G;
    
    CreateGraph(G);
    
    InsertNode(G, 'A');
    InsertNode(G, 'B');
    InsertNode(G, 'C');
    InsertNode(G, 'D');
    InsertNode(G, 'E');
    InsertNode(G, 'F');
    InsertNode(G, 'G');
    
    ConnectNode(G, 'A', 'B');
    ConnectNode(G, 'A', 'C');
    ConnectNode(G, 'B', 'D');
    ConnectNode(G, 'B', 'E');
    ConnectNode(G, 'C', 'F');
    ConnectNode(G, 'C', 'G');
    ConnectNode(G, 'E', 'F');
    
    PrintInfoGraph(G);
    
    adrNode startNode = findNode(G, 'A');
    
    if (startNode != NULL) {
        PrintDFS(G, startNode);
        
        PrintBFS(G, startNode);

        adrNode nodeD = findNode(G, 'D');
        if (nodeD != NULL) {
            PrintDFS(G, nodeD);
        }
        
        adrNode nodeC = findNode(G, 'C');
        if (nodeC != NULL) {
            PrintBFS(G, nodeC);
        }
    }
    
    return 0;
}
```
> Output soal 1,2,3
> 
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%2014/jawaban%20123.png)

Program di atas merupakan implementasi ADT (Abstract Data Type) Graph tidak berarah menggunakan bahasa C++ yang terdiri dari tiga file utama: `graph.h` untuk deklarasi struktur data dan prototipe fungsi, `graph.cpp` untuk implementasi algoritma, dan `main.cpp` untuk pengujian. Struktur data graph direpresentasikan dengan adjacency list yang terdiri dari node (ElmNode) yang menyimpan informasi karakter dan daftar edge (ElmEdge) yang menghubungkannya dengan node lain, dengan setiap node memiliki flag `visited` untuk penelusuran. Program menyediakan operasi dasar seperti `CreateGraph`, `InsertNode`, `ConnectNode`, dan `PrintInfoGraph`, serta implementasi dua algoritma penelusuran graph: **DFS (Depth-First Search)** yang menggunakan pendekatan rekursif untuk menelusuri graph secara mendalam hingga ke leaf node sebelum backtrack, dan **BFS (Breadth-First Search)** yang menggunakan queue untuk menelusuri graph secara melebar per level. Pada fungsi `main`, graph diinisialisasi dengan 7 node (A-G) dan dihubungkan sesuai ilustrasi Gambar 14-14, kemudian dilakukan penelusuran dari berbagai node awal untuk menunjukkan perbedaan output antara DFS dan BFS.

## Referensi
1.GeeksforGeeks: Graph and its representations https://www.geeksforgeeks.org/graph-and-its-representations/

2.GeeksforGeeks: Depth First Search or DFS for a Graph https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/

3.GeeksforGeeks: Breadth First Search or BFS for a Graph https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/

4.Programiz: Graph Data Structure https://www.programiz.com/dsa/graph
