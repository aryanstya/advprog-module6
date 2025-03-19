# Refleksi Commit 1

Kode ini membuat sebuah *TCP listener* pada alamat 127.0.0.1:7878, dan setiap koneksi yang masuk akan diteruskan ke fungsi `handle_connection`. Di dalam `handle_connection`, objek `TcpStream` dibungkus dengan `BufReader`, yang digunakan untuk membaca baris demi baris hingga menemukan baris kosong yang menandakan akhir dari *header* permintaan. Baris-baris header tersebut kemudian dikumpulkan ke dalam sebuah *vector* dan ditampilkan di konsol, memperlihatkan detail permintaan HTTP yang biasa. Karena tidak ada respons yang dikirimkan kembali, peramban atau perangkat lunak lain yang membuka koneksi akan terus menunggu hingga koneksi mengalami *timeout*.


# Refleksi Commit 2
![Commit 2 screen capture](assets/images/commit2.png)

Setelah dimodifikasi, fungsi `handle_connection` kini mengembalikan respons berupa HTML. Konten HTML tersebut dibaca dari file *hello.html* menggunakan `fs::read_to_string` dan disimpan dalam variabel `contents` sebagai sebuah *String*. Selain itu, *response body* juga dilengkapi dengan status line dan header `Content-Length`, yang penting untuk menunjukkan apakah koneksi berhasil atau gagal, serta memastikan panjang respons yang dikirim. Terakhir, `format!` digunakan untuk menggabungkan status line, `Content-Length`, dan isi HTML menjadi satu string utuh, yang kemudian dikirim melalui koneksi TCP menggunakan `stream.write_all()`.
