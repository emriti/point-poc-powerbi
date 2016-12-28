# Point PoC Power BI for .NET

Accessing PowerBI using application and implement filter capabilities for single report and hide the filter in the iframe.

Step :
1. Register login power bi ke dev.powerbi.com/apps. \n
	- Register sebagai Server-Side Web App. \n
	- Pastikan redirect dan homepage url sudah sesuai (aplikasi hosting di localhost / azure web app)\n
	- Catat client id dan secret\n
2. Lihat ke Azure AD, pastikan aplikasi sudah terdaftar pada azure ad -> lihat tab "App registrations"\n
3. Konfigurasi aplikasi\n
	- Sesuaikan client id dan client secret dengan aplikasi\n
	- Sesuaikan redirect uri (aplikasi hosting di localhost / azure web app)\n
4. pada url embedReport terdapat query string : "&filterPaneEnabled=false" ini berfungsi untuk meng-hide panel filter pada powerbi di iframe\n
5. pada post message terdapat variabel : oDataFilter: "qGetAllCities/stateprovincecode eq '" + txbCode + "'" ini berfungsi utk melakukan filter based on [NamaDataSet]/[NamaKolom] 'eq' textbox kode\n
6. accessToken adalah jwt yang dihasilkan oleh oauth, yang akan dipakai utk melakukan aktifitas ke server powerbi\n
7. Report pada powerbi dibuat dengan datasource yang terbentuk dari Store Procedure\n
\n
disclaimer : filter hanyalah sebatas filter report, belum pada tingkatan datasource, jd masih bisa ditingkatkan dari sisi performa dengan riset yang lebih mendalam.
\n
\n
# Saran implementasi pada point :\n
1. login point dg database point (terpisah dari powerbi)\n
2. perlu dibuat API service power bi utk dapetin access token dan list report yg boleh d akses. Juga identitas merchant (contoh:AL)\n
3. client akan melakukan kompilasi token, embedurl dan id merchant\n
4. untuk sisi security : login dan password power bi di lakukan di sisi services. Identitas merchant pakai GUID\n
5. user aplikasi (point@ecomindo.com) yang didaftarkan di AD, jd nggak perlu d buat user sebanyak merchant d AD.\n
6. didatabase point, nanti d daftarkan juga sejenis report role. utk mapping report yg boleh d akses oleh merchant tertentu.\n
