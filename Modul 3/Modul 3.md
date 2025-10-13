# <h1 align="center">Laporan Praktikum Modul 03 <br> Abstract Data Type</h1>
<p align="center">NASHIR KHOIRUL HUDA - 103112400168</p>

## Dasar Teori
Dasar teori dari program di atas berkaitan dengan Abstract Data Type (ADT) merupakan konsep dasar dalam pemrograman terstruktur yang digunakan untuk mendefinisikan tipe data baru beserta operasi-operasi dasar (primitif) yang dapat dilakukan terhadapnya. ADT bersifat abstrak karena pengguna hanya mengetahui apa yang dapat dilakukan tanpa perlu memahami bagaimana cara kerjanya secara internal. Dalam ADT biasanya terdapat konstruktor untuk membentuk objek, selector untuk mengakses nilai, mutator untuk mengubah nilai, validator untuk memeriksa keabsahan data, destruktor untuk menghapus objek, serta operator relasional, aritmatika, dan fungsi input/output sebagai antarmuka. Implementasi ADT umumnya dibagi menjadi dua bagian, yaitu file header (.h) yang berisi definisi tipe data dan deklarasi fungsi, serta file implementasi (.cpp) yang berisi realisasi fungsi tersebut. Dengan memisahkan spesifikasi dan implementasi, ADT dapat meningkatkan modularitas, reusabilitas, serta memudahkan pemeliharaan kode program.


## Guided

## Menghitung Rata Rata

## mahasiswa.h
```go
#ifndef MAHASISWA_H_INCLUDED
#define MAHASISWA_H_INCLUDED

struct mahasiswa
{
    char nim[10];
    int nilai1, nilai2;
};

void inputMhs(mahasiswa &m);
float rata2(mahasiswa m);

#endif
```

## Mahasiswa.cpp
```go
#include "mahasiswa.h"
#include <iostream>
using namespace std;

void inputMhs(mahasiswa &m)
{
    cout << "input nama = ";
    cin >> (m) .nim;
    cout << "input nilai = ";
    cin >> (m) .nilai1;
    cout << "input niali2 = ";
    cin >> m .nilai2;

}
float rata2(mahasiswa m)
{
    return float(m.nilai1 + m.nilai2) / 2;
}
```

## main.cpp
```go
#include <iostream>
#include "mahasiswa.h"
using namespace std;

int main(){
    mahasiswa mhs;
    inputMhs(mhs);
    cout << "rata rata = " << rata2(mhs);
    return 0;
}
```

## Unguided

### Soal 1

Buat program yang dapat menyimpan data mahasiswa (max. 10) ke dalam sebuah array
dengan field nama, nim, uts, uas, tugas, dan nilai akhir. Nilai akhir diperoleh dari FUNGSI
dengan rumus 0.3*uts+0.4*uas+0.3*tugas.

```go
#include <iostream>
#include <string>
using namespace std;

struct Mahasiswa {
    string nama;
    string nim;
    float uts;
    float uas;
    float tugas;
    float nilaiAkhir;
};

float hitungNilaiAkhir(float uts, float uas, float tugas) {
    return (0.3 * uts) + (0.4 * uas) + (0.3 * tugas);
}

void inputMahasiswa(Mahasiswa &mhs) {
    cout << "Masukkan Nama   : ";
    getline(cin, mhs.nama);
    cout << "Masukkan NIM    : ";
    getline(cin, mhs.nim);
    cout << "Masukkan Nilai UTS   : ";
    cin >> mhs.uts;
    cout << "Masukkan Nilai UAS   : ";
    cin >> mhs.uas;
    cout << "Masukkan Nilai Tugas : ";
    cin >> mhs.tugas;
    cin.ignore(); 
    mhs.nilaiAkhir = hitungNilaiAkhir(mhs.uts, mhs.uas, mhs.tugas);
}

void tampilMahasiswa(Mahasiswa mhs[], int jumlah) {
    cout << "\n==============================================\n";
    cout << "Daftar Data Mahasiswa\n";
    cout << "==============================================\n";
    for (int i = 0; i < jumlah; i++) {
        cout << "Mahasiswa ke-" << i + 1 << endl;
        cout << "Nama         : " << mhs[i].nama << endl;
        cout << "NIM          : " << mhs[i].nim << endl;
        cout << "UTS          : " << mhs[i].uts << endl;
        cout << "UAS          : " << mhs[i].uas << endl;
        cout << "Tugas        : " << mhs[i].tugas << endl;
        cout << "Nilai Akhir  : " << mhs[i].nilaiAkhir << endl;
        cout << "----------------------------------------------\n";
    }
}

int main() {
    Mahasiswa daftarMhs[10];
    int jumlah;

    cout << "Masukkan jumlah mahasiswa (max 10): ";
    cin >> jumlah;
    cin.ignore();

    if (jumlah > 10) {
        cout << "Jumlah melebihi batas maksimum (10)!" << endl;
        return 0;
    }

    for (int i = 0; i < jumlah; i++) {
        cout << "\nInput data mahasiswa ke-" << i + 1 << endl;
        inputMahasiswa(daftarMhs[i]);
    }

    tampilMahasiswa(daftarMhs, jumlah);

    return 0;
}
```

> Output
> ![Screenshot bagian x]()

Program di atas berfungsi untuk melakukan transpose pada sebuah matriks berukuran 3x3 menggunakan bahasa C++. Pertama, matriks awal diinisialisasi dengan elemen bernilai 1 hingga 9. Kemudian, dibuat matriks baru bernama `transpose` untuk menyimpan hasil penukaran baris dan kolom. Proses transpose dilakukan dengan menggunakan dua perulangan bersarang, di mana setiap elemen `matriks[i][j]` ditukar posisinya menjadi `transpose[j][i]`, sehingga baris menjadi kolom dan sebaliknya. Setelah proses selesai, program menampilkan matriks awal dan matriks hasil transpose ke layar, sehingga pengguna dapat melihat perbedaan antara keduanya.


### Soal 2




```go
#include <iostream>
using namespace std;

void kuadratkan(int &x) {
    x = x * x;
}

int main() {
    int nilai = 5;

    cout << "Nilai awal: " << nilai << endl;

    kuadratkan(nilai);

    cout << "Nilai setelah dikuadratkan: " << nilai << endl;

    return 0;
}

```

> Output
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/modul%202/jawaban%20no%202.png))

Program di atas digunakan untuk **mengkuadratkan sebuah bilangan menggunakan konsep *call by reference*** dalam bahasa C++. Variabel `nilai` diinisialisasi dengan angka 5, lalu ditampilkan sebagai nilai awal. Fungsi `kuadratkan(int &x)` menerima parameter berupa *reference* (`&`), sehingga setiap perubahan pada variabel `x` di dalam fungsi akan langsung mengubah nilai asli di luar fungsi. Di dalam fungsi, nilai `x` dikalikan dengan dirinya sendiri (`x = x * x`), sehingga hasilnya adalah kuadrat dari nilai awal. Setelah fungsi dipanggil, program menampilkan nilai yang sudah dikuadratkan, yaitu 25.
## Referensi

1. https://www.w3schools.com/cpp/cpp_arrays.asp
2. https://www.w3schools.com/cpp/cpp_references.asp
3. https://www.w3schools.com/cpp/cpp_pointers.asp
