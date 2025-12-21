# <h1 align="center">Laporan Praktikum Modul 10 <br> Tree </h1>
<p align="center">Nashir Khoirul Huda - 103112400168</p>

## Dasar Teori

Rekursif adalah teknik pemrograman di mana suatu fungsi memanggil dirinya sendiri untuk menyelesaikan masalah yang dapat dipecah menjadi bagian-bagian yang lebih kecil dan memiliki pola penyelesaian serupa. Setiap fungsi rekursif harus memiliki *base case* sebagai kondisi berhenti dan *recursive case* sebagai proses pemanggilan ulang fungsi. Meskipun rekursif dapat membuat algoritma lebih ringkas dan mudah dipahami, teknik ini kurang efisien dibanding iteratif karena membutuhkan memori tambahan untuk menyimpan *activation record* pada setiap pemanggilan fungsi. Konsep rekursif banyak digunakan pada berbagai struktur data, termasuk tree, yang merupakan struktur data non-linear berbentuk hirarki dengan simpul akar, simpul anak, dan simpul daun. Pada tree, rekursif mempermudah implementasi berbagai operasi seperti traversal, pencarian, penyisipan, dan penghapusan node.



## Guide

```go
#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node *kiri, *kanan;
};

Node *buatNode(int nilai)
{
    Node *baru = new Node();
    baru->data = nilai;
    baru->kiri = baru->kanan = NULL;
    return baru;
}

Node *insert(Node *root, int nilai)
{
    if (root == NULL)
        return buatNode(nilai);
    
    if (nilai < root->data)
        root->kiri = insert(root->kiri, nilai);
    else if (nilai > root->data)
        root->kanan = insert(root->kanan, nilai);

    return root;
}

Node *search(Node *root, int nilai)
{
    if (root == NULL || root->data == nilai)
        return root;

    if (nilai < root->data)
        return search(root->kiri, nilai);

    return search(root->kanan, nilai);
}

Node *nilaiTerkecil(Node *node)
{
    Node *current = node;
    while (current && current->kiri != NULL)
        current = current->kiri;

        return current;
}

Node *hapus(Node *root, int nilai)
{
    if (root == NULL)
        return root;

    if (nilai < root->data)
        root->kiri = hapus(root->kiri, nilai);
    else if (nilai > root->data)
        root->kanan = hapus(root->kanan, nilai);
    else
    {
        if (root->kiri == NULL)
        {
            Node *temp = root->kanan;
            delete root;
            return temp;
        }
        else if (root->kanan == NULL){
            Node *temp = root->kiri;
            delete root;
            return temp;
        }
        Node *temp = nilaiTerkecil(root->kanan);
        root->data = temp->data;
        root->kanan = hapus(root->kanan, temp->data);
    }
    return root;
}

Node *update(Node *root, int Lama, int baru)
{
    if (search(root, Lama) != NULL)
    {
        root = hapus(root, Lama);
        root = insert(root, baru);
        cout << "Data " << Lama << " diupdate menjadi " << baru << endl;
    }
    else
    {
        cout << "Data " << Lama << " tidak ditemukan!" << endl;
    }
    return root;
}

void preOrder(Node *root)
{
    if (root != NULL)
    {
        cout << root->data << " ";
        preOrder(root->kiri);
        preOrder(root->kanan);
    }
}

void inOrder(Node *root)
{
    if (root != NULL)
    {
        inOrder(root->kiri);
        cout << root->data << " ";
        inOrder(root->kanan);
    }
}

void postOrder(Node *root)
{
    if (root != NULL)
    {
        postOrder(root->kiri);
        postOrder(root->kanan);
        cout << root->data << " ";
    }
}

int main()
{
    Node *root = NULL;

    cout << "=== 1. INSERT DATA ===" << endl;
    root = insert(root, 10);
    insert(root, 5);
    insert(root, 20);
    insert(root, 3);
    insert(root, 7);
    insert(root, 15);
    insert(root, 25);
    cout << "Data berhasil dimasukan.\n" << endl;

    cout << "=== 2. TAMPILKAN TREE (TRAVELSAL) ===" << endl;
    cout << "PreOrder : ";
    preOrder(root);
    cout << endl;
    cout << "InOrder : ";
    inOrder(root);
    cout << endl;
    cout << "PostOrder : ";
    postOrder(root);
    cout << "\n" << endl;

    cout << "=== 3. TEST SEARCH ===" << endl;
    int cari1 = 7, cari2 = 99;
    cout << "Cari " << cari1 << ": " << (search(root,cari1) ? "Ketemu" : "Tidak Aada") << endl;
    cout << "Cari " << cari2 << ": " << (search(root,cari2) ? "Ketemu" : "Tidak Aada") << endl;
    cout << endl;

    cout << "=== 4. TEST UPDATE ===" << endl;
    root = update(root, 5, 8);
    cout << "Hasil Order setelah update: ";
    cout << endl;
    cout << endl;

    cout << "PreOrder : ";
    preOrder(root);
    cout << endl;
    cout << "InOrder : ";
    inOrder(root);
    cout << endl;
    cout << "PostOrder : ";
    postOrder(root);
    cout << "\n" << endl;

    cout << "== 5. TEST DELETE ===" << endl;
    cout << "Menghapus angka 20..." << endl;
    root = hapus(root, 20);

    cout << "PreOrder : ";
    preOrder(root);
    cout << endl;
    cout << "InOrder : ";
    inOrder(root);
    cout << endl;
    cout << "PostOrder : ";
    postOrder(root);
    cout << "\n" << endl;

    return 0;
}
```


## Unguide

### Soal 1
> ![Soal]()

## bstree.h
```go

```

## bstreee.cpp

```go

```

## main.cpp

```go

```

> Output
> ![Screenshot bagian x]( )

Program di atas 


### Soal 2
Buatlah fungsi untuk menghitung jumlah node dengan fungsi berikut.

➢ fungsi hitungJumlahNode( root:address ) : integer

/* fungsi mengembalikan integer banyak node yang ada di dalam BST*/

➢ fungsi hitungTotalInfo( root:address, start:integer ) : integer

/* fungsi mengembalikan jumlah (total) info dari node-node yang ada di dalam BST*/

➢ fungsi hitungKedalaman( root:address, start:integer ) : integer

/* fungsi rekursif mengembalikan integer kedalaman maksimal dari binary tree */
```
int main() {
cout << "Hello World" << endl;
address root = Nil;
insertNode(root,1);
insertNode(root,2);
insertNode(root,6);
insertNode(root,4);
insertNode(root,5);
insertNode(root,3);
insertNode(root,6);
insertNode(root,7);
InOrder(root);
cout<<"\n";
cout<<"kedalaman : "<<hitungKedalaman(root,0)<<endl;
cout<<"jumlah Node : "<<hitungNode(root)<<endl;
cout<<"total : "<<hitungTotal(root)<<endl;
return 0;
}
```

## bstree.h
```go

```

### bstree.cpp
```

```

### main.cpp
```

```
> Output
> ![Screenshot bagian x]( )

Program di atas

### Soal 3
> ![Soal]( )

## no3.cpp
```go

```

> Output
> ![Screenshot bagian x]( )

Program di atas



## Referensi
1. https://www.w3schools.com/dsa/dsa_theory_trees.php
2. https://www.w3schools.com/dsa/dsa_data_binarytrees.php
3. https://www.w3schools.com/dsa/dsa_data_binarysearchtrees.php
4. https://www.w3schools.com/dsa/dsa_algo_binarytrees_preorder.php
5. https://www.w3schools.com/dsa/dsa_algo_binarytrees_inorder.php
6. https://www.w3schools.com/dsa/dsa_data_avltrees.php




