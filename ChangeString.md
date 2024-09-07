# Solusi Change String (Rada gak niat tapi)
Problem : https://tlx.toki.id/problems/arkavidia-8-pc-final/C

## Definisi
Berikut merupakan beberapa definisi yang akan digunakan pada solusi ini
1. $$n$$ ialah bilangan bulat terbesar sehingga $$2^n \leq N$$
2. Urutan string dinyatakan dari karakter terakhir dengan indeks 1, dengan kata lain karakter pertama "ABC" ialah "C" dan karakter ketiganya ialah "A". Pendefenisian ini digunakan untuk memudahkan penulisan solusi. Di sisi lain, pendefinisian substring tetap dari kiri ke kanan (i.e. substring dari karakter ke-6 sampai karakter ke-4)
3. Suatu string dapat dinotasikan sebagai $$P(p_n, p_{n-1}, \ldots, p_1, p_0)$$, dengan $$p_i$$ menyatakan banyaknya karakter ke- $$m$$ yang merupakan "A" dalam modulo 2, dan $$m$$ memenuhi $$2^i || m$$. Sebagai contoh, "AABA" memiliki notasi $$P(1,0,0)$$ dan "BAABAAAB" memiliki notasi $$P(0,1,0,0)$$. Perlu diperhatikan bahwa dua buah string yang berbeda dapat memiliki notasi yang sama. Lebih lanjut, notasi $$\bar{P}(p_n, p_{n-1}, \ldots, p_1, p_0)$$ menyatakan negasi dari notasi $$P$$. 

## Ide Utama
Pemain akan selalu dapat melakukan langkah kecuali jika semua karakter pada string ialah "B". Sehingga keadaan kalahnya ialah "BBB...BB" yang memiliki notasi $$P(0,0,0,...,0,0)$$. Di sini, kita akan membuktikan bahwa semua string dengan notasi tersebut ialah *losing position*, sedangkan string lain ialah *winning position*. Untuk membuktikan hal tersebut, kita akan membuktikan dua hal ini.
1. Setiap langkah dari string $$P(0,0,...,0)$$ akan menghasilkan $$\bar{P}(0,0,...,0)$$.
2. Untuk setiap string $$\bar{P}(0,0,...,0)$$, pasti selalu ada setidaknya satu buah langkah yang membuat string tersebut menjadi $$P(0,0,...,0)$$.

## Bukti Poin 1
- Jika substring yang diambil memiliki panjang 1, sudah jelas bahwa pasti ada suatu $$i$$ sehingga $$p_i=1$$.
- Jika substring yang diambil memiliki panjang lebih dari 1, misalkan substring tersebut diambil dari karakter ke- $$l$$ sampai karakter ke- $$r$$ (inklusif), dengan $$l>r$$. Misalkan bit ke- $$k$$ dari $$l$$ dan $$r$$ merupakan bit paling kiri yang berbeda. Karena $$l>r$$, jelas bahwa bit ke- $$k$$ dari $$l$$ pasti 1 dan bit ke- $$k$$ dari $$r$$ pasti 0. Setelah melakukan langkah, dapat dipastikan juga bahwa $$p_k$$ pasti menjadi 1 karena hanya ada satu bilangan $$x$$ sehingga $$2^k||x$$ dengan $$r\leq x \leq l$$.

Oleh karena itu, poin 1 terbukti.

## Bukti Poin 2
Misalkan $$\alpha$$ merupakan bilangan bulat nonnegatif paling besar sehingga $$p_\alpha = 1$$. Oleh karena itu, pasti ada bilangan bulat nonnegatif $$a$$ sehingga $$2^\alpha || a$$ dan karakter ke- $$a$$ merupakan "A". 

### Klaim 
Terdapat sebuah $$b$$ dengan $$b \geq a - 2^\alpha + 1$$ sehingga substring yang dipilih ialah dari karakter ke- $$a$$ sampai karakter ke- $$b$$ dapat membuat string tersebut menjadi $$P(0,0,...,0)$$.

### Bukti
Nilai $$b$$ dapat di-*construct* dengan cara mengecek apakah string tersebut perlu untuk mengubah $$p_{\alpha-1}$$. Jika perlu, maka $$b \leq a - 2^{\alpha-1}$$, kemudian perbarui $$P$$ karena karakter-karakter dari karakter ke- $$a$$ sampai karakter ke-($$a - 2^{\alpha-1}$$) pasti diubah. Jika tidak, maka $$b > a - 2^{\alpha-1}$$. Kemudian, hal tersebut dapat dilakukan untuk $$p_{\alpha-2},p_{\alpha-3},$$ dst. (Intinya mirip *binary search* tapi bingung cara jelasinnya gimana, terus ntar pasti jarak $$b$$ dari $$a$$ ga bakal $$2^\alpha$$ atau lebih gitu deh, lebih enak jelasin pake pidio + gambar tbh anggep aja terbukti)

## Konklusi
Jadi, terbukti bahwa $$P(0,0,\ldots,0)$$ merupakan *losing position*, dan $$\bar{P}(0,0,\ldots,0)$$ merupakan *winning position*. Implementasinya cukup sederhana.
1. Siapkan vektor `p`, inisialisasi semua elemennya dengan 0.
2. Iterasi string dari belakang
   a. Jika karakter ke- $$i$$ ialah "A", tambahkan `p[trailing_zero(i)]` dengan 1 (dalam modulo 2)
3. Jika semua elemen `p` bernilai 0, orang kedua menang. Jika tidak, orang pertama menang.

Kompleksitas : $$O(N \log N)$$ (???)


## Kode
```c++
cout << "Koding sendiri sana! >:(";
```


