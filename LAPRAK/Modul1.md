# <h1 align="center">Laporan Praktikum Modul 01 <br>  Pengenalan C++</h1>
<p align="center">NASHIR KHOIRUL HUDA - 103112400168</p>

## Dasar Teori

Dalam C++ ada beberapa dasar penting yang biasa dipelajari, yaitu struct, aritmatika, kondisi, perulangan, dan fungsi. Struct dipakai buat ngumpulin beberapa variabel dengan tipe berbeda dalam satu wadah supaya data lebih gampang diatur. Aritmatika berhubungan sama operator kayak +, -, *, /, dan % buat ngelakuin hitungan matematis. Kondisi atau percabangan (if, else if, else, switch) dipakai biar program bisa milih jalannya sesuai syarat yang ada. Perulangan (for, while, do while) berguna buat ngejalanin kode berulang-ulang tanpa harus nulis perintah banyak kali. Sementara itu, fungsi adalah blok kode yang bisa dipanggil kapan aja buat tugas tertentu, jadi program lebih rapi, gampang dibaca, dan bisa dipakai lagi.

## Unguided

### Soal 1

Buatlah program yang menerima input-an dua buah bilangan betipe float, kemudian memberikan output-an hasil penjumlahan, pengurangan, perkalian, dan pembagian dari dua bilangan tersebut.

```go
#include <iostream>
using namespace std;

int main(){
    float x, y;

    cout << "Masukkan bilangan pertama: ";
    cin >> x;
    cout << "Masukkan bilangan kedua: ";
    cin >> y;

    float tambah = x + y;
    cout << "Hasil penjumlahan: " << x << " + " << y << " = " << tambah << endl;

    float pengurangan = x - y;
    cout << "Hasil pengekuraangan: " << x << " - " << y << " = " << pengurangan << endl;

    float perkalian = x * y;
    cout << "Hasil perkalian: " << x << " * " << y << " = " << perkalian << endl;

    if (y != 0){
        float pembagian = x / y;
        cout << "Hasil pembagian: " << x << " / " << y << " = " << pembagian << endl;
    } else {
        cout << "Pembagian dengan nol tidak dapat dilakukan." << endl;
    }

    return 0;
}
```

> Output
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/LAPRAK/jawaban%201.png)

Program di atas merupakan kalkulator sederhana yang dibuat dengan C++. Cara kerjanya, pengguna diminta memasukkan dua bilangan, lalu program otomatis menampilkan hasil penjumlahan, pengurangan, perkalian, dan pembagian dari kedua bilangan tersebut. Untuk operasi bagi, program juga sudah diberi pengaman: kalau bilangan kedua yang dimasukkan adalah nol, program akan memberi tahu bahwa pembagian tidak bisa dilakukan. Jadi, program ini bisa membantu menghitung operasi dasar secara cepat dan aman langsung lewat terminal.


### Soal 2

Buatlah sebuah program yang menerima masukan angka dan mengeluarkan output nilai angka tersebut dalam bentuk tulisan. Angka yang akan di-input-kan user adalah bilangan bulat positif mulai dari 0 s.d 100.

```go
#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Masukkan angka (0-100): ";
    cin >> n;

    cout << n << " : ";

    if (n < 0 || n > 100) {
        cout << "Input di luar jangkauan";
    }
    else if (n == 0) {
        cout << "nol";
    }
    else if (n == 100) {
        cout << "seratus";
    }
    else if (n < 12) {
        if (n == 1) cout << "satu";
        else if (n == 2) cout << "dua";
        else if (n == 3) cout << "tiga";
        else if (n == 4) cout << "empat";
        else if (n == 5) cout << "lima";
        else if (n == 6) cout << "enam";
        else if (n == 7) cout << "tujuh";
        else if (n == 8) cout << "delapan";
        else if (n == 9) cout << "sembilan";
        else if (n == 10) cout << "sepuluh";
        else if (n == 11) cout << "sebelas";
    }
    else if (n < 20) {
        int sisa = n - 10;
        if (sisa == 1) cout << "sebelas";
        else if (sisa == 2) cout << "dua belas";
        else if (sisa == 3) cout << "tiga belas";
        else if (sisa == 4) cout << "empat belas";
        else if (sisa == 5) cout << "lima belas";
        else if (sisa == 6) cout << "enam belas";
        else if (sisa == 7) cout << "tujuh belas";
        else if (sisa == 8) cout << "delapan belas";
        else if (sisa == 9) cout << "sembilan belas";
    }
    else {
        int puluh = n / 10;
        int satuan = n % 10;

        if (puluh == 2) cout << "dua puluh";
        else if (puluh == 3) cout << "tiga puluh";
        else if (puluh == 4) cout << "empat puluh";
        else if (puluh == 5) cout << "lima puluh";
        else if (puluh == 6) cout << "enam puluh";
        else if (puluh == 7) cout << "tujuh puluh";
        else if (puluh == 8) cout << "delapan puluh";
        else if (puluh == 9) cout << "sembilan puluh";

        if (satuan > 0) {
            cout << " ";
            if (satuan == 1) cout << "satu";
            else if (satuan == 2) cout << "dua";
            else if (satuan == 3) cout << "tiga";
            else if (satuan == 4) cout << "empat";
            else if (satuan == 5) cout << "lima";
            else if (satuan == 6) cout << "enam";
            else if (satuan == 7) cout << "tujuh";
            else if (satuan == 8) cout << "delapan";
            else if (satuan == 9) cout << "sembilan";
        }
    }

    cout << endl;
    return 0;
}

```

> Output
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/LAPRAK/jawaban%202.png)

Program C++ tersebut dibuat untuk mengonversi angka antara 0 hingga 100 menjadi tulisan dalam bahasa Indonesia. Ketika pengguna memasukkan angka, program lebih dulu memeriksa apakah angkanya valid; jika tidak, akan muncul pesan bahwa input berada di luar jangkauan. Angka 0 ditampilkan sebagai “nol” dan angka 100 sebagai “seratus”. Untuk bilangan di bawah 12, program langsung menuliskan sesuai sebutan dasarnya, sedangkan bilangan 12 sampai 19 ditampilkan dengan format “... belas”. Sementara itu, angka 20 sampai 99 dipecah menjadi puluhan dan satuan, lalu digabungkan sehingga membentuk tulisan yang sesuai, contohnya angka 42 menjadi “empat puluh dua”. Dengan cara ini, program dapat menampilkan angka dalam bentuk kata yang lebih jelas dan mudah dipahami.


### Soal 3

Buatlah program yang dapat memberikan input dan output sbb.

```go
#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Masukkan angka: ";
    cin >> n;

    for (int i = n; i >= 1; i--) {
        for (int spasi = 0; spasi < n - i; spasi++) {
            cout << "  ";
        }

        for (int j = i; j >= 1; j--) {
            cout << j << " ";
        }

        cout << "* ";

        for (int k = 1; k <= i; k++) {
            cout << k << " ";
        }

        cout << endl;
    }

    for (int spasi = 0; spasi < n; spasi++) {
        cout << "  ";
    }
    cout << "*" << endl;

    return 0;
}

```

> Output
> ![Screenshot bagian x](https://github.com/Nashiw/Laporan-Praktikum/blob/main/LAPRAK/jawaban%203.png)

Program C++ ini berfungsi untuk mencetak pola angka berbentuk segitiga yang simetris dengan tanda bintang (*) sebagai pemisah di bagian tengah. Setelah pengguna memasukkan angka `n`, program akan menampilkan barisan angka menurun dari `i` sampai 1 di sisi kiri, kemudian mencetak bintang, dan dilanjutkan dengan angka menaik dari 1 hingga `i` di sisi kanan. Setiap baris diawali spasi agar hasilnya rata dan rapi, lalu diakhiri dengan sebuah baris tambahan yang hanya menampilkan spasi sebanyak `n` dan sebuah bintang. Singkatnya, program ini menghasilkan pola angka yang seimbang di kiri dan kanan dengan simbol bintang di tengah sehingga membentuk tampilan yang teratur.


## Referensi

1. https://en.wikipedia.org/wiki/Data_structure (diakses blablabla)

