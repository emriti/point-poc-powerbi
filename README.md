# Point PoC Power BI for .NET

Accessing PowerBI using application and implement filter capabilities for single report and hide the filter in the iframe.

Step :
1. Register login power bi ke dev.powerbi.com/apps. 
	- Register sebagai Server-Side Web App. 
	- Pastikan redirect dan homepage url sudah sesuai (aplikasi hosting di localhost / azure web app)
	- Catat client id dan secret
2. Lihat ke Azure AD, pastikan aplikasi sudah terdaftar pada azure ad -> lihat tab "App registrations"
3. Konfigurasi aplikasi
	- Sesuaikan client id dan client secret dengan aplikasi
	- Sesuaikan redirect uri (aplikasi hosting di localhost / azure web app)
4. pada url embedReport terdapat query string : "&filterPaneEnabled=false" ini berfungsi untuk meng-hide panel filter pada powerbi di iframe
5. pada post message terdapat variabel : oDataFilter: "qGetAllCities/stateprovincecode eq '" + txbCode + "'" ini berfungsi utk melakukan filter based on [NamaDataSet]/[NamaKolom] 'eq' textbox kode
6. accessToken adalah jwt yang dihasilkan oleh oauth, yang akan dipakai utk melakukan aktifitas ke server powerbi
7. Report pada powerbi dibuat dengan datasource yang terbentuk dari Store Procedure

disclaimer : filter hanyalah sebatas filter report, belum pada tingkatan datasource, jd masih bisa ditingkatkan dari sisi performa dengan riset yang lebih mendalam.


# Saran implementasi pada point :
1. login point dg database point (terpisah dari powerbi)
2. perlu dibuat API service power bi utk dapetin access token dan list report yg boleh d akses. Juga identitas merchant (contoh:AL)
3. client akan melakukan kompilasi token, embedurl dan id merchant
4. untuk sisi security : login dan password power bi di lakukan di sisi services. Identitas merchant pakai GUID
5. user aplikasi (point@ecomindo.com) yang didaftarkan di AD, jd nggak perlu d buat user sebanyak merchant d AD.
6. didatabase point, nanti d daftarkan juga sejenis report role. utk mapping report yg boleh d akses oleh merchant tertentu.
