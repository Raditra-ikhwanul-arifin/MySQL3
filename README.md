# Tugas Praktikum { Pertemuan ke 10 }


|**Nama**|**NIM**|**Kelas**|**Matkul**|
|----|---|-----|------|
|Raditra Ikhwanul Arifin|312310487|TI.23.A.5|Basis Data|

# Soal Latihan Praktikum

1. Lakukan penambahan data pada tabel mahasiswa dengan mengisi kd_ds yang belum ada pada data dosen.
dengan menggunakan kode berikut :
```
INSERT INTO dosen (kd_ds, nama) VALUES
('DS001', 'Arif'),
('DS002', 'Bagus'),
('DS003', 'Iqbal'),
('DS004', 'Radit'),
('DS005', 'Uyun');
```

![alt text](<ss/tambah data1.JPG>)

***Output :***

![alt text](ss/output1.JPG)

2. Hapus satu record data pada tabel dosen yang telah dirujuk pada tabel mahasiswa. 
```
DELETE FROM dosen WHERE kd_ds = 'DS005';
```
***Output :***

![alt text](ss/output2.JPG)

3. Ubah mode menjadi **ON UPDATE CASCADE ON DELETE RESTRICT** 

Untuk mengubah CONSTRAINT FOREIGN KEY menjadi **ON UPDATE CASCADE** dan **ON DELETE RESTRICT**, Anda perlu menambahkan CONSTRAINT dengan opsi yang diinginkan. Berikut adalah langkah-langkahnya:

Tambahkan CONSTRAINT FOREIGN KEY dengan opsi ON UPDATE CASCADE dan ON DELETE RESTRICT:
```
ALTER TABLE mahasiswa
ADD CONSTRAINT fk_dosen
FOREIGN KEY (kd_ds)
REFERENCES dosen (kd_ds)
ON UPDATE CASCADE
ON DELETE RESTRICT;
```
***Output :***

![alt text](<ss/on update.JPG>)

4. Lakukan perubahan data pada tabel dosen (kd_ds)

Berikut adalah contoh perintah untuk melakukan perubahan data pada tabel "dosen" dengan kolom "kd_ds":
```
UPDATE dosen SET kd_ds = 'DS005' WHERE nama = 'Radit';
```
Perintah di atas akan mengubah nilai kolom `"kd_ds" "Radit" menjadi "DS005" pada tabel "dosen"`. Anda dapat menyesuaikan nilai yang ingin Anda ubah dan kondisi WHERE sesuai dengan kebutuhan Anda.

Pastikan untuk menjalankan perintah dengan hati-hati dan memastikan bahwa perubahan data yang Anda lakukan sesuai dengan kebutuhan dan kebijakan yang berlaku dalam basis data Anda.

***Output :***

![alt text](<ss/output on update.JPG>)

5. Lakukan penghapusan data pada tabel dosen

Untuk menghapus data dari tabel "dosen" dengan kondisi "kd_ds = 'DS006'", Anda dapat menggunakan perintah DELETE dengan sintaks yang benar. Berikut adalah contoh perintah yang dapat Anda gunakan:
```
DELETE FROM Dosen WHERE kd_ds = 'DS006';
```

***Output :***


![alt text](<ss/output delet dosen.JPG>)

6. Ubah mode menjadi **ON UPDATE CASCADE ON DELETE SET NULL**
```
ALTER TABLE mahasiswa
DROP FOREIGN KEY fk_dosen;
```
```
ALTER TABLE mahasiswa
ADD CONSTRAINT fk_dosen
FOREIGN KEY (kd_ds) REFERENCES dosen (kd_ds)
ON UPDATE CASCADE ON DELETE SET NULL;
```
***Output :***

![alt text](<ss/output 6.JPG>)

Dengan perubahan di atas, ketika Anda menghapus record dari tabel "dosen" yang memiliki referensi di tabel "mahasiswa", nilai kolom "kd_ds" dalam tabel "mahasiswa" yang mengacu pada record yang dihapus akan diatur menjadi NULL.

Setelah menjalankan perintah di atas, Anda dapat kembali mencoba menghapus record dengan menggunakan perintah berikut:

7. Lakukan penghapusan data pada tabel dosen
```
DELETE FROM dosen WHERE kd_ds = 'DS003';
```
***0utput :***

![alt text](<ss/output 7.JPG>)

Perintah ini akan menghapus record dengan nilai "DS003" dari tabel "dosen", dan karena menggunakan opsi ON DELETE SET NULL, nilai kolom "kd_ds" dalam tabel "mahasiswa" yang mengacu pada record yang dihapus akan diatur menjadi NULL.

# Evaluasi dan Pertanyaan

### Tulis semua perintah-perintah SQL percobaan di atas beserta outputnya!

- Membuat foreign key

Dalam ALTER TABLE:
```
ALTER TABLE mahasiswa
ADD CONSTRAINT fk_dosen
FOREIGN KEY (kd_ds) REFERENCES dosen(kd_ds)
```

Dalam CREATE TABLE:
```
CREATE TABLE mahasiswa(
nim VARCHAR(10) NOT NULL,
nama VARCHAR(100) NOT NULL,
kd_ds VARCHAR(10),
PRIMARY KEY(nim),
CONSTRAINT fk_Dosen FOREIGN KEY (kd_ds)
REFERENCES dosen(kd_ds)
);
```

- Mengubah data
```
UPDATE mahasiswa
SET kd_ds = 'DS001' WHERE nim = 112233445;
```

- Menampilkan CREATE TABLE
```
SHOW CREATE TABLE  mahasiswa;
Mode ON UPDATE CASCADE ON DELETE CASCADE
```
```
ALTER TABLE mahasiswa
DROP FOREIGN KEY fk_mahasiswa_dosen,
ADD CONSTRAINT fk_dosen FOREIGN KEY (kd_ds) REFERENCES dosen(kd_ds) ON UPDATE CASCADE ON DELETE CASCADE;
```

- Menghapus data
```
DELETE FROM dosen WHERE kd_ds = 'DS001';
Mode ON UPDATE CASCADE ON DELETE NOT NULL
```
```
ALTER TABLE <table>
DROP FOREIGN KEY <nama_constraint_lama>,
ADD CONSTRAINT <nama_constraint_baru> FOREIGN KEY (field) REFERENCES <table_references(filed_references)> ON UPDATE CASCADE ON DELETE NOT NULL;
```

- Mengubah data
```
UPDATE dosen
SET kd_ds = 'DS006' WHERE nama = 'Haha Hihi';
```

- Menghapus data
```
DELETE FROM dosen WHERE nim = 'DS003';
```

### Apa bedanya penggunaan RESTRICT dan penggunaan CASCADE

- **RESTRICT:** Ketika Anda menggunakan opsi RESTRICT, itu berarti bahwa tindakan penghapusan atau pembaruan yang Anda lakukan akan ditolak jika ada data yang memiliki hubungan referensial dengan data yang akan dihapus atau diperbarui. Dengan kata lain, RESTRICT menghentikan tindakan tersebut jika menyebabkan konflik referensial. Misalnya, jika Anda mencoba menghapus sebuah baris dalam tabel yang memiliki anak-anak yang terhubung melalui kunci asing, operasi penghapusan akan ditolak jika ada ketergantungan referensial yang berlaku. RESTRICT secara efektif membatasi tindakan Anda agar tidak merusak integritas referensial dalam basis data.

- **CASCADE:** Sebaliknya, ketika Anda menggunakan opsi CASCADE, itu berarti bahwa tindakan penghapusan atau pembaruan yang Anda lakukan akan mempengaruhi semua data yang memiliki hubungan referensial dengan data yang dihapus atau diperbarui. Dengan kata lain, CASCADE akan melakukan tindakan yang sama pada data yang terkait. Misalnya, jika Anda menghapus sebuah baris dalam tabel yang memiliki anak-anak yang terkait melalui kunci asing dengan opsi CASCADE, operasi penghapusan akan mempengaruhi tidak hanya baris yang dihapus tetapi juga semua baris anak yang terkait secara rekursif. Hal ini berguna ketika Anda ingin menghapus semua data terkait dengan entitas utama atau memperbarui nilai di semua tempat yang menggunakan entitas tersebut.

Dalam banyak kasus, pemilihan antara `RESTRICT dan CASCADE `tergantung pada kebutuhan bisnis dan hubungan data dalam basis data. Jika Anda ingin memastikan integritas referensial dan mencegah tindakan yang dapat merusak data, Anda dapat menggunakan RESTRICT. Namun, jika Anda ingin melakukan tindakan yang berdampak luas pada data yang terkait, Anda dapat menggunakan CASCADE.

### Berikan Kesimpulan anda !

- SQL Constraint digunakan untuk menentukan aturan untuk data dalam tabel.

  - Constraint digunakan untuk membatasi jenis data yang bisa masuk ke tabel. Ini memastikan keakuratan dan keandalan data dalam tabel.

  - Constraint dapat berupa level kolom atau level tabel.

  - Constraint level kolom berlaku untuk kolom, dan batasan level tabel berlaku untuk seluruh tabel.

- **RESTRICT** membatasi tindakan penghapusan atau pembaruan jika ada ketergantungan referensial yang akan terganggu. Ini menjaga integritas referensial dalam basis data.

- **CASCADE** melakukan tindakan yang sama pada data yang terkait. Jika Anda menghapus atau memperbarui data, CASCADE akan mempengaruhi semua data terkait, termasuk data anak yang terhubung secara rekursif.  

### Buat laporan praktikum yang berisi, langkah-langkah praktikum beserta screenshot yang sudah dilakukan dalam bentuk dokumen.

<img src=https://pngimg.com/uploads/google_drive/google_drive_PNG9.png width="110px" >



## FINISH