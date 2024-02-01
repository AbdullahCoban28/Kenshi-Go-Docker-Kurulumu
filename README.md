# Kenshi-Go-Docker-Kurulumu

> [!NOTE]
> Kenshi Artık GOLang ile çalışacağını belirtti. Bu Sebeple Eski Node'unuzdan Public ve Private Keylerinizi Biryere Kaydedip Silebilirsiniz. Tek komutla silme yok malesef, tek tek dosyaları bulup silin.

<br>

## Sunucu Güncelleme ve Docker Kurulumu
```
# Öncelikle sunucudaki güncellemelerimizi ve yükseltmelerimizi yapalım.
sudo apt update -y && sudo apt upgrade -y

# Ardından sunucumuza HTTPS üzerinden indireceğimiz kaynak için sorun çıkmaması adına ve linkten indirdiğimiz zip dosyasını unzip ederken sorun yaşamamak için aşağıda yazan kodları girelim.
sudo apt install apt-transport-https ca-certificates curl software-properties-common wget unzip

# Docker GPG anahtarını sunucumuza ekleyelim
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Docker'ı kaynaklarımıza ekleyelim 
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Eklediğimiz kaynağın tanınması için yeniden güncelleyelim
sudo apt update

# Ubuntu yerin Docker üzerinden kurulum yapacağımızı garanti altına alalım
apt-cache policy docker-ce

```
> [!WARNING]
> En son yazmış olduğumuz kod bize bir ekran çıktısı verecektir. Buradaki çıktıda Installed: (none) olmasına dikkat edelim.
```
docker-ce:
  Installed: (none)
  ...
  ...
  5:20.10.14~3-0~ubuntu-focal 500
  500 https://download.docker.com/linux/ubuntu jammy/stable amd64 Packages
  5:20.10.13~3-0~ubuntu-focal 500
  500 https://download.docker.com/linux/ubuntu jammy/stable amd64 Packages
  ...
  ...

## Ve ardından Docker'ı yükleyelim
sudo apt install docker-ce

## Docker'ın kurulduğundan emin olmak için aşağıdaki kodu çalıştıralım.
sudo systemctl status docker
```
> [!WARNING]
> En son yazmış olduğumuz kod bize aşağıdaki gibi bir çıktı vermelidir.

```
Output
● docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
     ...
     ...
     ...
```
<br>

## Kenshi Unchained Go Versiyon Kurulumu

```
# wget ile dosyamızı indirelim
wget https://github.com/KenshiTech/unchained/releases/download/v0.11.0-alpha.5/unchained-v0.11.0-alpha.5-docker.zip

# İndirmiş olduğumuz dosyamızı unzipleyelim
unzip  unchained-v0.11.0-alpha.5-docker.zip

# Unzip ile ortaya çıkan dosyamızın içine girelim
cd unchained-v0.11.0-alpha.5-docker

# cp komutu ile dosya içerisinde bulunan conf.worker.yaml.template isimli dosyamızı conf.worker.yaml olarak kopyalayalım.
cp conf.worker.yaml.template conf.worker.yaml

# Oluşturduğumuz dosyanın içerisine girelim
cp conf.worker.yaml

# Aşağıdaki komut ile kopyaladığımız dosya içeriğini düzenleyelim. 
nano conf.worker.yaml

# ADINIZ YAZAN KISMI DEĞİŞTİRİN
● broker: wss://shinobi.brokers.kenshi.io
  log: info
  name: ADINIZ
  rpc:
    ethereum: https://eth.llamarpc.com

# Sonra sırasıyla CTRL + X, Y ve Enter diyerek editörden çıkabilirsiniz.


#Ardından aşağıdaki kodu girin,
nano secret.conf.yaml

#Açılan pencereye daha önceden yedek almış olduğunuz publickey ve secretkey inizi xxx yazan yerleri silerek giriniz.

publickey: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
secretkey: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

# Sonra sırasıyla CTRL + X, Y ve Enter diyerek editörden çıkabilirsiniz.

```
# Yukarıdaki işlemleri hallettiysek şimdi dosyamıza çalıştırma izni verelim.
chmod +x unchained.sh

# Artık çalıştırmaya hazırız! Aşağıdaki kod ile çalıştıralım.
./unchained.sh worker up -d

# Eğer node'unuza restart atma ihtiyacı duyarsanız bu komutu kullanabilirsiniz.

./unchained.sh worker restart

# Logları Kontrol Etmek İçin

 ./unchained.sh worker logs -f 

# Loglardan Çıkış İçin
Ctrl + C

> [!WARNING]
> # PUAN ARTIŞI OLMUYORSA MUHTEMELEN GO SİZE BAŞKA BİR PUBLİC KEY ATAMIŞTIR, ONUN İÇİN AŞAĞIDAKİ GÖRSELE BAKARAK DOĞRU DİZİNİ BULUN VE GÖRSELDEKİ 2 DOSYAYI KENDİNİZE GÖRE UYARLAYIN,

![image](https://github.com/geocmsk/Kenshi-Go-Docker-Kurulumu/assets/90604931/26a241b3-e21e-412c-8bf2-b6fc32495e61)


# Takip Ederseniz Sevinirim :) Düzenleme için @Dtractus hocama teşekkür ederim


