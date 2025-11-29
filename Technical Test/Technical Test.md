
## Technical Test:

Berikut Jawaban dari Technical test :

.


**Soal 2**

Poin a, b, dan c ada pada file xls di directory ini

c. **Saran perbaikan :**
Ada beberapa hal yang Saya rasa, Sebagai pengguna awam / baru :
1. Sebagai pengguna Saya bingung terkait fitur tambahan, option checkbox, yang Saya pribadi kurang paham definisi dari setiap opsi, dan fungsinya. Dan karena result yang dihasilkan berbeda - beda di setiap option, Saya jadi ada keraguan hasil yang benar yg mana, jadi Saya coba hitung dengan calculator hasil yang seharusnya (yg ternyata tanpa centang sama sekali)
2. Pada jargon aplikasi, tertulis 'A simple tool to compute n! instantly.' Tapi dengan adanya beberapa checkbox opsi, jadi seakan makna 'simple' itu hilang
3. Masih terkait option checkbox, Dikarenakan ini adalah perhitungan matematika, sependek sepengetahuan Saya, nilai dari perhitungan matematika adalah exact / sesuatu yang pasti , dan dapat diprediksi. Karena hasilnya bisa berbeda - beda di setiap checklist option, sekali lagi membuat Saya bingung makna dari setiap checkbox itu, mungkin untuk gamification / agak fitur nya lebih menarik dan banyak variasi (karena tidak ada informasi / definisi terkait opsi - opsi tersebut). Saran Saya diberikan tooltip informasi makna dari setiap checkbox opsi
4. button 'reload' & 'clear changes' memiliki fungsi yang tidak jauh berbeda. Berbeda nya hanya 'clear changes' tidak mereset pilihan checkbox. Jadi kesan nya seperti 2 tombol yang tidak ada bedanya. (Tapi pasti secara technical nya berbeda, krn yg 'reload' memang ada merefresh halaman sepersekian detik, untuk button 'clear changes' inputan dan reselt langsung ter-reset tanpa ada refresh halaman)


---


**Soal 3**

Pada aplikasi ini, langkah yang akan Saya rencanakan untuk mengimplementasikan automation agar stabil : 

1. Menentukan test Case yang layak untuk diautomation
Tidak semua test case yang sudah QA susun penting untuk diautomation. Test Case yang penting untuk diautomasikan biasanya :
- happy path
- Critical flow, seperti login, transaksi
- sering kali dijalankan
- Banyak terdampak / dependencies dengan fitur lain
- Memiliki sejarah BUG dengan dengan level blocker / severity critical
Untuk test case yang penting untuk diautomasi, diberi label 'will automate' pada tabel test case.

.

2. Menganalisa element - element yang dibutuhkan untuk test case - test case yang akan diautomation
- Setelah menentukan test case yang akan di automasi, penting untuk QA cek selector dari element - element yang digunakan pada test case yang akan diautomasi
- QA harus memastikan element yang akan digunakan memiliki id/class/nama yang unik, agar automation yang dibuat nantinya akan lebih stabil, dan tidak mudah flaky, jika ada perubahan UI yang minor, jadi QA hanya perlu menyesuaikan selector jika memang benar - benar ada revamp halaman major.
- Jika element - element yang diperlukan QA, ada yang belum memiliki selector unik, QA bisa minta bantuan FE dev untuk membuatkan nama selector yang unik
- Selector yang stabil, yang bisa QA mintakan dev memprovide jika belum ada, antara lain :
- a. custom attributs : data-testid, data-qa, dll
- b. ID unik : #usernameku
- c. nama : //button[name="btn_verif_email"]
- d. CSS class spesifik : .verif-email-button
- e. hindari selector yang terlalu general (//button[text()="Submit"]), xpath yang penjang yang berpotensi sering berubah (//*[@id="root"]/div[3]/div/form/div[1]/input), walaupun hanya perubahan minor di UI
- Selain memastikan selector memiliki id yang unik, QA perlu memastikan selector yang akan kita gunakan, hanya merujuk ke 1 element. Tidak 2 - 3 , bahkan lebih element
- Memastikan selector yang digunakan merujuk ke element tunggal <img width="1866" height="776" alt="image" src="https://github.com/user-attachments/assets/94ec2fa2-e579-4637-a90b-28f6ba05cfb5" />

- Bukan merujuk ke > 1 element <img width="1901" height="871" alt="image" src="https://github.com/user-attachments/assets/eaee8580-d870-403f-a227-6094719e5140" />

.

3. Mengorganisir Struktur folder & modularitas pada framework automation yang akan digunakan
- Membuat penyeragaman pengorganisiran modul, seperti ini misal ;
- a. folder Test-case
- b. folder page objects
- c. folder utilities (logger, reporting, helper)
- d. folder config (env, data test)
- e. foldur external file

.

4. Data Strategy
Data yang digunakan pada automation tidak bisa hanya sekedar data random tanpa strategy / tanpa memikirkan apakah data itu akan sustain pada waktu yang berkala, pada antar test case, dll
- Data bisa mandiri antar test case, sehingga jika Test Case A berjalan, tidak mempengaruhi Test case B, begitu juga Test Case C.
- Menggunakan data faker. Misalkan untuk email, username, dll. Misalkan menggunakan : `test_${timestamp}@mail.com`
- Di kasus aplikasi Factory ini, misal menggunakan random dari angka 0 - 170 untuk test case positif. Misalkan menggunakan : min = 0, max = 170 ->  `rand(min..max)`
- Data diletakkan pada file test data, yang nantinya akan dipanggil di tiap function yang membutuhkan data tersebut
- Dengan meletakkan test data terpusat pada file data, jika ada requirement yang berubah terkait aturan minimum dan maximum, cukup diadjust pada file test data saja, tidak perlu adjust di function / code satu persatu

