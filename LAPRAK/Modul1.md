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

soal nomor 2A

```go
package main

func main() {
	fmt.Println("kode untuk soal nomor 2A")
}
```

> Output
> ![Screenshot bagian x](output/screenshot_soal2A.png)

penjelasan kode

Kalau adalanjutan di lanjut disini aja

soal nomor 2B

```go
package main

func main() {
	fmt.Println("kode untuk soal nomor 2B")
}
```

> Output
> ![Screenshot bagian x](output/screenshot_soal2B.png)

penjelasan bedanya sesuai soal

## Referensi

1. https://en.wikipedia.org/wiki/Data_structure (diakses blablabla)

