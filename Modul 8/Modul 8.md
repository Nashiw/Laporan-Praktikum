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
> ![Screenshot bagian x](OUTPUT/guided1.png)

Program guided1.cpp merupakan implementasi struktur data Queue menggunakan array statis berukuran lima elemen yang bekerja dengan prinsip FIFO (First In First Out), di mana elemen pertama yang masuk akan keluar terlebih dahulu. Struktur queue memiliki atribut data, head, dan tail untuk menyimpan elemen serta menandai posisi awal dan akhir antrian. Program menyediakan fungsi enqueue() untuk menambah data ke bagian belakang antrian dan dequeue() untuk menghapus data dari bagian depan dengan menggeser elemen lain ke kiri. Dalam fungsi utama, program menambahkan beberapa elemen ke antrian, menghapus sebagian, dan menampilkan hasilnya setelah setiap operasi. Melalui program ini, pengguna dapat memahami proses dasar antrian seperti penambahan, penghapusan, dan pengecekan kondisi penuh atau kosong menggunakan representasi array di C++.

## UNGUIDED

### Soal 1
Buatlah implementasi ADT Queue pada file “queue.cpp” dengan menerapkan mekanisme
queue Alternatif 1 (head diam, tail bergerak).

#### queue.h
```

```
#### queue.cpp
```

```

#### main.cpp
```

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



