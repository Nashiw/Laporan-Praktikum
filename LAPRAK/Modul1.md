# <h1 align="center">Laporan Praktikum Modul 01 <br>  Pengenalan C++</h1>
<p align="center">NASHIR KHOIRUL HUDA - 103112400168</p>

## Dasar Teori

yang panjang dikit

## Unguided

### soal 1

aku mengerjakan perulangan

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
> %% Untuk mencantumkan screenshot, tidak boleh ada spasi di urlnya `()`, penamaan file bebas asal gak sara dan mudah dipahami aja,, dan jangan lupa hapus komen ini yah%%

Penjelasan ttg kode kalian disini

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

penjelasan kode

Kalau adalanjutan di lanjut disini aja

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

penjelasan bedanya sesuai soal

## Referensi

1. https://en.wikipedia.org/wiki/Data_structure (diakses blablabla)

