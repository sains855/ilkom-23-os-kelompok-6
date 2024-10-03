# ilkom-23-os-kelompok-6
docker adalah sebuah sistem manajemen server berbasis CI/CD

Kelebihan Docker:
1. Docker memberikan tingkat isolasi yang tinggi antara sistem host dan aplikasi yang terkontainerisasi, memastikan bahwa masalah atau kerentanan tertentu terdapat di dalam kontainer.
2. Docker memiliki konfigurasi yang mudah disesuaikan sesuai kebutuhan aplikasi, sehingga dapat menciptakan lingkungan terpisah dari server utama hanya dengan beberapa kode.
3. Docker sangat fleksibel karena dapat dijalankan di berbagai sistem operasi, seperti Linux, MacOS, dan Windows.
4. Docker dapat dijalankan di berbagai platform cloud, memberikan fleksibilitas dalam porting aplikasi.

   Docker memiliki banyak keunggulan, namun juga memiliki beberapa kekurangan yang perlu diperhatikan, terutama ketika digunakan dalam skala besar atau dalam konteks tertentu.
Kekurangan Docker:
1. Overhead Sistem
Docker menambah overhead pada sistem, terutama jika dibandingkan dengan menjalankan aplikasi langsung di sistem host. Meskipun lebih ringan dari virtual machine, Docker tetap memerlukan tambahan resource seperti CPU dan memori.
2. Keamanan
Kontainer berbagi kernel dengan host, sehingga potensi eksploitasi keamanan lebih tinggi dibandingkan VM tradisional yang memiliki isolasi penuh pada level hypervisor. Jika ada bug pada kernel host, hal ini dapat berdampak pada seluruh kontainer yang berjalan di atasnya.
3. Manajemen Storage
Manajemen storage di Docker bisa menjadi kompleks, terutama untuk data yang bersifat persisten. Mengelola volume dan binding mount terkadang memerlukan konfigurasi tambahan dan tidak selalu mudah untuk diimplementasikan.
4. Kompleksitas Jaringan
Konfigurasi jaringan antar kontainer dapat menjadi rumit, terutama ketika harus berkomunikasi lintas host. Penggunaan overlay networks atau konfigurasi Docker Swarm bisa menambah kompleksitas pengelolaan.
