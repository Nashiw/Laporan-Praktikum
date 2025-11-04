# <h1 align="center">Laporan Praktikum Modul 7 <br> Stack</h1>
<p align="center">Nashir Khoirul Huda - 103112400168</p>

## Dasar Teori
Dasar teori dari program stack ini adalah bahwa **stack** merupakan salah satu bentuk struktur data linear yang bekerja berdasarkan prinsip **LIFO (Last In First Out)**, artinya elemen yang terakhir dimasukkan akan menjadi elemen pertama yang diambil. Stack dapat direpresentasikan menggunakan **array** atau **pointer**, dengan satu penunjuk utama yang disebut **TOP** untuk menunjukkan posisi elemen teratas. Operasi dasar pada stack meliputi **push** (menambah elemen ke atas stack), **pop** (menghapus elemen dari atas stack), dan **printInfo** (menampilkan isi stack). Selain itu, dapat ditambahkan operasi tambahan seperti **balikStack** untuk membalik urutan data, **pushAscending** untuk menyisipkan elemen agar tetap terurut menaik, serta **getInputStream** untuk membaca input secara berurutan dari pengguna. Dengan implementasi berbasis array, stack memiliki batas ukuran tetap, namun mudah diakses karena indeks dapat digunakan langsung tanpa manajemen memori dinamis.

## Guide

```go
#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node *next;
};

bool isEmpety(Node *top)
{
    return top == nullptr;
}

void push(Node *&top, int data){
    Node *newNode = new Node;
    newNode -> data = data;
    newNode -> next = top;
    top = newNode;
}

int pop(Node *&top)
{
    if (isEmpety(top))
    {
        cout << "Stack Kosong, tidak bisa pop!" << endl;
        return 0;
    }

    int poppedData = top -> data;
    top = top -> next;

    Node *temp;
    return poppedData;
}

void show (Node *top)
{
    if (isEmpety(top))
    {
        cout << "Stack kosong," << endl;
        return;
    }
    cout << "TOP -> ";
    Node *temp = top;

    while (temp != nullptr)
    {
        cout << temp->data << "-> ";
        temp = temp->next;
    }

    cout << "NULL" << endl;

}

int main()
{
    Node *stack = nullptr;

    push(stack, 10);
    push(stack, 20);
    push(stack, 30);

    cout << "Menampilkan isi stack:" << endl;
    show (stack);

    cout << "pop;" << pop(stack) << endl;

    cout << "Menampilkan sisa Stack:" << endl;
    show(stack);

    return 0;
}
```


## Unguide

### Soal 1

### stack.h
```go
#ifndef STACK_H
#define STACK_H

const int MAX = 20;

typedef int infotype;

struct Stack {
    infotype info[MAX];
    int top;
};

void createStack(Stack &S);
void push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);

#endif

```

### stack.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

void createStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype x) {
    if (S.top < MAX - 1) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

infotype pop(Stack &S) {
    if (S.top >= 0) {
        infotype x = S.info[S.top];
        S.top--;
        return x;
    } else {
        cout << "Stack kosong!" << endl;
        return -1;
    }
}

void printInfo(Stack S) {
    cout << "[TOP] ";
    for (int i = S.top; i >= 0; i--) {
        cout << S.info[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp;
    createStack(temp);

    while (S.top >= 0) {
        push(temp, pop(S));
    }

    S = temp;
}

```

### main.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

int main() {
    cout << "Hello world!" << endl;

    Stack S;
    createStack(S);

    push(S, 3);
    push(S, 4);
    push(S, 2);
    push(S, 9);
    pop(S);
    push(S, 8);
    pop(S);
    push(S, 2);
    pop(S);
    push(S, 3);
    push(S, 9);

    printInfo(S);
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);

    return 0;
}
   
```

> Output
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%207/jawaban%201.png)

Pada program pertama,dibuat sebuah ADT Stack yang diimplementasikan menggunakan array. Stack memiliki atribut berupa array info untuk menyimpan data dan variabel top sebagai penanda elemen paling atas pada stack. Fungsi createStack() digunakan untuk menginisialisasi stack dalam kondisi kosong dengan menetapkan nilai top = -1. Operasi push() berfungsi untuk menambahkan elemen baru ke bagian atas stack selama kapasitas belum penuh, sedangkan pop() digunakan untuk menghapus elemen teratas dan mengembalikannya. Prosedur printInfo() menampilkan isi stack mulai dari elemen teratas hingga elemen paling bawah. Selain itu, tersedia prosedur balikStack() yang membalik urutan elemen dalam stack dengan memindahkan elemen satu per satu ke stack sementara, lalu mengembalikannya sehingga urutannya menjadi terbalik. Secara keseluruhan, stack pada nomor ini bekerja mengikuti prinsip LIFO (Last In First Out). 

### Soal 2

### stack.h
```go
#ifndef STACK_H
#define STACK_H

const int MAX = 20;
typedef int infotype;

struct Stack {
    infotype info[MAX];
    int top;
};

void createStack(Stack &S);
void push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);
void pushAscending(Stack &S, infotype x);

#endif

```

### stack.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

void createStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype x) {
    if (S.top < MAX - 1) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

infotype pop(Stack &S) {
    if (S.top >= 0) {
        infotype x = S.info[S.top];
        S.top--;
        return x;
    } else {
        cout << "Stack kosong!" << endl;
        return -1;
    }
}

void printInfo(Stack S) {
    cout << "[TOP] ";
    for (int i = S.top; i >= 0; i--) {
        cout << S.info[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp;
    createStack(temp);
    while (S.top >= 0) {
        push(temp, pop(S));
    }
    S = temp;
}

void pushAscending(Stack &S, infotype x) {
    Stack temp;
    createStack(temp);

    while (S.top >= 0 && S.info[S.top] > x) {
        push(temp, pop(S));
    }

    push(S, x);

    while (temp.top >= 0) {
        push(S, pop(temp));
    }
}

```

### main.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

int main() {
    cout << "Hello world!" << endl;

    Stack S;
    createStack(S);

    pushAscending(S, 3);
    pushAscending(S, 4);
    pushAscending(S, 8);
    pushAscending(S, 2);
    pushAscending(S, 3);
    pushAscending(S, 9);

    printInfo(S);

    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);

    return 0;
}

```

> Output
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%207/jawaban%202.png)

Pada program kedua,ditambahkan prosedur pushAscending() yang berfungsi untuk mempertahankan urutan elemen dalam stack tetap ascending (menaik) dari bawah ke atas setelah proses penyisipan data. Cara kerjanya adalah dengan membuat stack sementara, kemudian memindahkan elemen-elemen yang memiliki nilai lebih besar dibandingkan nilai yang akan disisipkan ke stack sementara tersebut. Setelah posisi yang tepat ditemukan, data baru dimasukkan ke stack utama menggunakan push(). Selanjutnya, semua elemen dari stack sementara dipindahkan kembali ke stack utama. Dengan mekanisme ini, urutan ascending pada stack tetap terjaga meskipun proses penyisipan dilakukan berulang-ulang. Ketika stack ditampilkan dengan printInfo(), nilai yang terlihat dari atas ke bawah menjadi tampak seperti descending, namun sebenarnya dari bawah ke atas tersusun ascending. 

### Soal 3


### stack.h
```go
#ifndef STACK_H
#define STACK_H

const int MAX = 20;
typedef int infotype;

struct Stack {
    infotype info[MAX];
    int top;
};

void createStack(Stack &S);
void push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);
void getInputStream(Stack &S);

#endif

```

### stack.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

void createStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype x) {
    if (S.top < MAX - 1) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

infotype pop(Stack &S) {
    if (S.top >= 0) {
        infotype x = S.info[S.top];
        S.top--;
        return x;
    } else {
        cout << "Stack kosong!" << endl;
        return -1;
    }
}

void printInfo(Stack S) {
    cout << "[TOP] ";
    for (int i = S.top; i >= 0; i--) {
        cout << S.info[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp;
    createStack(temp);
    while (S.top >= 0) {
        push(temp, pop(S));
    }
    S = temp;
}

void getInputStream(Stack &S) {
    cout << "Masukkan angka (ENTER untuk selesai): ";

    char c;
    cin.get(c); 

    while (c != '\n') {     
        if (c >= '0' && c <= '9') {   
            push(S, c - '0');        
        }
        cin.get(c);
    }
}   
 
```

### main.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

int main() {
    cout << "Hello world!" << endl;

    Stack S;
    createStack(S);

    getInputStream(S);
    printInfo(S);

    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);

    return 0;
}

```

> Output
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/Modul%207/jawaban%203.png)

Pada program ketiga,ditambahkan prosedur getInputStream() yang memungkinkan program membaca input pengguna secara langsung dalam bentuk karakter satu per satu tanpa perlu dipisahkan spasi. Proses pembacaan dilakukan menggunakan cin.get() sehingga setiap karakter yang dimasukkan dapat diproses hingga pengguna menekan tombol ENTER sebagai tanda selesai. Jika karakter yang terbaca merupakan angka, maka karakter tersebut dikonversi menjadi nilai integer dan dimasukkan ke dalam stack menggunakan push(). Dengan cara ini, pengguna dapat memasukkan deretan angka seperti string, misalnya 4729601, dan angka-angka tersebut otomatis disimpan dalam stack secara berurutan sesuai urutan input. Dengan demikian, getInputStream() memberikan cara input yang lebih fleksibel dan sederhana bagi pengguna saat mengisi stack.

## Referensi
1. https://www.w3schools.com/cpp/cpp_functions.asp
2. https://www.w3schools.com/cpp/cpp_arrays.asp
3. https://www.w3schools.com/cpp/cpp_user_input.asp
4. https://www.w3schools.com/cpp/cpp_while_loop.asp
5. https://www.w3schools.com/cpp/cpp_stacks.asp

