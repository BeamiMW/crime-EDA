# Latar Belakang
- Berdasarkan [washingtonpost](https://www.washingtonpost.com/outlook/we-dont-know-why-violent-crime-is-up-but-we-know-theres-more-than-one-cause/2021/07/09/467dd25c-df9a-11eb-ae31-6b7c5c34f0d6_story.html), tingkat pembunuhan di AS meningkat, meskipun lambat dan tanpa banyak perhatian media, sebelum pandemi. Dari tahun 2014 hingga 2019, angka tersebut meningkat sebesar 13 persen. Maka akan dilakukan analisis berdasarkan data historikal, yang berupa dokumentasi laporan insiden kriminal yang disediakan oleh Boston Police Department yang terjadi di tahun 2015-2018. Dengan adanya analisis data historikal ini diharapkan dapat memberikan insight yang nantinya dapat dijadikan rekomendasi untuk Boston Police Department dalam menentukan perlengkapan dan tindakan dalam patroli, yang harapannya dapat menurunkan angka kriminalitas di Boston, serta juga dapat meningkatkan keamanan berdasarkan banyaknya jenis pelanggaran kejahatan di Boston.

# Tujuan:
- Meningkatkan keamanan di Boston berdasarkan banyaknya jenis pelanggaran
- Menentukan perlengkapan dan tindakan yang dapat diambil dan dipersiapkan oleh Boston Police Departement berdasarkan banyaknya jenis pelanggaran sehingga bisa menurunkan angka kriminalitas di Boston

# Rumusan Masalah:
- Insiden kriminal apa yang paling sering terjadi? dan sering terjadinya di district mana?
- Apa saja jenis insiden kriminal yang paling sering terjadi berdasakan UCR Part?
- Berapa persen perbandingan antara kasus insiden kriminal dengan adanya penembakan dan tidak ada penembakan?
- Bagaimana perubahan trend kriminalitas dari waktu ke waktu?

# Exploring Data
- Importing libraries & dataset diberi nama variabel df
- Cek jumlah total baris dan kolom
- Cek tipe-tipe data, baris yang terisi, dan memory usage menggunakan df.info()
- Cek 5 data teratas dengan df.head()
- Cek 5 data terbawah dengan df.tail()
- Menjelaskan informasi kolom dari dataset crime
- Mengecek format penulisan dari tiap kolom
- Menampilkan df.describe() semua kolom
- Melihat tanggal awal dan akhir dokumentasi pelaporan ini berdasarkan unique value datenya

# Cleaning Data
- Cek dan hapus data duplikat
- Cek jumlah unique value dari incident number
- Cek dan hapus data duplikat dari unique value Incident number
- Mengganti blank value/value kosong agar dianggap sebagai missing value
- Cek jumlah missing value dari tiap kolom
- Melihat persentase missing value dari dataframe df
- Menampilkan kolom yang ada missing valuenya
- Menemukan pola pada kolom 'area' ternyata banyak yang blank value. Padahal sudah di replace menjadi missing value untuk blank valuenya pada tahapan awal cleaning data.     Kolom Area sendiri berisikan penjelasan tentang area pelaporan, darimana insiden kriminal itu dilaporkan, bukan dimana insiden kiriminal itu terjadi. karena kolom Area,     tidak terlalu berpengaruh banyak pada data pengamatan, maka saya akan mendrop kolom Area.

# Missing value pada kolom shooting
- Melihat unique value pada kolom Shooting
- kolom Shooting menjelaskan mengenai adanya penembakan yang terjadi.
- kasus adanya penembakan yang hanya dilaporkan, dituliskan Y, dan kasus kriminal yang tidak ada penembakan dibiarkan sebagai missing value. 
- maka untuk missing value pada kolom Shooting, diisi dengan N yang artinya tidak ada penembakan.
- Mengganti missing value pada kolom Shooting dengan 'N'
- Cek ulang jumlah missing value pada kolom Shooting setelah di isi

# Missing value pada kolom UCR Part
- Melihat unique value dari kolom UCR Part
- UCR Part adalah kolom berisikan grup Pelaporan Kejahatan Universal (1,2,3) berdasarkan kolom [Group] 
- UCR (Uniform Crime Report) adalah laporan tahunan yang dikeluarkan oleh FBI yang menyajikan data tentang kategori kejahatan tertentu yang dilaporkan ke polisi.
- [penjelasan mengenai UCR PART](https://www.cityofroseville.com/DocumentCenter/View/26568/Description-of-Uniform-Crime-Offenses)
- Cek format penulisan berdasarkan unique value dari kolom Group
- Setelah di cek ternyata pada kolom Group ada beberapa format penulisan yang berbeda namun maksud sama, seperti:
  - 'Investigate Person' dan 'INVESTIGATE PERSON' maka saya akan ubah format penulisannya menjadi 'Investigate Person'
  - 'HUMAN TRAFFICKING' yang termasuk UCR part one dibagi menjadi 2 yaitu 'Human Trafficking - Commercial Sex Acts' dan 'Human Trafficking - Involuntary Servitude',
     - maka untuk 'HUMAN TRAFFICKING' akan saya ubah menjadi 'Human Trafficking - Commercial Sex Acts',
     - dan untuk 'HUMAN TRAFFICKING - INVOLUNTARY SERVITUDE' akan saya ubah format penulisannya menjadi 'Human Trafficking - Involuntary Servitude'
  - Penulisan 'HOME INVASION' menggunakan capital semua maka akan saya ubah menjadi 'Home Invasion'
- Cek format penulisannya lagi setelah diubah berdasarkan unique value dari kolom Group
- Menampilkan semua baris yang missing value pada kolom UCR Part
- Untuk mengisi missing value pada kolom UCR Part, dapat dilihat berdasarkan kolom Group. Kolom Group sendiri berisikan grup-grup pelanggaran dari [UCR_PART]
- Setelah di cek, missing value pada kolom UCR Part adalah yang memiliki Group pelanggaran berupa: Investigate Person, Home Invasion, dan Human Trafficking.
   - pada Group pelanggaran Investigate Person, terdapat data yang tidak missing value UCR Partnya (disitu terdata bahwa Group pelanggaran Investigate Person sebagai UCR Part Three), maka saya isi missing value pada Kolom UCR Part dengan Group pelanggaran Investigate Person dengan UCR Part Three.
   - Home Invasion menurut [wikipedia.org](wikipedia.org), also called a hot prowl burglary, is a sub-type of burglary (or in some jurisdictions, a separately defined crime) in which an offender unlawfully enters into a building residence while the occupants are inside (merupakan Group pelanggaran burglary). Burglary, menurut [UCR PART](https://www.cityofroseville.com/DocumentCenter/View/26568/Description-of-Uniform-Crime-Offenses) , dikelompokkan menjadi UCR Part One. Maka saya isi missing value pada kolom UCR Part dengan Group pelanggaran Home Invasion dengan UCR Part one
   - 'Human Trafficking - Commercial Sex Acts' dan 'Human Trafficking - Involuntary Servitude', menurut [UCR PART](https://www.cityofroseville.com/DocumentCenter/View/26568/Description-of-Uniform-Crime-Offenses) , dikelompokkan menjadi UCR Part One. Maka saya isi missing value pada kolom UCR Part dengan Group pelanggaran Home Invasion dengan UCR Part one
- Cek ulang jumlah missing value pada kolom UCR Part setelah di isi

# Missing value pada kolom District
- [penjelasan dari kolom District](https://bpdnews.com/districts)
- kolom District: berisikan daerah terjadinya insiden kriminal
- Cek unique value kolom district
- Menampilkan semua baris yang missing value pada kolom district
- Melihat persentase missing value dari kolom district = kurang dari 10%
- Kolom District akan saya isi dengan ^ dan tidak akan saya drop karena data yang lainnya masih berguna.
- kolom district sebagai data kategorikal bisa saja diisi dengan modus, namun tidak saya lakukan karena seakan banyaknya terjadi kriminal di district tersebut

# Missing value pada kolom street
- Melihat persentase missing value dari kolom street = kurang dari 10%
- Kolom Street akan saya isi dengan ^ dan tidak akan saya drop karena data yang lainnya masih berguna.
- kolom Street sebagai data kategorikal bisa saja diisi dengan modus, namun tidak saya lakukan karena seakan banyaknya terjadi kriminal di Street tersebut

# Missing value pada kolom latitude
- Melihat persentase missing value dari kolom latitude = kurang dari 10%
- Kolom Latitude akan saya isi dengan -1 dan tidak akan saya drop karena data yang lainnya masih berguna.

# Missing value pada kolom longitude
- Melihat persentase missing value dari kolom longitude = kurang dari 10%
- Kolom longitude akan saya isi dengan -1 dan tidak akan saya drop karena data yang lainnya masih berguna.

# Cek data duplikat dan drop ulang

# ANALISIS DATA BERDASARKAN RUMUSAN MASALAH

# Insiden kriminal apa yang paling sering terjadi? dan sering terjadinya di district mana?
# Insight
- Berdasarkan top ten of offense group, offense group yang berada di urutan pertama adalah 'Motor Vehicle Accident Response' yaitu berjumlah sekita 39.000. Motor Vehicle Accident Response termasuk ke dalam UCR Part III, yaitu termasuk ke dalam kategori insiden kriminal traffic violations. Sedangkan di urutan ke sepuluh, yaitu ada pada group pelanggaran 'Towed' yang termasuk ke dalam UCR Part III, yaitu berjumlah sekitar 11.000. Towed termasuk ke dalam kategori insiden kriminal traffic violations juga, yaitu pelanggaran dengan parkir kendaraan bermotor di tempat-tempat terlarang, sehingga kepolisian mengambil tindakan penderekan kendaraan tersebut. 
- Offense group dari 'motor vehicle accident response' yang berjumlah paling banyak diantara grup pelanggaran lainnya ini sering sekali terjadi di district B2 pada waktu malam hari yaitu di sekitar jam 20.00-04.59
# Rekomendasi
- Diharapkan kepolisian meningkatkan patroli di district B2 yang merupakan district rawan kriminalitas traffic violations dari group pelanggaran 'motor vehicle accident response', di waktu malam hari pada sekitar jam 20.00-04.59
- Diharapkan kepolisian memasang cctv untuk memantau laju lalu lintas di titik rawan kriminalitas traffic violations ini
- Di Kota Boston sendiri sudah menggunakan teknologi untuk membayangkan kembali jalanannya. Di jalan cerdas, kami menggunakan teknologi — seperti kamera dan sensor — untuk mempelajari lebih lanjut tentang cara orang menavigasi dan berinteraksi di jalan-jalan Kota. Pekerjaan terbaru kami berfokus pada keselamatan jalan raya (https://www.boston.gov/innovation-and-technology/smart-streets). Namun untuk kamera tilang elektornik seperti red light and speed camera, masih ilegal di boston (https://ww2.motorists.org/do-we-have-red-light-cameras-in-massachusetts/). Diharapkan tilang elektronik ini bisa menjadi pertimbangan dari kepolisian untuk diajukan menjadi legal kepada pemerintahan

# Apa saja jenis insiden kriminal yang paling sering terjadi berdasakan UCR Part?
# Insight
- Berdasarkan UCR part, insiden kriminal berdasarkan part one paling sering terjadi di District D4
  - UCR Part one meliputi offense group kejahatan berat, seperti Criminal Homicide - The killing of another person (Murder and Nonnegligent Manslaughter & Manslaughter), Rape, Robbery (Armed Robbery-Any Weapon & Strong Arm-No Weapon), Aggravated Assault (Gun, Knife or Cutting Instrument, Other Dangerous Weapons, Hands, Fists, Feet, etc. Aggravated), Burglary (Forcible Entry, Unlawful Entry-No Force, Attempted Forcible Entry), Larceny , Motor Vehicle Theft , Arson, Human Trafficking - Commercial Sex Acts, Human Trafficking - Involuntary Servitude.
  - Insiden kriminal berdasarkan UCR part one yang paling banyak terjadi meliputi pemberian tindakan medis untuk individu yang terluka dari sebuah insiden kriminal sebesar 11.85%, kegiatan investigasi terhadap individu sebesar 11.83%, perbuatan merusak harta benda dan kabur dengan kendaraan bermotor sebesar 10.30%, adu mulut sebesar 8.26%, tilang terhadap kendaraan bermotor sebesar 7.12% dan kegiatan investigasi terhadap harta benda sebesar 7.02%

- sedangkan untuk insiden kriminal part two dan part three paling sering terjadi di district B2
   - Part two meliputi kejahatan ringan, seperti Other Assaults, Forgery and Counterfeiting , Fraud, Embezzlement, Stolen Property, Vandalism, Weapons, Prostitution and Commercialized Vice , Sex Offenses , Drug Abuse Violation, Gambling , Offenses Against Family and Children, Driving Under the Influence , Liquor Laws, Disorderly Conduct, Vagrancy , All Other Offenses (All violations of state or local laws not specifically identified as Part I or Part II offenses,except traffic violations. This classification includes: • Admitting minors to improper places • Bigamy and polygamy • Blackmail and extortion • Contempt of court • Kidnapping • Possession of drug paraphernalia • Riot and rout, etc. • Attempts to commit any of the above), Curfew and Loitering Law Violation (Juvenile), Runaways (Juvenile)
   - part three sering terjadi di district B2

- Insiden kriminal yang paling banyak dilaporkan adalah UCR Part three seperti pemberian tindakan medis untuk individu yang terluka dari sebuah insiden kriminal sebesar 11.85%, kegiatan investigasi terhadap individu sebesar 11.83%, perbuatan merusak harta benda dan kabur dengan kendaraan bermotor sebesar 10.30%, adu mulut sebesar 8.26%, tilang terhadap kendaraan bermotor sebesar 7.12% dan kegiatan investigasi terhadap harta benda sebesar 7.02%. 
- Insiden kriminal berdasarkan UCR Part two yang paling banyak terjadi meliputi vandalisme (perbuatan merusak hasil karya seni / barang berharga) dan ancaman serta serangan dengan proporsi masing masing sedikit diatas 15%. Selanjutnya, ada ancaman secara fisik sebesar 9.27%, penipuan (4.11%)

# Rekomendasi
- Diharapkan kepolisian meningkatkan patroli keliling di setiap district dengan menyiapkan perlengkapan patroli sesuai dengan insiden kriminalitas yang sering terjadi
- Diharapkan kepolisian memasang cctv di titik rawan kriminalitas di titik-titik sesuai peta tersebut

# Berapa persen perbandingan antara kasus insiden kriminal dengan adanya penembakan dan tidak ada penembakan?
# Insight
- Kolom shooting terdiri dari value 'Y' yang menyatakan insiden kriminal yang dicatat disertai terjadinya penembakan, persentasenya sebesar 99.68%
- sedangkan yang diberikan value 'N' yaitu sebagai tidak disertai penembakan berpresentase 0.32%

# Rekomendasi
- Diharapkan kepolisian melakukan upaya tambahan sesuai konstitusi negara Amerika Serikat maupun negara bagian Massachusetts tanpa campur tangan senjata api sehingga membuat masyarakat nyaman

# Bagaimana perubahan trend kriminalitas dari waktu ke waktu?
- Berdasarkan data klinis yang dikumpulkan oleh National Confidential Inquiry into Suicide and Safety in Mental Health (NCISH), Pelanggaran/tindak kriminal lebih mungkin terjadi pada akhir pekan, sebagian besar pada hari Sabtu, berdasarkan [Do homicide rates increase during weekends and national holidays?](https://www.researchgate.net/publication/332279464_Do_homicide_rates_increase_during_weekends_and_national_holidays)
- Untuk itu saya akan mencoba uji hipotesis dengan one sample z-test:
  - Hipotesis:
  - H0 : persentase tindakan kriminal yang terjadi pada weekend = 0.28 (2/7 (jumlah weekend/jumlah hari))
  - Ha : persentase tindakan kriminal yang terjadi pada weekend != 0.28 (2/7 (jumlah weekend/jumlah hari))
  - pvalue =1.444206728150146e-63, pvalue < 0.05, berhasil menolak Ho')
    kita punya cukup bukti untuk mengatakan bahwa tindakan kriminal yang terjadi pada weekend tidak sama dengan 0.05
    (proporsi berbeda signifikan)
# Insight:
- Persentase tindakan kriminal yang terjadi pada akhir pekan tidak lebih banyak dibandingkan hari kerja, dibuktikan dengan Uji Hipotesis dan Pie Chart yang ditampilkan diatas. Hal ini juga dipengaruhi faktor bahwa akhir pekan hanya berjumlah 2 hari yaitu hari sabtu dan hari minggu, sedangkan terdapat 5 hari dalam hari kerja.
- jumlah insiden kriminal yang terjadi di hari sabtu dan hari minggu berjumlah sekitar 40.000-43.000, lebih rendah dibandingkan weekday yaitu sekitar 46.000 - 49.000 kasus
- Di hari senin jumlahnya lebih sedikit dibandingkan hari lainnya.
- Rata-rata terjadi 39-42 kasus per hari saat weekday dan 34-38 kasus per hari saat weekend
- Tingkat kriminalitas di Amerika Serikat diperingkatkan berdasarkan jumlah kasus per 100.000 orang, dengan jumlah kasus di kota Boston yang berada di rentang sekitar 40 kasus per hari, ini berarti dalam satu tahun kira-kira terjadi 14.600 kasus kriminal (365 hari x 40 kasus per hari). Jumlah kasus tersebut dibagi dengan populasi kota Boston yaitu 675,647 orang sesuai data United States census records and Population Estimates Program data. Ini berarti bahwa tingkat kriminalitas per 100.000 orang di kota Boston ada di angka 2.161 (populasi dikali dengan 100.000/populasi), mendekati angka yang dilansir FBI pada tahun 2011 dengan total 2.484 kasus FBI. Jika dibandingkan dengan 9 kota metropolitan terbesar lainnya di Amerika Serikat, kota Boston termasuk dalam peringkat 9 dengan tingkat kriminalitas tertinggi

# Rekomendasi:
- Tidak ada perbedaan signifikan antara tingkat kriminalitas per harinya, sehingga diharapkan untuk kepolisian Boston Police Department membuat program yang direncanakan yang sama untuk di setiap harinya, tanpa perlu adanya patroli khusus di hari-hari tertentu.
- Dibandingkan kota-kota metropolitan terbesar lainnya di Amerika Serikat, kota Boston hanya menempati peringkat 9 dari 10 kota dengan tingkat kriminalitas tertinggi per 100.000 orang. Namun, angka kriminalitas di Boston ini bisa dibilang tidak terlalu fluktuatif, namun tanpa bisa ditekan agar berkurang, maka dari itu kepolisian Boston Police Department tidak boleh cepat berpuas diri, namun tetap melakukan patroli maupun tindakan preventif agar di kemudian hari, angka kriminalitas bisa diturunkan. Proggresnya sudah mulai terlihat yaitu turunnya tingkat kriminalitas di Boston sampai 23% untuk hampir semua kategori kriminal pada tahun 2021 (Boston Herald,2021).

# Kesimpulan
- Selama periode 15 Juni 2015-3 September 2018, angka kriminalitas di kota Boston cenderung stabil. Hal tersebut dapat dilihat dari tindakan kepolisian dalam menerima laporan insiden kriminal dari masyarakat yang melapor. 
- Namun hal tersebut bisa juga karena upaya yang diterapkan oleh Boston Police Department belum efektif untuk menekan turunnya angka kriminalitas di kota Boston. Maka dari itu, direkomendasikan untuk melakukan upaya tambahan sesuai konstitusi negara Amerika Serikat maupun negara bagian Massachusetts tanpa campur tangan senjata api sehingga membuat masyarakat nyaman dengan tindakan polisi yang sebelumnya cenderung terlihat represif terhadap pelaku kejahatan yang dapat terlihat dari kolom Shooting yaitu sebesar 99.68% adanya insiden penembakan.
- Sistem pencatatan bedasarkan incident number diharapkan lebih rapi lagi. 1 Incident number diharapkan dapat mewakili satu pelaporan dengan offense group yang berbeda.
- District B2 merupakan district dengan tingkat aktivitas polisi paling banyak incident pelaporan kriminalitas dibandingkan 11 district lainnya di kota Boston. Maka diharapkan kepolisan Boston harus mengerahkan lebih banyak jumlah polisi untuk patroli dan berjaga di district tersebut
- District A15 menjadi district dengan tingkat aktivitas tindakan kepolisian Boston terendah di kota Boston.
- Tindakan kepolisian yang paling banyak dilakukan selama periode waktu 15 Juni 2015-3 September 2018 adalah bantuan medis kepada individu di tempat kejadian perkara, dilanjutkan oleh tindakan investigasi baik kepada individu maupun harta benda. Diharapkan polisi memiliki skill pemberian pertolongan pertama yang dapat dilakukan di TKP sambil menunggu petugas medis. Dan juga menambah staff dari divisi investigasi lihat banyak sekali kasus yang membutuhkan tindakan investigate person
- Diharapkan kepolisian Boston dapat mengadakan program pelatihan pertolongan pertama seperti DRSABC, yaitu kepanjangan dari Danger, Response, Shout, Airway, Breathing, Circulation. 

