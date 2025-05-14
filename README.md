# install Teaspeak Server
```
apt-get update
apt-get upgrade
apt-get install curl
apt-get install ffmpeg
apt-get install youtube-dl
apt-get install screen
apt-get install libnice10 -y
```
For your own security, do not run TeaSpeak or any other closed source program on your root account,
Create another user for it.
Create a new user called TeaSpeak, for example:

```
adduser --disabled-login teaspeak
```
# Masuk ke pengguna yang baru dibuat:
```
cd /home/teaspeak/; su teaspeak
```
# 64bit Download versi terbaru dengan tautan di bawah ini:
```
https://repo.teaspeak.de/server/linux/amd64_$teaspeak_channel/TeaSpeak-$teaspeak_version.tar.gz
```
# 32bit Download versi terbaru dengan tautan di bawah ini:
```
https://repo.teaspeak.de/server/linux/amd32_$teaspeak_channel/TeaSpeak-$teaspeak_version.tar.gz
```
# Ekstrak file “.tar.gz” dan hapus:
```
tar -xzf TeaSpeak.tar.gz
rm TeaSpeak.tar.gz
```
# Mulai server menggunakan sesi layar sehingga tetap berjalan di latar belakang dan tidak mati sendiri saat Anda meninggalkan sesi SSH:
# layar -AmdS TeaSpeak-Server
# layar -x
```
./teastart_minimal.sh
```
Simpan token dan data login kueri Anda ke Wordpad atau tempat lain yang memungkinkan Anda mendapatkannya kembali kapan saja. Tutup sesi lagi dengan CTRL+C
```
./teastart.sh start
```
# Hentikan dengan menggunakan:
```
./teastart.sh stop
```
# Teaspeak mulai otomatis
```
cd /home
```
```
nano tsanticrash.sh
```
```
#!/bin/bash
case $1 in
teaspeakserver)
teaspeakserverpid=`ps ax | grep TeaSpeakServer | grep -v grep | wc -l`
if [ $teaspeakserverpid -eq 1 ]
then exit
else cd /home/teaspeak/
./teastart.sh start
fi
;;
esac
```
Catatan Penting : ubah “/home/teaspeak/” ke folder instalasi yang tepat lalu tekan kombinasi kedua tombol ini pada keyboard Anda (CTRL+X) lalu Tekan ketik y dan kemudian tekan ENTER untuk menyimpan dan keluar
```
chmod 777 tsanticrash.sh
```
```
crontab -e
```
```
*/1 * * * * /home/tsanticrash.sh teaspeakserver
```
lalu lagi (CTRL+X) lalu Tekan ketik y lalu tekan ENTER untuk menyimpan dan keluar
# Memperbarui Server Teaspeak
```
zip -r teaspeak-backup-$(date +"%m-%d-%y-%r").zip *
teaspeak_channel="stable" && \
teaspeak_version=$(curl -k https://repo.teaspeak.de/server/linux/amd64_$teaspeak_channel/latest) && \
wget https://repo.teaspeak.de/server/linux/amd64_$teaspeak_channel/TeaSpeak-$teaspeak_version.tar.gz && \
tar xvf TeaSpeak-$teaspeak_version.tar.gz && \
rm TeaSpeak-$teaspeak_version.tar.gz
```
```
./teastart.sh start
```
# Selesai, server Anda telah berjalan pada port 9987!
# Selamat Bersenang-Senang
