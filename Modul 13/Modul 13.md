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

## multilist.h

```go
#ifndef MULTILIST_H
#define MULTILIST_H

#include <iostream>
using namespace std;

struct infotype_child {
    string nama;
    int umur;
};

typedef struct elmlist_child *address_child;

struct elmlist_child {
    infotype_child info;
    address_child next;
    address_child prev;
};

struct infotype_parent {
    string nama_keluarga;
    address_child first_child;
};

typedef struct elmlist_parent *address_parent;

struct elmlist_parent {
    infotype_parent info;
    address_parent next;
};

struct List_parent {
    address_parent first;
};

void createListChild(address_child &L);
address_child createElmChild(infotype_child data);
void insertFirstChild(address_child &L, address_child P);
void insertLastChild(address_child &L, address_child P);
void insertAfterChild(address_child Prec, address_child P);
void deleteFirstChild(address_child &L, address_child &P);
void deleteLastChild(address_child &L, address_child &P);
void deleteAfterChild(address_child Prec, address_child &P);
void printListChild(address_child L);
address_child searchChild(address_child L, string nama);

void createListParent(List_parent &L);
address_parent createElmParent(infotype_parent data);
void insertFirstParent(List_parent &L, address_parent P);
void insertLastParent(List_parent &L, address_parent P);
void insertAfterParent(address_parent Prec, address_parent P);
void deleteFirstParent(List_parent &L, address_parent &P);
void deleteLastParent(List_parent &L, address_parent &P);
void deleteAfterParent(address_parent Prec, address_parent &P);
void printListParent(List_parent L);
address_parent searchParent(List_parent L, string nama_keluarga);

void addChildToParent(List_parent &L, string nama_keluarga, infotype_child data_child);
void printAllData(List_parent L);
void deleteChildFromParent(List_parent &L, string nama_keluarga, string nama_child);

#endif

```

## multilist.cpp

```go
#include "multilist.h"

void createListChild(address_child &L) {
    L = NULL;
}

address_child createElmChild(infotype_child data) {
    address_child P = new elmlist_child;
    P->info = data;
    P->next = NULL;
    P->prev = NULL;
    return P;
}

void insertFirstChild(address_child &L, address_child P) {
    if (L == NULL) {
        L = P;
    } else {
        P->next = L;
        L->prev = P;
        L = P;
    }
}

void insertLastChild(address_child &L, address_child P) {
    if (L == NULL) {
        L = P;
    } else {
        address_child Q = L;
        while (Q->next != NULL) {
            Q = Q->next;
        }
        Q->next = P;
        P->prev = Q;
    }
}

void insertAfterChild(address_child Prec, address_child P) {
    if (Prec != NULL) {
        P->next = Prec->next;
        P->prev = Prec;
        if (Prec->next != NULL) {
            Prec->next->prev = P;
        }
        Prec->next = P;
    }
}

void deleteFirstChild(address_child &L, address_child &P) {
    if (L != NULL) {
        P = L;
        if (L->next == NULL) {
            L = NULL;
        } else {
            L = L->next;
            L->prev = NULL;
            P->next = NULL;
        }
    }
}

void deleteLastChild(address_child &L, address_child &P) {
    if (L != NULL) {
        if (L->next == NULL) {
            P = L;
            L = NULL;
        } else {
            address_child Q = L;
            while (Q->next->next != NULL) {
                Q = Q->next;
            }
            P = Q->next;
            Q->next = NULL;
            P->prev = NULL;
        }
    }
}

void deleteAfterChild(address_child Prec, address_child &P) {
    if (Prec != NULL && Prec->next != NULL) {
        P = Prec->next;
        Prec->next = P->next;
        if (P->next != NULL) {
            P->next->prev = Prec;
        }
        P->next = NULL;
        P->prev = NULL;
    }
}

void printListChild(address_child L) {
    address_child P = L;
    int i = 1;
    while (P != NULL) {
        cout << i << ". Nama: " << P->info.nama << ", Umur: " << P->info.umur << endl;
        P = P->next;
        i++;
    }
    if (L == NULL) {
        cout << "  (Tidak ada data)" << endl;
    }
}

address_child searchChild(address_child L, string nama) {
    address_child P = L;
    while (P != NULL) {
        if (P->info.nama == nama) {
            return P;
        }
        P = P->next;
    }
    return NULL;
}
void createListParent(List_parent &L) {
    L.first = NULL;
}

address_parent createElmParent(infotype_parent data) {
    address_parent P = new elmlist_parent;
    P->info = data;
    P->info.first_child = NULL;
    P->next = NULL;
    return P;
}

void insertFirstParent(List_parent &L, address_parent P) {
    if (L.first == NULL) {
        L.first = P;
    } else {
        P->next = L.first;
        L.first = P;
    }
}

void insertLastParent(List_parent &L, address_parent P) {
    if (L.first == NULL) {
        L.first = P;
    } else {
        address_parent Q = L.first;
        while (Q->next != NULL) {
            Q = Q->next;
        }
        Q->next = P;
    }
}

void insertAfterParent(address_parent Prec, address_parent P) {
    if (Prec != NULL) {
        P->next = Prec->next;
        Prec->next = P;
    }
}

void deleteFirstParent(List_parent &L, address_parent &P) {
    if (L.first != NULL) {
        P = L.first;
        if (L.first->next == NULL) {
            L.first = NULL;
        } else {
            L.first = L.first->next;
            P->next = NULL;
        }
    }
}

void deleteLastParent(List_parent &L, address_parent &P) {
    if (L.first != NULL) {
        if (L.first->next == NULL) {
            P = L.first;
            L.first = NULL;
        } else {
            address_parent Q = L.first;
            while (Q->next->next != NULL) {
                Q = Q->next;
            }
            P = Q->next;
            Q->next = NULL;
        }
    }
}

void deleteAfterParent(address_parent Prec, address_parent &P) {
    if (Prec != NULL && Prec->next != NULL) {
        P = Prec->next;
        Prec->next = P->next;
        P->next = NULL;
    }
}

void printListParent(List_parent L) {
    address_parent P = L.first;
    int i = 1;
    while (P != NULL) {
        cout << i << ". Keluarga: " << P->info.nama_keluarga << endl;
        P = P->next;
        i++;
    }
    if (L.first == NULL) {
        cout << "  (Tidak ada data keluarga)" << endl;
    }
}

address_parent searchParent(List_parent L, string nama_keluarga) {
    address_parent P = L.first;
    while (P != NULL) {
        if (P->info.nama_keluarga == nama_keluarga) {
            return P;
        }
        P = P->next;
    }
    return NULL;
}

void addChildToParent(List_parent &L, string nama_keluarga, infotype_child data_child) {
    address_parent parent = searchParent(L, nama_keluarga);
    if (parent != NULL) {
        address_child new_child = createElmChild(data_child);
        insertLastChild(parent->info.first_child, new_child);
        cout << "Anak " << data_child.nama << " berhasil ditambahkan ke keluarga " << nama_keluarga << endl;
    } else {
        cout << "Keluarga " << nama_keluarga << " tidak ditemukan!" << endl;
    }
}

void printAllData(List_parent L) {
    address_parent P = L.first;
    if (P == NULL) {
        cout << "Tidak ada data keluarga." << endl;
        return;
    }
    
    cout << "===== DATA SELURUH KELUARGA =====\n";
    while (P != NULL) {
        cout << "\nKeluarga: " << P->info.nama_keluarga << endl;
        cout << "Anggota keluarga:" << endl;
        printListChild(P->info.first_child);
        P = P->next;
    }
}

void deleteChildFromParent(List_parent &L, string nama_keluarga, string nama_child) {
    address_parent parent = searchParent(L, nama_keluarga);
    if (parent != NULL) {
        address_child child = searchChild(parent->info.first_child, nama_child);
        if (child != NULL) {
        
            if (child == parent->info.first_child) {
                address_child deleted;
                deleteFirstChild(parent->info.first_child, deleted);
                delete deleted;
            } 
            else {
                address_child prec = parent->info.first_child;
                while (prec->next != child) {
                    prec = prec->next;
                }
                address_child deleted;
                deleteAfterChild(prec, deleted);
                delete deleted;
            }
            cout << "Anak " << nama_child << " berhasil dihapus dari keluarga " << nama_keluarga << endl;
        } else {
            cout << "Anak " << nama_child << " tidak ditemukan dalam keluarga " << nama_keluarga << endl;
        }
    } else {
        cout << "Keluarga " << nama_keluarga << " tidak ditemukan!" << endl;
    }
}

```

## main.cpp

```go
#include "multilist.h"
#include <cstdlib>

void showMenu() {
    cout << "\n===== SISTEM DATA KELUARGA =====\n";
    cout << "1. Tambah Keluarga Baru\n";
    cout << "2. Tambah Anggota Keluarga\n";
    cout << "3. Tampilkan Semua Keluarga\n";
    cout << "4. Tampilkan Semua Data\n";
    cout << "5. Cari Keluarga\n";
    cout << "6. Hapus Anggota Keluarga\n";
    cout << "7. Hapus Keluarga\n";
    cout << "8. Keluar\n";
    cout << "Pilih menu: ";
}

int main() {
    List_parent data_keluarga;
    createListParent(data_keluarga);
    
    int choice;
    string nama_keluarga, nama_anak;
    int umur;

    cout << "Membuat data contoh..." << endl;

    infotype_parent keluarga1 = {"Wijaya", NULL};
    infotype_parent keluarga2 = {"Sari", NULL};
    infotype_parent keluarga3 = {"Santoso", NULL};
    
    address_parent p1 = createElmParent(keluarga1);
    address_parent p2 = createElmParent(keluarga2);
    address_parent p3 = createElmParent(keluarga3);
    
    insertLastParent(data_keluarga, p1);
    insertLastParent(data_keluarga, p2);
    insertLastParent(data_keluarga, p3);
    
    infotype_child anak1 = {"Budi", 25};
    infotype_child anak2 = {"Siti", 23};
    infotype_child anak3 = {"Andi", 30};
    infotype_child anak4 = {"Rina", 28};
    infotype_child anak5 = {"Dewi", 22};
    
    addChildToParent(data_keluarga, "Wijaya", anak1);
    addChildToParent(data_keluarga, "Wijaya", anak2);
    addChildToParent(data_keluarga, "Sari", anak3);
    addChildToParent(data_keluarga, "Santoso", anak4);
    addChildToParent(data_keluarga, "Santoso", anak5);
    
    do {
        showMenu();
        cin >> choice;
        cin.ignore(); 
        
        switch(choice) {
            case 1: {
                cout << "\nMasukkan nama keluarga: ";
                getline(cin, nama_keluarga);
                
                infotype_parent keluarga_baru = {nama_keluarga, NULL};
                address_parent new_parent = createElmParent(keluarga_baru);
                insertLastParent(data_keluarga, new_parent);
                cout << "Keluarga " << nama_keluarga << " berhasil ditambahkan.\n";
                break;
            }
            
            case 2: {
                cout << "\nMasukkan nama keluarga: ";
                getline(cin, nama_keluarga);
                cout << "Masukkan nama anggota: ";
                getline(cin, nama_anak);
                cout << "Masukkan umur: ";
                cin >> umur;
                cin.ignore();
                
                infotype_child anak_baru = {nama_anak, umur};
                addChildToParent(data_keluarga, nama_keluarga, anak_baru);
                break;
            }
            
            case 3: {
                cout << "\n===== DAFTAR KELUARGA =====\n";
                printListParent(data_keluarga);
                break;
            }
            
            case 4: {
                printAllData(data_keluarga);
                break;
            }
            
            case 5: {
                cout << "\nMasukkan nama keluarga yang dicari: ";
                getline(cin, nama_keluarga);
                
                address_parent result = searchParent(data_keluarga, nama_keluarga);
                if (result != NULL) {
                    cout << "Keluarga ditemukan: " << result->info.nama_keluarga << endl;
                    cout << "Anggota keluarga:\n";
                    printListChild(result->info.first_child);
                } else {
                    cout << "Keluarga " << nama_keluarga << " tidak ditemukan.\n";
                }
                break;
            }
            
            case 6: {
                cout << "\nMasukkan nama keluarga: ";
                getline(cin, nama_keluarga);
                cout << "Masukkan nama anggota yang akan dihapus: ";
                getline(cin, nama_anak);
                
                deleteChildFromParent(data_keluarga, nama_keluarga, nama_anak);
                break;
            }
            
            case 7: {
                cout << "\nMasukkan nama keluarga yang akan dihapus: ";
                getline(cin, nama_keluarga);
                
                address_parent parent = searchParent(data_keluarga, nama_keluarga);
                if (parent != NULL) {
                    
                    address_child child;
                    while (parent->info.first_child != NULL) {
                        deleteFirstChild(parent->info.first_child, child);
                        delete child;
                    }

                    if (parent == data_keluarga.first) {
                        deleteFirstParent(data_keluarga, parent);
                    } else {
                        address_parent prec = data_keluarga.first;
                        while (prec->next != parent) {
                            prec = prec->next;
                        }
                        deleteAfterParent(prec, parent);
                    }
                    delete parent;
                    cout << "Keluarga " << nama_keluarga << " berhasil dihapus.\n";
                } else {
                    cout << "Keluarga " << nama_keluarga << " tidak ditemukan.\n";
                }
                break;
            }
            
            case 8: {
                cout << "\nTerima kasih telah menggunakan program.\n";
                break;
            }
            
            default: {
                cout << "\nPilihan tidak valid. Silakan coba lagi.\n";
                break;
            }
        }
        
    } while (choice != 8);
    
    return 0;
}

```

> Output
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%2013/jawaban%202.png)

Program multilist ini mengimplementasikan struktur data senarai ganda yang terdiri dari list induk (parent) yang merepresentasikan keluarga dan list anak (child) yang berisi anggota keluarga, di mana setiap simpul induk terhubung ke list simpul anaknya, dengan fungsi-fungsi lengkap untuk menambah, menghapus, mencari, dan menampilkan data baik untuk induk maupun anak, serta dilengkapi dengan menu interaktif yang memungkinkan pengelolaan data keluarga secara dinamis melalui program utama.



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
#ifndef CIRCULARLIST_H
#define CIRCULARLIST_H

#include <iostream>
#include <string>
using namespace std;

struct infotype {
    string nama;
    string nim;
    char jenis_kelamin;
    float ipk;
};

typedef struct elmlist* address;

struct elmlist {
    infotype info;
    address next;
};

struct List {
    address first;
};


void createList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void insertFirst(List &L, address P);
void insertAfter(List &L, address Prec, address P);
void insertLast(List &L, address P);
void deleteFirst(List &L, address &P);
void deleteAfter(List &L, address Prec, address &P);
void deleteLast(List &L, address &P);
address findElm(List L, infotype x);
void printInfo(List L);

address createData(string nama, string nim, char jenis_kelamin, float ipk);

#endif
```

## circular.cpp
```go
#include "circularlist.h"

void createList(List &L) {
    L.first = NULL;
}

address alokasi(infotype x) {
    address P = new elmlist;
    P->info = x;
    P->next = NULL;
    return P;
}


void dealokasi(address &P) {
    delete P;
    P = NULL;
}

void insertFirst(List &L, address P) {
    if (L.first == NULL) {
        L.first = P;
        P->next = P;  
    } else {
        address last = L.first;
        
        while (last->next != L.first) {
            last = last->next;
        }
        P->next = L.first;
        L.first = P;
        last->next = P;  
    }
}


void insertAfter(List &L, address Prec, address P) {
    if (Prec != NULL) {
        P->next = Prec->next;
        Prec->next = P;
    }
}

void insertLast(List &L, address P) {
    if (L.first == NULL) {
        L.first = P;
        P->next = P;
    } else {
        address last = L.first;
        
        while (last->next != L.first) {
            last = last->next;
        }
        last->next = P;
        P->next = L.first;
    }
}

void deleteFirst(List &L, address &P) {
    if (L.first != NULL) {
        P = L.first;
        if (L.first->next == L.first) {  
            L.first = NULL;
        } else {
            address last = L.first;
            
            while (last->next != L.first) {
                last = last->next;
            }
            L.first = L.first->next;
            last->next = L.first;
            P->next = NULL;
        }
    }
}

void deleteAfter(List &L, address Prec, address &P) {
    if (Prec != NULL && Prec->next != NULL) {
        P = Prec->next;
        if (P->next == P) {  
            Prec->next = Prec;
        } else {
            Prec->next = P->next;
            P->next = NULL;
        }
    }
}

void deleteLast(List &L, address &P) {
    if (L.first != NULL) {
        if (L.first->next == L.first) {  
            P = L.first;
            L.first = NULL;
        } else {
            address last = L.first;
            address prev = NULL;
        
            while (last->next != L.first) {
                prev = last;
                last = last->next;
            }
            P = last;
            prev->next = L.first;
            P->next = NULL;
        }
    }
}

address findElm(List L, infotype x) {
    if (L.first == NULL) {
        return NULL;
    }
    
    address P = L.first;
    do {
        if (P->info.nim == x.nim) {
            return P;
        }
        P = P->next;
    } while (P != L.first);
    
    return NULL;
}

void printInfo(List L) {
    if (L.first == NULL) {
        cout << "List kosong" << endl;
        return;
    }
    
    cout << "Data Mahasiswa (Circular Linked List):" << endl;
    cout << "========================================" << endl;
    
    address P = L.first;
    int i = 1;
    do {
        cout << i << ". Nama: " << P->info.nama << endl;
        cout << "   NIM: " << P->info.nim << endl;
        cout << "   Jenis Kelamin: " << P->info.jenis_kelamin << endl;
        cout << "   IPK: " << P->info.ipk << endl;
        cout << "----------------------------------------" << endl;
        P = P->next;
        i++;
    } while (P != L.first);
    
    cout << "Total data: " << i-1 << endl;
}

address createData(string nama, string nim, char jenis_kelamin, float ipk) {
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

## main.cpp
```go
#include "circularlist.h"
#include <iostream>
using namespace std;

int main() {
    List L;
    address P1, P2, P3;
    
    createList(L);
    cout << "1. List berhasil dibuat (kosong)" << endl;
    
    cout << "\n2. Membuat data mahasiswa..." << endl;
    
    P1 = createData("Nanda B. P.", "1103134395", 'L', 3.3);
    cout << "   Data 1: " << P1->info.nama << " - " << P1->info.nim << " dibuat" << endl;
    
    P2 = createData("Dawki H. M.", "1103120134", 'L', 3.71);
    cout << "   Data 2: " << P2->info.nama << " - " << P2->info.nim << " dibuat" << endl;
    
    P3 = createData("Yosi Ineba", "1103130120", 'P', 3.5);
    cout << "   Data 3: " << P3->info.nama << " - " << P3->info.nim << " dibuat" << endl;

    cout << "\n3. Menyisipkan data ke dalam list..." << endl;
    
    insertFirst(L, P1);
    cout << "   " << P1->info.nama << " dimasukkan di awal" << endl;
    
    insertLast(L, P2);
    cout << "   " << P2->info.nama << " dimasukkan di akhir" << endl;
    
    infotype searchKey;
    searchKey.nim = "1103134395";
    address Prec = findElm(L, searchKey);
    if (Prec != NULL) {
        insertAfter(L, Prec, P3);
        cout << "   " << P3->info.nama << " dimasukkan setelah " << Prec->info.nama << endl;
    }
    
    cout << "\n4. Menambahkan data tambahan..." << endl;
    
    address P4 = createData("Masayibah Nur Aula", "1103130120", 'P', 4.0);
    insertLast(L, P4);
    cout << "   " << P4->info.nama << " dimasukkan di akhir" << endl;
    
    address P5 = createData("Puad A.S.", "1103130118", 'L', 1.34);
    insertLast(L, P5);
    cout << "   " << P5->info.nama << " dimasukkan di akhir" << endl;
    
    address P6 = createData("Syair A.L.S", "1103134400", 'L', 3.45);
    insertLast(L, P6);
    cout << "   " << P6->info.nama << " dimasukkan di akhir" << endl;
    
    address P7 = createData("Lugman B.R", "11031344472", 'L', 3.76);
    insertLast(L, P7);
    cout << "   " << P7->info.nama << " dimasukkan di akhir" << endl;
    
    address P8 = createData("Fahmi A.", "11031344392", 'L', 3.3);
    insertLast(L, P8);
    cout << "   " << P8->info.nama << " dimasukkan di akhir" << endl;
    
    cout << "\n5. Menampilkan semua data dalam list:" << endl;
    cout << "========================================" << endl;
    printInfo(L);

    cout << "\n6. Mencari data berdasarkan NIM..." << endl;
    infotype searchData;
    
    searchData.nim = "1103134395";
    address found = findElm(L, searchData);
    if (found != NULL) {
        cout << "   Data ditemukan: " << found->info.nama << " (NIM: " << found->info.nim << ")" << endl;
    } else {
        cout << "   Data dengan NIM " << searchData.nim << " tidak ditemukan" << endl;
    }
    
    searchData.nim = "9999999999";
    found = findElm(L, searchData);
    if (found == NULL) {
        cout << "   Data dengan NIM " << searchData.nim << " tidak ditemukan (seharusnya)" << endl;
    }
    
    cout << "\n7. Menghapus data..." << endl;

    address deleted;
    deleteFirst(L, deleted);
    if (deleted != NULL) {
        cout << "   Data pertama (" << deleted->info.nama << ") berhasil dihapus" << endl;
        dealokasi(deleted);
    }
    
    deleteLast(L, deleted);
    if (deleted != NULL) {
        cout << "   Data terakhir (" << deleted->info.nama << ") berhasil dihapus" << endl;
        dealokasi(deleted);
    }
    
  
    cout << "\n8. Data setelah penghapusan:" << endl;
    cout << "========================================" << endl;
    printInfo(L);
    
    cout << "\nProgram selesai!" << endl;
    
    return 0;
}
```

> Output
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%2013/jawaban%203.png)

Program diatas  mengimplementasikan struktur data circular linked list untuk menyimpan data mahasiswa yang terdiri dari nama, NIM, jenis kelamin, dan IPK, dengan sistem sirkular di mana elemen terakhir terhubung kembali ke elemen pertama membentuk lingkaran, serta menyediakan fungsi-fungsi dasar seperti pembuatan list, penyisipan di awal/tengah/akhir, penghapusan elemen, pencarian berdasarkan NIM, dan penampilan seluruh data yang diuji secara lengkap melalui program utama dengan data contoh.


## Referensi
1. https://www.w3schools.com/dsa/dsa_data_linkedlists_types.php
2. https://www.w3schools.com/dsa/trydsa.php?filename=demo_linkedlists_circsingly
3. https://www.w3schools.com/dsa/dsa_theory_linkedlists.php
4. https://www.w3schools.com/dsa/dsa_algo_linkedlists_operations.php]
5. https://www.w3schools.com/dsa/
