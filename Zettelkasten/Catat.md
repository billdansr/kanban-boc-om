- 8 September
	- Safety Induction
	- Proses ID Card
	- Pengenalan awal pembimbing dan pembiasaan di lingkungan
- 9 September
	- Mendapat tugas membuat Visitor Management System
- 10 September
	- Cancel tugas lama
	- Mendapat tugas baru membuat BOC OM (Basic Operational Care)
	- Mendesain Use Case dan alur sistem BOC OM
	- Mempelajari Konsep dasar ASP.NET Core Web App (Model-View-Controller)
- 11 September
	- Lanjut belajar
		- CRUD perlu context.
		- Jika Action Controller fetch dari DB, gunakan async/await dan Task.
- 12 September
	- Belajar bahwa pengembangan itu mengikuti flow dari user, mulai dari tampilan baru ke data.
- 13 September
	- Belajar ASP.NET Core Web App (Model-View-Controller).
- 14 September
	- Belajar ASP.NET Core Identity.
- 15 September
	- SeedData
	- Mulai Frontend
	- Jadi tampilan Home Page
- 16 September
	- Lanjut frontend
	- Bikin breadcrumbs
- 17 September
	- Lanjut frontend
	- Bikin UI multi step form
	- Animasi card hover
	- Refactor code
	- Bantu catat stok tinta cartridge
	- Bantu angkat barang
- 18 September
	- Membuat halaman admin
	- Merapihkan navbar
	- Membuat sidebar untuk admin
- 19 September
	- Melanjutkan pengembangan fitur manage user admin
	- Bikin tabel daftar user
- 22 September
	- Mempertimbangkan implementasi table menggunakan MVC-only atau DataTables
	- Setup DataTables untuk users
- 23 September
	- Buat Migration untuk tambah kolom Name, NIP, Job, dan SignaturePath ke tabel AspNetUsers
	- Berhasil Create User menggunakan form modal
	- Implementasi Delete User
	- Mempertimbangkan Ajax atau pure MVC untuk CRUD
		- \_userForm mungkin gajadi
		- ManageUsersViewModel mungkin gajadi
- 24 September
	- Memindahkan barang megaphone dan speaker ke ruang lain
	- Berhasil implementasi create user form
	- Membuat Area Admin
	- Memilih arsitektur MVC murni dan tidak memakai AJAX
- 25 September
	- Belajar \_ViewImports dan \_ViewStart
	- Selesai implementasi Edit dan Delete User (Manage User)
- 26 September
	- Hitung stok catridge
	- Analisis alur proses BOC OM
	- Desain Class Diagram
	- Memilih Code-First Approach
- 28 September
	- Mempelajari bahwa desain Model di MVC harus memperhatikan multiplicity dan relationship (apakah suatu class bisa di-instantiate tanpa class lain atau ketergantungan?)
	- Desain dan Implementasi Models
	- Konfigurasi DbContext
	- Migration dengan skema terbaru
- 29 September
	- SeedData untuk Core Application Data
	- Update schema database dan add migration
	- Membuat form untuk generate form
	- Mulai mengerjakan use case submit report
	- Ubah schema agar tidak redundan
	- Membuat form report submission untuk generate form
- 30 September
	- Membuat CRUD untuk AreaOfWork, EquipmentCategory, dan FunctionalLocation
	- Ditemukan masalah ketika mencoba mengimplementasikan Report Submission, tidak jelas antara data master dan data transaksi sehingga dilakukan desin database ulang.
- 1 Oktober
	- Implementasi desain class diagram ke Models dan migrate 
- 2 Oktober
	- Bantu turunin barang untuk keperluan printing dari rak atas gudang
	- Refactor data model untuk meningkatkan maintainability
	- Bantu angkat barang dari lantai bawah ke atas

```mermaid
stateDiagram-v2
    state "General Manager" as ceo
    state "Yulianti Triwibowo" as ceo
    ceo --> devmngr
    ceo --> admmngr
    ceo --> law

    state "Dev. Manager" as devmngr
    state "Alice" as devmngr
    devmngr --> dev

    state "Development Team" as dev
    state "Bob" as dev
    state "Charles" as dev
    state "David" as dev
    state "Eveline" as dev

    state "Adm. Manager" as admmngr
    state "Florence" as admmngr
    admmngr --> adm

    state "Administration Team" as adm
    state "Grace" as adm
    state "Holt" as adm
    state "Ivan" as adm

    state "Lawyer" as law
    state "John" as law
```

```mermaid
graph TD
    A[Senior Vice President Refining Operation] --> B[General Manager RU VI]
    B --> C[Secretary]
    B --> D[Senior Manager Operation & Manufacturing]
    D --> E[Production I Manager]
    D --> F[Production II Manager]
    D --> G[Refinery Planning & Optimization Manager]
    D --> H[Maintenance Execution Manager]
    D --> I[Maintenance Planning & Support Manager]
    D --> J[Engineering Manager]
    D --> K[HSE Manager]
    D --> L[Finance Manager]
    D --> M[Procurement Manager]
    D --> N[IT Manager]
    D --> O[Reliability Manager]
    D --> P[Legal Counsel/Compliance]
    
    E --> E1[RCC]
    E --> E2[HSC]
    E --> E3[DHC]
    
    F --> F1[OM]
    F --> F2[Utilities]
    F --> F3[Laboratory]
    F --> F4[POC]
```
