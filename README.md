# Python Socket Programing


<h1 align="center">
  <br>
  <a href="http://www.amitmerchant.com/electron-markdownify"><img src="https://static.vecteezy.com/system/resources/previews/014/007/776/non_2x/python-logo-icon-design-illustration-vector.jpg" alt="Markdownify" width="200"></a>
  <br>
  Python Socket Programing
  <br>
</h1>

<h4 align="center">A minimal Markdown Editor desktop app built on top of <a href="http://electron.atom.io" target="_blank">Electron</a>.</h4>

<p align="center">
  <a href="https://badge.fury.io/js/electron-markdownify">
    <img src="https://badge.fury.io/js/electron-markdownify.svg"
         alt="Gitter">
  </a>
  <a href="https://gitter.im/amitmerchant1990/electron-markdownify"><img src="https://badges.gitter.im/amitmerchant1990/electron-markdownify.svg"></a>
  <a href="https://saythanks.io/to/bullredeyes@gmail.com">
      <img src="https://img.shields.io/badge/SayThanks.io-%E2%98%BC-1EAEDB.svg">
  </a>
  <a href="https://www.paypal.me/AmitMerchant">
    <img src="https://img.shields.io/badge/$-donate-ff69b4.svg?maxAge=2592000&amp;style=flat">
  </a>
</p>

<p align="center">
  <a href="#Ders 1">Ders 1</a> •
  <a href="#Ders 2">Ders 2</a> •
  <a href="#Ders 3">Ders 3</a> •
  <a href="#Ders 4">Ders 4</a> •
  <a href="#Ders 5">Ders 5</a> •
  <a href="#Ders 6">Ders 6</a> •
  <a href="#Ders 7">Ders 7</a> •
  <a href="#Ders 8">Ders 8</a> •

</p>

![screenshot](https://raw.githubusercontent.com/amitmerchant1990/electron-markdownify/master/app/img/markdownify.gif)

## Python Socket Programlama:
<p>Socket programlama, ağ üzerinde veri iletişimi için kullanılan bir Python modülüdür. Socket programlama, bilgisayarlar arasında veri iletimi sağlayan bir arayüz sağlar.</p>

## Ders 1
<p>Bu kod, basit bir TCP sunucusunu temsil eder. Sunucu, belirli bir portu dinler ve bir istemcinin bağlanmasını bekler. İstemci bağlandığında, sunucu istemciden komutlar alır, bu komutları sistemde çalıştırır ve ardından komutun çıktısını istemciye geri gönderir.</p>

<h4><u>Kodun genel akışı şu şekildedir:</u></h4> 

* **_<u>socket</u>_** modülü kullanılarak bir TCP sunucu soketi oluşturulur.
* Belirtilen IP adresi ve port numarasına bağlanır ve gelen bağlantıları dinlemeye başlar.
* Bir istemci bağlandığında, bağlantı kabul edilir ve istemci adresi ekrana yazdırılır.
* Sonsuz bir döngü içinde, istemciden gelen komut alınır **_<u>(recv ile)</u>_**, bu komut sistemde çalıştırılır **_<u>(subprocess.run ile)</u>_** ve çıktı istemciye gönderilir **_<u>(conn.send ile).</u>_**
* Eğer komutun çıktısı boşsa, "Komut başarıyla çalıştırıldı" mesajı gönderilir.
* Bağlantı sürekli olarak dinlenir ve işlemler tekrarlanır.
* Sonsuz döngüden çıkıldığında, bağlantı kapatılır **_<u>(conn.close).</u>_**

### Server Programlama
```bash
import socket
import subprocess

# Sunucu IP adresi ve port numarası
host = '127.0.0.1'
port = 4246

# Socket oluştur ve belirtilen IP adresi ve port numarasına bağla
server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server_socket.bind((host, port))
server_socket.listen()

# Bağlantı kabul et
conn, addr = server_socket.accept()
print("Bağlantı yapıldı, Adres: " + str(addr))

# Sonsuz döngü ile bağlantıyı dinle
while True:
    # İstemciden gelen veriyi al
    data = conn.recv(1024).decode()
    print("Alınan veri: " + data)

    # Alınan komutu sistemde çalıştır
    result = subprocess.run(data, stdout=subprocess.PIPE, shell=True)

    # Komutun çıktısını al
    if result.stdout.decode() != "":
        response_data = result.stdout
    else:
        response_data = "Komut başarıyla çalıştırıldı".encode()

    # Çıktıyı istemciye gönder
    conn.send(response_data)

# Sonsuz döngüden çıkıldığında bağlantıyı kapat
conn.close()

```
### Client Programlama

<p>Bu kod, basit bir TCP istemcisini temsil eder. İstemci, belirli bir IP adresi ve port numarasına bağlanır ve kullanıcının girdiği mesajları sunucuya gönderir. Sunucudan gelen cevapları ekrana yazdırır. "quit" komutu girildiğinde, döngüden çıkılır ve bağlantı kapatılır.</p>

<h4><u>Kodun genel akışı şu şekildedir:</u></h4> 

* **_<u>socket</u>_** modülü kullanılarak bir TCP istemci soketi oluşturulur.
* Belirtilen IP adresi ve port numarasına bağlanılır **_<u>(client_socket.connect((host, port))).</u>_**
* Kullanıcıdan sürekli olarak giriş alınır **_<u>(input(">> ")).</u>_**
* Eğer kullanıcı "quit" yazarsa, döngüden çıkılır <u>(_break_)</u>.
* Kullanıcının girdiği mesaj sunucuya gönderilir **_<u>(client_socket.sendall(message.encode())).</u>_**
* Sunucudan gelen cevap alınır **_<u>(data = client_socket.recv(1024).decode()).</u>_**
* Sunucudan gelen veriyi ekrana yazdırır **_<u>(print("Sunucudan gelen yanıt: " + data)).</u>_**
* Döngü sürekli olarak devam eder, kullanıcı "quit" yazana kadar.
* Döngüden çıkıldığında, bağlantı kapatılır **_<u>(client_socket.close()).</u>_**

```bash
import socket

# Sunucu IP adresi ve port numarası
host = '127.0.0.1'
port = 4246

# Socket oluştur ve belirtilen IP adresi ve port numarasına bağlan
client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client_socket.connect((host, port))

# Kullanıcıdan alınan girişle sürekli dönen bir döngü
while True:
    message = input(">> ")  # Kullanıcıdan giriş alınır
    if message.lower().strip() == "quit":
        break  # Kullanıcı "quit" yazarsa döngüden çık

    # Kullanıcının girdiği mesajı sunucuya gönder
    client_socket.sendall(message.encode())  # Güvenilir gönderim için `sendall()` kullanılır

    # Sunucudan gelen cevabı al
    data = client_socket.recv(1024).decode()
    print("Sunucudan gelen yanıt: " + data)  # Sunucudan gelen veriyi ekrana yazdırır

# Döngüden çıkıldığında, bağlantıyı kapat
client_socket.close()


```


## Ders 2

To clone and run this application, you'll need [Git](https://git-scm.com) and [Node.js](https://nodejs.org/en/download/) (which comes with [npm](http://npmjs.com)) installed on your computer. From your command line:

```bash
# Clone this repository
$ git clone https://github.com/amitmerchant1990/electron-markdownify

# Go into the repository
$ cd electron-markdownify

# Install dependencies
$ npm install

# Run the app
$ npm start
```

> **Note**
> If you're using Linux Bash for Windows, [see this guide](https://www.howtogeek.com/261575/how-to-run-graphical-linux-desktop-applications-from-windows-10s-bash-shell/) or use `node` from the command prompt.


## Ders 3

You can [download](https://github.com/amitmerchant1990/electron-markdownify/releases/tag/v1.2.0) the latest installable version of Markdownify for Windows, macOS and Linux.

## Ders 4

Markdownify is an [emailware](https://en.wiktionary.org/wiki/emailware). Meaning, if you liked using this app or it has helped you in any way, I'd like you send me an email at <bullredeyes@gmail.com> about anything you'd want to say about this software. I'd really appreciate it!

## Ders 5

This software uses the following open source packages:

- [Electron](http://electron.atom.io/)
- [Node.js](https://nodejs.org/)
- [Marked - a markdown parser](https://github.com/chjj/marked)
- [showdown](http://showdownjs.github.io/showdown/)
- [CodeMirror](http://codemirror.net/)
- Emojis are taken from [here](https://github.com/arvida/emoji-cheat-sheet.com)
- [highlight.js](https://highlightjs.org/)

## Ders 6

[markdownify-web](https://github.com/amitmerchant1990/markdownify-web) - Web version of Markdownify

## Ders 7

<a href="https://www.buymeacoffee.com/5Zn8Xh3l9" target="_blank"><img src="https://www.buymeacoffee.com/assets/img/custom_images/purple_img.png" alt="Buy Me A Coffee" style="height: 41px !important;width: 174px !important;box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;-webkit-box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;" ></a>

<p>Or</p> 

<a href="https://www.patreon.com/amitmerchant">
	<img src="https://c5.patreon.com/external/logo/become_a_patron_button@2x.png" width="160">
</a>

## Ders 8

- [Pomolectron](https://github.com/amitmerchant1990/pomolectron) - A pomodoro app
- [Correo](https://github.com/amitmerchant1990/correo) - A menubar/taskbar Gmail App for Windows and macOS

## License

MIT

---

> [amitmerchant.com](https://www.amitmerchant.com) &nbsp;&middot;&nbsp;
> GitHub [@amitmerchant1990](https://github.com/amitmerchant1990) &nbsp;&middot;&nbsp;
> Twitter [@amit_merchant](https://twitter.com/amit_merchant)

