## Reflection On Hello Minikube

1. Saat saya memeriksa log sebelum dan setelah aplikasi diekspos sebagai layanan, saya menemukan perbedaan dalam isi log tersebut. Sebelum aplikasi diekspos, log hanya mencatat bahwa server HTTP dan UDP telah dimulai pada port 8080. Namun, setelah aplikasi diekspos, log menunjukkan berbagai riwayat permintaan HTTP GET. Menurut pengamatan saya, hal ini terjadi karena setiap kali saya membuka aplikasi dan me-refresh halaman web, log mencatat permintaan HTTP GET tambahan. Berikut adalah lampiran dari percobaan tersebut:

![alt text](1.png)
![alt text](2.png)
![alt text](3.png)

2. Dalam perintah kubectl, opsi -n digunakan untuk menentukan namespace tertentu di cluster Kubernetes. Namespace di Kubernetes berfungsi memisahkan objek dalam kluster agar sumber daya lebih terorganisir dan terisolasi. Misalnya, jika Anda menggunakan opsi -n kube-system, perintah kubectl get hanya akan menampilkan objek yang berada di namespace kube-system. Alasan output tidak menunjukkan pods atau layanan secara eksplisit adalah karena sumber daya tersebut kemungkinan besar dibuat di namespace lain.

## Reflection on Rolling Update & Kubernetes Manifest File

1. Strategi rolling update dan recreate deployment memiliki perbedaan utama dalam hal downtime. Pada recreate deployment, terjadi waktu henti antara pembaruan aplikasi karena metode ini mengharuskan penghapusan aplikasi yang lama sebelum menginstal yang baru. Hal ini menyebabkan aplikasi tidak tersedia selama proses pembaruan berlangsung. Sebaliknya, rolling update memperbarui aplikasi secara bertahap, menggantikan instans lama dengan yang baru satu per satu. Dengan cara ini, downtime bisa diminimalisir atau bahkan dihilangkan.

2. Ya, saya berhasil menerapkan strategi deployment Recreate dengan mengikuti tutorial https://dev.to/cloudskills/kubernetes-deployment-strategy-recreate-3kgn, bagian manual recreate deployment. Pertama, saya menjalankan kubectl edit deployments spring-petclinic-rest untuk mengedit versi dari file teks yang muncul. Pada tangkapan layar, terlihat bahwa perintah untuk menghapus pod telah dijalankan. Terlihat bahwa pod-pod lama dihapus terlebih dahulu sebelum pod baru dibuat setelah perintah tersebut. Proses ini menyebabkan downtime singkat, namun pod baru segera menggantikan pod lama sehingga aplikasi kembali berjalan dengan cepat. Selain itu, juga terlihat bahwa service berjalan di localhost, memungkinkan akses melalui URL yang diberikan.

3. File tersebut sudah saya lampirkan pada repository ini dengan nama deploymentrecreate.yaml.

4.  - Mampu menetapkan kondisi yang diinginkan untuk setiap objek Kubernetes dalam kluster.
    - Proses manajemen infrastruktur menjadi lebih efisien dan tahan terhadap kesalahan.
    - Mampu mengelola objek secara deklaratif, yakni dengan mendefinisikan kondisi yang diinginkan sehingga Kubernetes akan mengambil langkah-langkah yang diperlukan untuk mencapainya.
    - Dengan menggunakan file manifest, versi konfigurasi dapat diatur bersama dengan kode dan diterapkan ke kluster secara deklaratif.
    - Memungkinkan pengelolaan pembaruan kolaboratif untuk objek Kubernetes dengan mudah.