# report-modul-6-7

## Rafael Gunawan (5027231019)

## Step Pengerjaan
1. ``Lakukan scanning menggunakan nMap pada machine`` <br>
   ![image](https://github.com/user-attachments/assets/c86b3560-fc21-4025-b68d-aee42020a52d) <br>
   ``Bisa dilihat disini bahwa port 21 disini terbuka dan statusnya "login allowed" yang artinya kita bisa login dari FTP. Dari hasil scan tersebut kita juga bisa melihat bahwa mesin ini juga menyimpan file   
     list.xyz dan readme.txt dalam port 21.``
2.  ``Lalu disini kita coba untuk login langsung melalui FTP``<br>
   ![image](https://github.com/user-attachments/assets/4bb71491-0342-4ca1-873d-0b7247c231f4) <br>
   ``Disini kita diminta untuk memasukan username, nah tapi disini kita belum tau untung usernamenya sendiri tuh apa``
3. ``Kemudian disini kita lakukan brute force menggunakan "hydra -l anonymous -P ~/Downloads/dictionary.txt ftp://10.15.42.245" untuk menemukan kombinasi username & password yg sesuai. Untuk dictionary.txt 
     sendiri saya dapat dari discord yang dikirim oleh mas Valen`` <br>
   ![image](https://github.com/user-attachments/assets/16a81095-4f3d-4a89-be3c-df484b84f436) <br>
4. ``Setelah berhasil masuk dengan salah satu kombinasi tadi, kita ls untuk melihat ada file apa saja yang ada di dalam direktori tersebut. Kemudian kita download dua file tersebut`` <br>
   ![image](https://github.com/user-attachments/assets/a5f927f4-53db-40f5-8a7c-da40b3952597) <br>
   ![image](https://github.com/user-attachments/assets/4ebb727a-3307-4b53-9d64-032809bf8d5a) <br>
   ![image](https://github.com/user-attachments/assets/eeb43e59-fec3-4856-9adc-679decb2b1b5) <br>
   ``Disini bisa dilihat juga kalau file list.xyz berisikan data dari 1000 user yang berisikan id, username, password, dan email dari para penggunanya. Ada juga disini file readme.txt yang berisikan puisi unik.``
5. ``Selanjutnya, kita akan langsung menghashing password-password tersebut. Untuk mempermudah, kita akan memisahkan password dari data yang lain-lainnya menggunakan "grep -o '\$2[abxy]\$[^\"]*' list.xyz > 
   hashfile.txt". Setelah itu kita gunakan command "hashcat -m 3200 -a 0 hashfile.txt ~/Downloads/dictionary.txt" untuk memecahkan hashnya menggunakan Dictionary.txt.`` <br>
   ![image](https://github.com/user-attachments/assets/9cfd5c95-5f55-4795-a3d2-ae1b4bb98626) <br>
   ![image](https://github.com/user-attachments/assets/9ba302d4-71f2-4144-ab07-77bc56d2011c) <br>
6. ``Setelah itu, kita coba login menggunakan username dan password yang tadi sudah kita dapatkan. Disini bisa dilihat bahwa ada file readme.txt lagi dan saat kita buka ada zonk. Disini juga kita mendapatkan 
   beberapa informasi lain seperti file ".basrc, .bash_logout, dan .profile".``
   ![image](https://github.com/user-attachments/assets/5dee227c-b6aa-4b58-aa58-1d3fef5caaec) <br>
   ![image](https://github.com/user-attachments/assets/2cc7ca53-e43e-4c5a-b4af-94701547b878) <br>
   ![image](https://github.com/user-attachments/assets/8fd1c1ae-2f7e-488b-b142-53ba9b71a9be) <br>
   ![image](https://github.com/user-attachments/assets/1e24f232-8e95-4a71-8147-b5f9456b2ab7) <br>
7. ``Sekarang kita balik lagi scan nMap yang awal, dilihat juga bahwa ada port 487 yang terbuka dan ketika kita buka terlihat ada dua post yang kalau kita click lalu inspect bakal keluar pluginnya atu kita bisa gunakan "wpscan --url http://10.15.42.245:487/2024/10/03/trial/ --wp-content-dir wp-content --enumerate p" untuk melihat lebih detail.`` <br>
   ![image](https://github.com/user-attachments/assets/a8bb4af5-4d41-4a81-8b09-f56d65d15df2) <br>
   ![image](https://github.com/user-attachments/assets/269a4dd4-d34d-44b8-bae9-48f00944d642) <br>
   ![image](https://github.com/user-attachments/assets/8e8325c3-f96d-4819-985d-2de65b04296a) <br>
   ``Nah disini kita bisa tau bahwa plugin yang ada pada url tersebut adalah wpdiscuz``
8. ``Setelah tau plugin dari url tersebut, kita bisa mengeksploitasi mesin tersebut menggunakan metasploit framework`` <br>
   ![image](https://github.com/user-attachments/assets/5146c76c-a9de-4259-bc3c-82d011f7d54c) <br>
   ![image](https://github.com/user-attachments/assets/683d677c-b916-45b7-bff8-e9d88fa49fc4) <br>
   ``Disini kita setting LHOST dari ip vpn kita, RHOST 10.15.42.245, RPORT 487, set BLOGPATH /2024/10/03/trial/ (post yg berisi puisi), dan set TARGETURI / (merujuk langsung ke wordpress).``
9. ``Sesudah berhasil masuk, kita bisa melihat berbagai informasi yang ada disini. Misalnya, kita bisa melihat info dari sistem tersebut, kemudian kita juga bisa melihat path ke password tiap user yang ada. 
   Terakhir, kita pun juga bisa melihat dan mengedit file-file yang berada dalam direktori tersebut`` <br>
   ![image](https://github.com/user-attachments/assets/1881b5e9-aa0b-4370-9e7f-d88fde7c63d0)
