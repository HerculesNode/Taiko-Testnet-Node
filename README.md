# Taiko Node Kurulum Rehberi
![image](https://user-images.githubusercontent.com/101635385/210137987-bdc3fe6f-270d-40f8-b843-d927a58ca6e9.png)


<h1 align="center"> Taiko Node </h1>
<h1 align="center"> Merhaba taiko Node kurulum rehberi <br> << Hercules >>
</h1>

## 🟢 Ön bilgi

Node kurabilmeniz için öncelikle Platform testnetini yapmanız gerekiyor. Platform testnetinde kullandığınız cüzdan adresini burada kullanacağız. Sistem 6060 port ile çalışıyor celestia gibi node kurduysanız çakışacaktır buna dikkat ediniz. <br>

Platform testneti ile ilgili Bilgi <br>

* [Platform Tesneti](https://twitter.com/Hercules4413/status/1608026986164748288)


### Explorer:
 * [Explorer](https://l2explorer.a1.taiko.xyz/)

 
 ### Linkler
 * [Hercules Telegram](https://t.me/HerculesNode)
 * [Hercules Twitter](https://twitter.com/Hercules4413)
 * [Taiko Dc](https://discord.gg/taikoxyz)
 
 ## 🟢 Sistem özellikleri

Minimum:
- CPU with 2+ cores
- 4GB RAM
- 500 Gb 


Önerilern:
- Fast CPU with 4+ cores
- 16GB+ RAM
- High-performance SSD with at least 1TB of free space


## 🟢 Sistem Güncelleme
```shell
sudo apt update
```

```shell
sudo apt upgrade
```


## 🟢 Docker Setup

```shell
apt install docker-compose
```

```shell

sudo apt-get update && sudo apt install jq && sudo apt install apt-transport-https ca-certificates curl software-properties-common -y && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin && sudo apt-get install docker-compose-plugin

```


## 🟢 1. Taiko dosyalarını indirin

```
git clone https://github.com/taikoxyz/simple-taiko-node.git
```

Screen Oluşturalım
```
screen -S taiko
```

taiko Klasörüne Giriş yapalım
```
cd simple-taiko-node
```

.env dosyası oluşturalım. Bu dosyayı oluşturduktan sonra Taiko platform testnetinde kullandığınız adresin Private keyini Tilki cüzdanınızdan alacaksınız ve .env dosyasına kaydedeceksiniz. 
```
cp .env.sample .env
```

.Env dosyasına girelim burada değiştirmeniz gereken en alttaki bölüm. <br>

```
nano .env
```

<br>

*ENABLE_PROPOSER=true  ( Falseden true çeviriyoruz ) <br>
*L1_PROPOSER_PRIVATE_KEY= Cüzdanımızın private keyini yazıyoruz <br>
*L2_SUGGESTED_FEE_RECIPIENT= Cüzdan adresimizi yazıyoruz. <br>
*ctrl + x Yes diyerek kaydediyoruz. <br>

<br>

![image](https://user-images.githubusercontent.com/101635385/210138160-c01d12f1-c1d1-40b5-96f0-ac907d3110cc.png)

<br>

Private Key nasıl alınır sağdaki 3 noktaya tıklayın --- >> ardından hesap bilgileri --- >> Özel anahtarı dışa aktar

![image](https://user-images.githubusercontent.com/101635385/210151390-4342cbb3-5c1c-4e35-96ff-fde422ac08bb.png)

<br>

![image](https://user-images.githubusercontent.com/101635385/210151407-a7b0aa7e-ae39-47cc-b1ab-2697e0d25edf.png)





## 🟢 Çalıştırma

Bu işlem sonrası kurulum yapacak ve senkronize olmaya başlayacaktır.

```
docker-compose up
```

![image](https://user-images.githubusercontent.com/101635385/210138255-d7c31fb4-bbe4-4d6d-8703-6ee16f1a0b47.png)


## 🟢 Explorer üzerinden block görüntüleme 

Explorer üzerinden adresinizi yazın aşağıdaki resimdeki gibi ise sorun yok tabi önce senkronize olması gerekiyor. 

 * [Explorer](https://l2explorer.a1.taiko.xyz/)

![image](https://user-images.githubusercontent.com/101635385/210138905-3baea6ea-5424-4197-b4c4-0c23d9578247.png)


## 🟢 Log Görme

Eğer başta screen oluşturmadıysanız bir screen oıluşturup logları görebilirsiniz.

```
cd simple-taiko-node
docker compose logs -f
```


## 🟢 Durdurma

Bu işlem sonrası bloklar silinmez sadece node durur.

```
docker compose down
```

## 🟢 Nodeyi silme


```
docker compose down -v
cd
rm -fr simple-taiko-node
```


## 🟢 Port çakışması yaşayanlar

.env dosyasındaki portları resimdeki gibi yapın

![image](https://user-images.githubusercontent.com/101635385/212497942-98ebf473-517d-4932-b8d1-305bcfffde0c.png)


docker-compose dosyasındaki şu alanı değiştirin 


![image](https://user-images.githubusercontent.com/101635385/212497966-803cb9f5-40f5-4067-aaca-47469ee79d4c.png)


Artık sorunsuz çalıştırabilirsiniz. Hercules Node Telegram kanalında bunu paylaşan arkadaşa teşekkür ederim.



## 🟢 Sözleşme Oluşturma ( Bunu yapmak şart değil isterseniz yapın )

Bu işlem sonrası kurulum yapacak ve senkronize olmaya başlayacaktır.

```
curl -L https://foundry.paradigm.xyz | bash
```

![image](https://user-images.githubusercontent.com/101635385/210168053-69d942f9-65b9-44cc-a42f-32f6d086b537.png)


```
source /root/.bashrc
```

```
foundryup
```

![image](https://user-images.githubusercontent.com/101635385/210168068-bf4d800a-84e2-4c66-a65a-9f831307a6b5.png)


```
forge init hello_foundry && cd hello_foundry
```

Nodeyi kurduğunuz cüzdanın private keyini yazın 

```
forge create --legacy --rpc-url https://l2rpc.a1.taiko.xyz --private-key CÜZDAN-PRİVATE-KEY src/Counter.sol:Counter
```

![image](https://user-images.githubusercontent.com/101635385/210168108-94cac132-d52e-4c0f-9d90-43043e5d1a7a.png)


Sözleşme aşağıdaki gibi oluştu. Kod bölümüne gelin ve doğrulayı tıklayın bir sayfa açılacak en altta doğrula butonuna basın

![image](https://user-images.githubusercontent.com/101635385/210168140-b4b0413e-3020-46d1-8e6a-58468094abdb.png)

![image](https://user-images.githubusercontent.com/101635385/210168227-efba71d6-7e5e-40aa-91a6-b846dcdb4903.png)



Forklamayı ve beğenmeyi unutmayınız :)
