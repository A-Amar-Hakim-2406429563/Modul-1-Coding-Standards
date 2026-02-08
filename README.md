# Reflection 1

Pada modul ini, saya telah mengimplementasikan dua fitur baru pada aplikasi e-shop menggunakan Spring Boot, yaitu fitur **Edit Product** dan **Delete Product** yang masing-masing fitur berada pada branch nya masing-masing. Dari proses pengembangan fitur tersebut, saya melakukan evaluasi terhadap penerapan *clean code principles* dan *secure coding practices* yang telah saya pelajari di minggu pertama kuliah ini dan dari Module 01 - Coding Standards juga.

## Clean Code Principles yang Diterapkan

1. **Separation of Concerns (SoC)**  
Aplikasi dibangun menggunakan arsitektur MVC (Model-View-Controller) karena menggunakan Spring Boot.
    - Controller bertanggung jawab menangani HTTP request dan response nya (mirip dengan view pada Django dengan arsitektur MVT).
    - Service berisi logika bisnis aplikasi.
    - Repository menangani pengelolaan data produk.
Pemisahan ini membuat kode lebih terstruktur dan mudah dipelihara.

2. **Penamaan Kelas dan Method yang Jelas**
Nama kelas dan method seperti `ProductController`, `ProductService`, `create()`, `findAll()`, `update()`, dan `delete()` sudah mencerminkan fungsinya masing-masing sehingga mudah dipahami dan di maintain.

3. **Single Responsibility Principle**  
Setiap class hanya memiliki satu tanggung jawab utama. Contohnya: `ProductRepository` hanya bertanggung jawab terhadap pengelolaan data produk, tanpa mengandung logika tampilan atau request handling.

4. **Kode Mudah Dibaca dan Tidak Duplikatif**  
Logika bisnis tidak ditulis langsung di controller, melainkan diserahkan dulu ke service untuk ditangani. Hal ini dilakukan untuk menghindari duplikasi kode dan membuat controller tetap sederhana.

## Secure Coding Practices yang Diterapkan

1. **Penggunaan Model Binding**  
Data dari form aku ini akan di handle menggunakan `@ModelAttribute`, sehingga tidak perlu memproses parameter request secara manual. Hal ini mengurangi risiko kesalahan input handling.

2. **Tidak Mengakses Data Secara Langsung dari View**  
View (Thymeleaf) hanya menerima data dari model yang disiapkan oleh controller, sehingga tidak ada logika bisnis yang bocor ke layer tampilan.

3. **Validasi Alur Akses Data**  
Operasi edit dan delete dilakukan berdasarkan `productId`, sehingga setiap perubahan data dapat diidentifikasi dengan jelas karena tiap id itu bersifat unik.

4. **Konfirmasi Aksi Delete**  
Pada fitur delete product, ditambahkan konfirmasi sebelum penghapusan data untuk mencegah penghapusan yang tidak disengaja.

## Evaluasi dan Perbaikan yang Dapat Dilakukan

1. **Belum Ada Validasi Input**  
Saat ini belum terdapat validasi untuk memastikan bahwa `productName` tidak kosong dan `productQuantity` tidak bernilai negatif. Perbaikan dapat dilakukan dengan menambahkan validasi menggunakan annotation seperti `@NotBlank` dan `@Min`.

2. **Penyimpanan Data Masih Menggunakan In-Memory List**  
Data produk masih disimpan dalam `List` di memory, sehingga akan hilang ketika aplikasi di-restart. Ke depannya, aplikasi dapat ditingkatkan dengan menggunakan database dan Spring Data JPA.

3. **Belum Ada Penanganan Error Secara Eksplisit**  
Jika `productId` tidak ditemukan saat edit atau delete, aplikasi belum memberikan feedback khusus. Hal ini dapat diperbaiki dengan menambahkan error handling atau halaman error custom.

4. **Konfirmasi Dengan Menggunakan Modal**
Sekarang ini aku hanya baru mengimplementasikan konfirmasi dengan confirm() saja (misal di saat ingin men-delete suatu product) yang mana ini adalah built-in JavaScript dialog, tetapi kode ini masih bisa diperbagus dengan menggunakan modal untuk konfirmasinya.

## Kesimpulan

Secara keseluruhan, implementasi fitur Edit dan Delete Product telah menerapkan prinsip clean code dan dasar secure coding dengan baik. Struktur kode sudah rapi, mudah dipahami, dan mengikuti pola yang dianjurkan dalam Spring Boot dan dalam perkuliahan Adpro ini. Beberapa perbaikan masih dapat dilakukan untuk meningkatkan dan memperbagus kualitas aplikasi, terutama pada aspek yang telah aku sebutkan diatas.