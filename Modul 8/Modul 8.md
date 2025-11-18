# <h1 align="center">Laporan Praktikum Modul 8 <br>QUEUE</h1>
<p align="center">NASHIR KHOIRUL HUDA - 103112400168</p>

## Dasar Teori
Queue adalah struktur data yang cara kerjanya mirip dengan antrean di loket pembelian tiket Kereta Api, di mana orang yang datang terlebih dahulu akan dilayani lebih dulu, sedangkan orang yang datang paling akhir akan dilayani paling akhir; prinsip ini disebut FIFO (*First In First Out*) atau yang pertama masuk adalah yang pertama keluar. Pada Queue, elemen yang pertama dimasukkan akan diproses lebih dulu dibandingkan elemen yang datang setelahnya, sehingga struktur ini sangat cocok digunakan untuk situasi yang memerlukan urutan layanan yang adil dan teratur. Dalam bahasa C, Queue dapat diimplementasikan menggunakan array maupun linked list, di mana array memberikan pengelolaan indeks yang lebih sederhana, sedangkan linked list memungkinkan penambahan dan penghapusan elemen dengan lebih fleksibel tanpa perlu menggeser elemen lain.


## Guided

### Guided 1
```c++
#include <iostream>
using namespace std;

#define MAX 5 // ukuran maksimal queue

// Struktur Queue
struct Queue {
    int data[MAX];
    int head;
    int tail;
};

// Membuat antrean kosong
void createQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmpty(Queue Q) {
    return (Q.head == -1 && Q.tail == -1);
}

bool isFull(Queue Q) {
    return (Q.tail == MAX - 1);
}

// Menampilkan isi antrian
void printQueue(Queue Q) {
    if (isEmpty(Q)) {
        cout << "Queue kosong!" << endl;
    } else {
        cout << "Queue : ";
        for (int i = Q.head; i <= Q.tail; i++) {
            cout << Q.data[i] << " ";
        }
        cout << endl;
    }
}

void enqueue(Queue &Q, int x) {
    if (isFull(Q)) {
        cout << "Queue penuh! Tidak bisa menambah data." << endl;
    } else {
        if (isEmpty(Q)) {
            Q.head = Q.tail = 0;
        } else {
            Q.tail++;
        }
        Q.data[Q.tail] = x;
        cout << "Enqueue: " << x << endl;
    }
}

void dequeue(Queue &Q) {
    if (isEmpty(Q)) {
        cout << "Queue kosong! Tidak ada data yang dihapus." << endl;
    } else {
        cout << "Dequeue: " << Q.data[Q.head] << endl;
        // Jika hanya 1 elemen
        if (Q.head == Q.tail) {
            Q.head = Q.tail = -1;
        } else {
            // Geser semua elemen ke kiri
            for (int i = Q.head; i < Q.tail; i++) {
                Q.data[i] = Q.data[i + 1];
            }
            Q.tail--;
        }
    }
}

int main() {
    Queue Q;
    enqueue(Q, 5);
    enqueue(Q, 2);
    enqueue(Q, 7);
    printQueue(Q);

    dequeue(Q);
    printQueue(Q);

    enqueue(Q, 4);
    enqueue(Q, 9);
    printQueue(Q);

    dequeue(Q);
    dequeue(Q);
    printQueue(Q);

    return 0;
}
```

> Output
> 
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%208/Screenshot%202025-11-18%20075538.png)

Program di atas adalah implementasi struktur data **Queue** berbasis array dengan ukuran maksimal lima elemen, menggunakan konsep **FIFO**. Queue memiliki operasi utama yaitu `enqueue()` untuk menambah data di belakang antrian dan `dequeue()` untuk menghapus data dari depan, lengkap dengan pengecekan kondisi penuh dan kosong. Saat data dihapus, elemen-elemen digeser ke kiri untuk menjaga posisi antrian. Program `main()` menampilkan contoh penggunaan queue dengan beberapa proses penambahan, penghapusan, dan penampilan isi antrian untuk memperlihatkan cara kerja struktur data tersebut.


## UNGUIDED

### Soal 1
Buatlah implementasi ADT Queue pada file “queue.cpp” dengan menerapkan mekanisme
queue Alternatif 1 (head diam, tail bergerak).

#### queue.h
```c++
#ifndef QUEUE_H
#define QUEUE_H

typedef int infotype;

typedef struct {
    infotype info[5];
    int head;
    int tail;
} Queue;

void createQueue(Queue &Q);
bool isEmptyQueue(Queue Q);
bool isFullQueue(Queue Q);
void enqueue(Queue &Q, infotype x);
infotype dequeue(Queue &Q);
void printInfo(Queue Q);

#endif
```
#### queue.cpp
```c++
#include <iostream>
#include "queue.h"
using namespace std;

void createQueue(Queue &Q) {
    Q.head = 0;
    Q.tail = -1;
    for(int i = 0; i < 5; i++) {
        Q.info[i] = 0;
    }
}

bool isEmptyQueue(Queue Q) {
    return (Q.tail < Q.head);
}

bool isFullQueue(Queue Q) {
    return (Q.tail == 4);
}

void enqueue(Queue &Q, infotype x) {
    if (!isFullQueue(Q)) {
        Q.tail++;
        Q.info[Q.tail] = x;
    } else {
        cout << "Queue Penuh!" << endl;
    }
}

infotype dequeue(Queue &Q) {
    if (!isEmptyQueue(Q)) {
        infotype x = Q.info[Q.head];

        for (int i = 0; i < Q.tail; i++) {
            Q.info[i] = Q.info[i + 1];
        }

        Q.tail--;
        return x;
    } else {
        cout << "Queue Kosong!" << endl;
        return -1;
    }
}

void printInfo(Queue Q) {
    cout << "H=" << Q.head << ", T=" << Q.tail << " | Queue Info : ";

    if (isEmptyQueue(Q)) {
        cout << "empty queue" << endl;
        return;
    }

    for (int i = Q.head; i <= Q.tail; i++) {
        cout << Q.info[i] << " ";
    }
    cout << endl;
}
```

#### main.cpp
```c++
#include <iostream>
#include "queue.h"
using namespace std;

int main() {
    cout << "Hello World" << endl;
    Queue Q;
    createQueue(Q);

    cout << "--------------------------" << endl;
    cout << "H - T \t | Queue info" << endl;
    cout << "--------------------------" << endl;

    printInfo(Q);
    enqueue(Q, 5); printInfo(Q);
    enqueue(Q, 2); printInfo(Q);
    enqueue(Q, 7); printInfo(Q);
    enqueue(Q, 4); printInfo(Q);
    dequeue(Q); printInfo(Q);
    dequeue(Q); printInfo(Q);

    return 0;
}
```
> Output soal 1
> 
> ![Screenshot bagian x]()

Program ini 


### Soal 2
Buatlah implementasi ADT Queue pada file “queue.cpp” dengan menerapkan mekanisme
queue Alternatif 2 (head bergerak, tail bergerak).

#### queue.cpp
```

```

> Output soal 2
> 
> ![Screenshot bagian x]()

Program ini


### Soal 3
Buatlah implementasi ADT Queue pada file “queue.cpp” dengan menerapkan mekanisme
queue Alternatif 3 (head dan tail berputar).

#### queue.cpp
```

```

> Output soal 3
> 
> ![Screenshot bagian x]()
> 
Program ini

## Referensi



