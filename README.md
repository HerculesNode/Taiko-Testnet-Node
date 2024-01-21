# Taiko Node Kurulum Rehberi
![image](https://user-images.githubusercontent.com/101635385/210137987-bdc3fe6f-270d-40f8-b843-d927a58ca6e9.png)


<h1 align="center"> Taiko Alpha-3 Node </h1>
<h1 align="center"> Merhaba taiko Alpha-3 Node kurulum rehberi <br> << Hercules >>
</h1>

## 🟢 Ön bilgi

Sistem 30303 port ile çalışıyor eğer 30303 portu başka bir uygulama kullanıyorsa altta port değiştirme işlemini yapın. <br>


### Taiko Bridge:

 * [Bridge](https://bridge.test.taiko.xyz/#/)
 * [Ağları Cüzdana Ekleme ](https://chainid.network/)
 * [Explorer](https://explorer.test.taiko.xyz/)

 
 ### Linkler
 * [Hercules Telegram](https://t.me/HerculesNode)
 * [Hercules Twitter](https://twitter.com/Hercules4413)
 * [Taiko Dc](https://discord.gg/taikoxyz)
 
 ## 🟢 Sistem özellikleri



Önerilern:
- CPU - 16 cores
- Memory - 32GB RAM
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

<br><br>

Şimdi sepolia RPC almamız gerekiyor Alchemy üzerinden alabilirsiniz. 

![image](https://github.com/herculessx/Taiko-Testnet-Node/assets/101635385/cf92585d-94c3-4a3a-8a76-b5416620351b)




L1_ENDPOINT_HTTP=Alchemy üzerinden alacağınız https linki<br>
L1_ENDPOINT_WS=Alchemy üzerinden alacağınız wss linki

![image](https://user-images.githubusercontent.com/101635385/226990799-a596650f-1978-4d0a-8fb2-021d07672d62.png)

<br>

![image](https://user-images.githubusercontent.com/101635385/226991109-bc633b4b-d30a-405a-90ad-667f99d48684.png)


<br><br>

ENABLE_PROVER=true yapın<br>
L1_PROVER_PRIVATE_KEY=Matemask adresinizin private keyini yazın

![image](https://user-images.githubusercontent.com/101635385/226991245-2543ea5d-5371-4fa1-be81-243dfb68413a.png)


*ctrl + x Yes diyerek kaydediyoruz. <br>

<br>




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

![image](https://user-images.githubusercontent.com/101635385/226992188-1f9174f9-9b8c-4593-bbe8-ece1086d56e4.png)


## 🟢 Explorer üzerinden block görüntüleme 


 * [Explorer](https://explorer.test.taiko.xyz/)



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

![image](https://user-images.githubusercontent.com/101635385/226996911-78dd39d2-d08c-4630-9ae6-e7e0cae90842.png)




Artık sorunsuz çalıştırabilirsiniz. 


## 🟢Token oluşturma 

https://twitter.com/Hercules4413/status/1638791758635991040


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
forge create --legacy --rpc-url https://rpc.a2.taiko.xyz --private-key CÜZDAN-PRİVATE-KEY src/Counter.sol:Counter
```

![image](https://user-images.githubusercontent.com/101635385/210168108-94cac132-d52e-4c0f-9d90-43043e5d1a7a.png)


Sözleşme aşağıdaki gibi oluştu. Kod bölümüne gelin ve doğrulayı tıklayın bir sayfa açılacak en altta doğrula butonuna basın

![image](https://user-images.githubusercontent.com/101635385/210168140-b4b0413e-3020-46d1-8e6a-58468094abdb.png)

![image](https://user-images.githubusercontent.com/101635385/210168227-efba71d6-7e5e-40aa-91a6-b846dcdb4903.png)



## 🟢 Sepolia Ağı TTKO token



Sepolia ağında TTKO test tokenleri geldiyse aşağıdaki işlemleri yapınız.  Gelip gelmediğini kontrol etmek için isterseniz Tilki cüzdanınızdan explorerde görüntüle diyebilir yada tilki cüzdana aşağıdaki sözleşme adresini ekleyerek bakabilirsiniz.

TTKO Sözleşme adresi : 0xE52952B8063d0AE6Bd35E894866d8148976ce645

![image](https://github.com/herculessx/Taiko-Testnet-Node/assets/101635385/1c8eae94-c247-4413-b3f0-40511b1b6416)



```
cd simple-taiko-node
```

```
docker compose down
```



Sözleşme üzerinden deposit işlemi yapın. 50 tane yatırmanız gerekiyor

https://sepolia.etherscan.io/address/0x6375394335f34848b850114b66a49d6f47f2cda8#writeProxyContract#F2

![image](https://github.com/herculessx/Taiko-Testnet-Node/assets/101635385/fc15ef0d-9fa3-4cee-ab58-5279f36b7737)


amount kısmına 5000000000  bunu yazın ve write butonuna basın ardından tilki cüzdanından onay isteyecek. Ardından aşağıdaki işlemlere devam edin.


```
nano .env
```

.env dosyanıza girdiğinizde en altta bulunan alanı aşağıdaki gibi değiştirin. CTRL + X YES komutu ile kaydedin ardından alttaki komut ile nodenizi çaıştırın.


ENABLE_PROPOSER=true <br>
L1_PROPOSER_PRIVATE_KEY=MATEMASK CÜZDAN PRİVATE KEY <br>
L2_SUGGESTED_FEE_RECIPIENT=MATEMASK CÜZDAN ADRESİNİZ <br>



```
docker compose up
```

Sonuç

![image](https://github.com/herculessx/Taiko-Testnet-Node/assets/101635385/6987b0a2-a5d7-4b96-a14e-1806cce648be)

<br>

Yatıdığınız 50 TTKO tokenin ne kadar kaldığını görmek için aşağıdaki adresten Cüzdan adresinizi yazın.  

https://sepolia.etherscan.io/address/0x6375394335f34848b850114b66a49d6f47f2cda8#readProxyContract#F10

![image](https://github.com/herculessx/Taiko-Testnet-Node/assets/101635385/e5089611-2390-49bb-be37-338e9bb53f1c)





Forklamayı ve beğenmeyi unutmayınız :)
