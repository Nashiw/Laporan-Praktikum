# <h1 align="center">Laporan Praktikum Modul 13 <br> Multi Linked List </h1>
<p align="center">Nashir Khoirul Huda - 103112400168</p>

## Dasar Teori

Dasar teori dari modul **Multi Linked List** adalah bahwa struktur data ini merupakan perluasan dari konsep linked list tunggal maupun ganda, di mana setiap elemen pada list induk dapat memiliki list lain yang terhubung sebagai list anak. Multi Linked List memungkinkan representasi hubungan **hierarkis** antara data, misalnya hubungan *pegawai–anak* sebagaimana ditampilkan pada modul, sehingga setiap node induk tidak hanya menyimpan informasi dan pointer ke node berikutnya, tetapi juga memiliki pointer menuju sebuah list anak yang berisi elemen-elemen terkait. Dengan struktur seperti ini, Multi Linked List menjadi sangat fleksibel untuk mengelola data yang memiliki relasi satu‐ke‐banyak, karena operasi dasar seperti **insert**, **delete**, dan **pencarian** dapat dilakukan baik pada level induk maupun level anak secara terpisah namun tetap terhubung, sehingga struktur ini efisien dalam mengorganisasi data kompleks yang membutuhkan keterkaitan antar elemen.

## Guide

```go
#include <iostream>
#include <string>
using namespace std;

struct ChildNode
{
    string info;
    ChildNode *next;
};

struct ParentNode
{
    string info;
    ChildNode *childHead;
    ParentNode *next;
};

ParentNode *createParent(string info)
{
    ParentNode *newNode = new ParentNode;
    newNode->info = info;
    newNode->childHead = NULL;
    newNode->next = NULL;
    return newNode;
}

ChildNode *createChild(string info)
{
    ChildNode *newNode = new ChildNode;
    newNode->info = info;
    newNode->next = NULL;
    return newNode;
}

void insertParent(ParentNode *&head, string info)
{
    ParentNode *newNode = createParent(info);
    if (head == NULL)
    {
        head = newNode;
    }
    else
    {
        ParentNode *temp = head;
        while (temp->next != NULL)
        {
            temp = temp->next;
        }
        temp->next = newNode;
    }
}

void insertChild(ParentNode *head, string parentInfo, string childInfo)
{
    ParentNode *p = head;
    while (p != NULL && p->info != parentInfo)
    {
        p = p->next;
    }
    
    if (p != NULL)
    {
        ChildNode *newChild = createChild(childInfo);
        
        if (p->childHead == NULL)
        {
            p->childHead = newChild;
        }
        else
        {
            ChildNode *c = p->childHead;
            while (c->next != NULL)
            {
                c = c->next;
            }
            c->next = newChild;
        }
    }
}

void printAll(ParentNode *head)
{
    ParentNode *p = head;
    while (p != NULL)
    {
        cout << p->info;
        ChildNode *c = p->childHead;
        if (c != NULL)
        {
            while (c != NULL)
            {
                cout << " -> " << c->info;
                c = c->next;
            }
        }
     cout << endl;
        p = p->next;
    }
}

int main()
{
    ParentNode *list = NULL;
    
    insertParent(list, "Parent Node 1");
    insertParent(list, "Parent Node 2");
    
    printAll(list);
    cout << "\n";
    
    insertChild(list, "Parent Node 1", "Child Node A");
    insertChild(list, "Parent Node 1", "Child Node B");
    insertChild(list, "Parent Node 2", "Child Node C");
    
    printAll(list);
    
    return 0;
}
```


## Unguide

### Soal 2
Perhatikan program 46 multilist.h, buat multilist.cpp untuk implementasi semua fungsi pada
multilist.h. Buat main.cpp untuk pemanggilan fungsi-fungsi tersebut.

## multilist.cpp

```go


```

## main.cpp

```go


```

> Output
> ![Screenshot bagian x]( )

Program 

### Soal 3
Buatlah implementasi ADT Doubly Linked list pada file “circularlist.cpp”. Tambahkan fungsi/prosedur berikut pada file “main.cpp”.

• fungsi create ( in nama, nim : string, jenis_kelamin : char, ipk : float)
• fungsi disediakan, ketik ulang code yang diberikan
• fungsi mengalokasikan sebuah elemen list dengan info sesuai input
```
address createData(string nama, string nim, char jenis_kelamin, float ipk)
{
    /**
     * PR : mengalokasikan sebuah elemen list dengan info dengan info sesuai input
     * FS : address P menunjuk elemen dengan info sesuai input
     */
    infotype x;
    address P;
    x.nama = nama;
    x.nim = nim;
    x.jenis_kelamin = jenis_kelamin;
    x.ipk = ipk;
    P = alokasi(x);
    return P;
}
```

Cobalah hasil implementasi ADT pada file “main.cpp”

```
int main()
{
    List L, A, B, L2;
    address P1 = Nil;
    address P2 = Nil;
    infotype x;
    createList(L);

    cout<<"coba insert first, last, dan after"<<endl;

    P1 = createData("Danu", "04", 'l', 4.0);
    insertFirst(L,P1);

    P1 = createData("Fahmi", "06", 'l',3.45);
    insertLast(L,P1);

    P1 = createData("Bobi", "02", 'l',3.71);
    insertFirst(L,P1);

    P1 = createData("Ali", "01", 'l', 3.3);
    insertFirst(L,P1);

    P1 = createData("Gita", "07", 'p', 3.75);
    insertLast(L,P1);

    x.nim = "07";
    P1 = findElm(L,x);
    P2 = createData("Cindi", "03", 'p', 3.5);
    insertAfter(L, P1, P2);

    x.nim = "02";
    P1 = findElm(L,x);
    P2 = createData("Hilmi", "08", 'p', 3.3);
    insertAfter(L, P1, P2);

    x.nim = "04";
    P1 = findElm(L,x);
    P2 = createData("Eli", "05", 'p', 3.4);
    insertAfter(L, P1, P2);

    printInfo(L);
    return 0;
}
```

## circular.h
```go

```

## circular.cpp
```go

```

## main.cpp
```go

```

> Output
> ![Screenshot bagian x]( )

Program .


## Referensi
1. https://www.w3schools.com/dsa/dsa_data_linkedlists_types.php
2. https://www.w3schools.com/dsa/trydsa.php?filename=demo_linkedlists_circsingly
3. https://www.w3schools.com/dsa/dsa_theory_linkedlists.php
4. https://www.w3schools.com/dsa/dsa_algo_linkedlists_operations.php]
5. https://www.w3schools.com/dsa/
