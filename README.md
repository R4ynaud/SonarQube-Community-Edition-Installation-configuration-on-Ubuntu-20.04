# SonarQube Community Edition Installation & Configuration On Ubuntu 20.04


Guide to SonarQube Community Edition Installation & Configuration On Ubuntu 20.04


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/83af9c1f-d925-47d8-9cc7-330bffece55d)


## What Is an SonarQube ?  


• SonarQube is an open-source platform used for analyzing and monitoring code quality and security. This platform offers various tools and features to assess and enhance the quality of code throughout every stage of the software development process.


• Its main purpose is to improve the performance, security, sustainability, and overall quality of software projects. SonarQube provides static code analysis, code coverage reports, code smell analysis, security vulnerability scans, code duplications detection, and many more assessment and reporting tools.


Key features of SonarQube include:


1-) Static Code Analysis: Detects errors, style violations, and quality issues in your codebase.


2-) Code Coverage Reports: Shows which parts of the codebase are covered by tests, allowing you to assess test coverage.


3-) Code Smell Analysis: Identifies code smells and indicates the likelihood of these smells affecting code quality.


4-) Security Vulnerability Scans: Identifies known security vulnerabilities and weaknesses, helping to minimize security risks.


5-) Code Duplications: Detects repeated code blocks and structures, promoting code sustainability and cleanliness.


6-) Integration Tools: Integrates with DevOps tools, enabling continuous monitoring and improvement of code quality.


7-) Support for Various Programming Languages: Offers support for multiple programming languages.


This allows development teams to observe the overall quality and security of code, catch errors in early stages, and make software projects more robust, secure, and maintainable.


## SonarQube Nedir ? Ne İşe Yarar ? 


• SonarQube, kod kalitesi ve güvenliği analiz etmek ve izlemek için kullanılan açık kaynaklı bir platformdur. Bu platform, yazılım geliştirme sürecinin her aşamasında kodun kalitesini değerlendirmek ve geliştirmek için çeşitli araçlar ve özellikler sunar.


• Ana amacı, yazılım projelerinin performansını, güvenliğini, sürdürülebilirliğini ve genel kalitesini artırmaktır. SonarQube, statik kod analizi, kod kapsamı raporları, kod kokulu analizi, güvenlik açıkları taraması, kod tekrarları ve daha pek çok değerlendirme ve raporlama aracı sunar.


SonarQube'un ana özellikleri şunlar olabilir:


1-) Statik Kod Analizi: Kod tabanınızdaki hataları, stil ihlallerini ve kalite sorunlarını tespit eder.


2-) Kod Kapsamı Raporları: Hangi bölümlerin kod kapsamı içinde olduğunu görüntüler, böylece test kapasitesini değerlendirebilirsiniz.


3-) Kod Kokulu Analizi: Kod kokularını (Code Smells) tespit eder ve bu kokuların kaliteyi olumsuz etkileme olasılığını belirtir.


4-) Güvenlik Açıkları Taraması: Bilinen güvenlik açıklarını ve zayıf noktaları tespit eder, böylece güvenlik risklerini minimize edebilirsiniz.


5-) Kod Tekrarları: Tekrarlanan kod bloklarını ve yapıları tespit eder, böylece kodun daha sürdürülebilir ve temiz olmasını sağlar.


6-) Entegrasyon Araçları: DevOps araçlarıyla entegrasyon sağlar, böylece kod kalitesini sürekli olarak izlemeyi ve geliştirmeyi kolaylaştırır.


7-) Çeşitli Programlama Dilleri Desteği: Birden fazla programlama dili için destek sunar.


Bu sayede geliştirme ekibi, kodun genel kalitesini ve güvenliğini gözlemleyebilir, hataları erken aşamalarda yakalayabilir ve yazılım projelerini daha sağlam, güvenli ve sürdürülebilir hale getirebilir.


## First, let's download the "SonarQube Community Edition" version from the address https://www.sonarsource.com/.


## Öncelikle https://www.sonarsource.com/ adresinden 'SonarQube Community Edition' sürümünü indirelim.


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/0e5a70c5-4c6a-43fa-8622-b1abe3861f86)
 

![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/8b1f0639-d36f-499e-aa4b-05279f212203)


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/7e56de0b-9e88-4bef-8bd0-cee061922404)


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/c44fac73-b328-4b4f-9127-1cdf27e403a6)


## SonarQube kurulumuna geçmeden önce PostgreSQL veritabanını kurmamız gerekiyor,  PostgreSQL veritabanını kurmak için aşağıdaki komutları sırayla çalıştırın.


## Before proceeding with the SonarQube installation, we need to install the PostgreSQL database. To install the PostgreSQL database, execute the following commands in sequence.

```
sysctl -w vm.max_map_count=262144
```
```
sysctl -w fs.file-max=65536
```
```
ulimit -n 65536
```
```
ulimit -u 4096
```
```
vim /etc/security/limits.conf
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/5c4cf2b7-acd2-4ca9-9a88-b64c36985ade)


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/7708f02a-5e5c-41d0-847a-6e05d2892536)


• For the root user ;
```
apt update -y
```
```
sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'
```
```
wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | sudo apt-key add -
```
```
apt install postgresql postgresql-contrib -y
```
```
systemctl enable postgresql
```
```
systemctl start postgresql
```
```
systemctl status postgresql
```
```
passwd postgres
```
![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/8272efe1-694b-4946-848c-691843d64db9)


```
passwd postgres
```
```
su - postgres
```
```
create user sonarqube
```
```
psql
```
```
ALTER USER sonarqube WITH ENCRYPTED password 'Son4r23+';
```
```
CREATE DATABASE sonarqube OWNER sonarqube;
```
```
GRANT ALL PRIVILEGES ON DATABASE sonarqube to sonarqube;
```
```
\q
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/b784a602-1fa9-4935-8af8-cdaa105fdb8e)


• For the other user ;
```
sudo apt update -y
```
```
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'
```
```
wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | sudo apt-key add -
```
```
sudo apt install postgresql postgresql-contrib -y
```
```
sudo systemctl enable postgresql
```
```
sudo systemctl start postgresql
```
```
sudo systemctl status postgresql
```
```
sudo  passwd postgres
```
![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/8272efe1-694b-4946-848c-691843d64db9)


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/d9b9f933-6539-4465-994c-f9baf8a2f0b5)


```
sudo passwd postgres
```
```
su - postgres
```
```
create user sonarqube
```
```
psql
```
```
ALTER USER sonarqube WITH ENCRYPTED password 'Son4r23+';
```
```
CREATE DATABASE sonarqube OWNER sonarqube;
```
```
GRANT ALL PRIVILEGES ON DATABASE sonarqube to sonarqube;
```
```
\q
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/b784a602-1fa9-4935-8af8-cdaa105fdb8e)



## Let's begin the installation of SonarQube's Community Edition version on our operating system.


## İşletim sistemimize SonarQube'ın Community Edition sürümünü kurmaya başlayalım. 


### 1-) Kurulumdan önce işletim sistemimizin paketlerini güncellemek için aşağıdaki komutları çalıştırıyoruz.


### 1-) We run the following commands to update our operating system's packages before installation.


• For the root user ;
```
 apt-get update 
```
• For the other user ;
```
 sudo apt-get update
```
• For the root user ;
```
 apt-get upgrade
```
• For the other user ;
```
 sudo apt-get upgrade
```


### 1-) Please execute the following command for Java installation.


### 1-) Java kurulumu için aşağıdaki komutu çalıştırın.


• For the root user ;
```
 apt install openjdk-11-jdk
```
```
 vim /etc/environment
```
```
 JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"
```
• For the other user ;
```
 sudo apt install openjdk-11-jdk
```
```
 sudo vim /etc/environment
```
```
 JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"
```

![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/62e84804-1e8e-4efc-8189-79c0269707df)


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/ec073f71-f837-4bbf-8b01-44cc7375b2ea)


### 2-) Run the following command to download the latest version of SonarQube.


### 2-) SonarQube'un en son sürümünü indirmek için aşağıdaki komutu çalıştırın.


```
 wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.8.0.63668.zip
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/00f2454b-1c14-40df-9fa9-34cee09f5ec3)


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/f5242279-4970-45bb-b51a-1379ee175309)


### 3-) Extract the downloaded file from the zip archive.


### 3-) İndirilen dosyayı zip arşivinden çıkarın. 


```
unzip sonarqube-9.8.0.63668.zip
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/80d56c99-638f-447a-a2a7-8887957d5736)



### 4-) Let's create a new folder named 'sonarqube' under the '/opt' directory.


### 4-) '/opt' dizini altında 'sonarqube' adında yeni bir klasör oluşturalım.


```
mkdir opt/SonarQube
```


### 5-) Move the 'sonarqube-9.8.0.63668' folder to the 'SonarQube' folder that we created.


### 5-) 'sonarqube-9.8.0.63668' klasörünü oluşturduğumuz 'SonarQube' klasörüne taşıyın.


• For the root user ;
```
 mv sonarqube-9.8.0.63668 /opt/SonarQube
```
• For the other user ;
```
 sudo mv sonarqube-9.8.0.63668 /opt/SonarQube
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/94c3fc1f-3a57-4904-b12a-a08d38023370)


### 6-) Let's create a user for SonarQube.


### 6-) SonarQube için bir kullanıcı oluşturalım.


• For the root user ;
```
 adduser --system --no-create-home --group sonarqube
```
```
 chown -R sonarqube:sonarqube /opt/SonarQube
```
• For the other user ;
```
 sudo adduser --system --no-create-home --group sonarqube
```
```
 sudo chown -R sonarqube:sonarqube /opt/SonarQube
```


• Plugin ; 

```
 cd /opt/SonarQube/sonarqube-9.8.0.63668/extensions/plugins
```
```
 wget https://github.com/mc1arke/sonarqube-community-branch-plugin/releases/download/1.14.0/sonarqube-community-branch-plugin-1.14.0.jar
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/0141f9ec-1cc1-4963-a803-2442710d4769)


• SonarQube configuration ; 


```
vim opt/SonarQube/sonarqube-9.8.0.63668/conf/sonar.properties
```


```
sonar.jdbc.username=sonarqube
sonar.jdbc.password=Son4r23+
sonar.jdbc.url=jdbc:postgresql://localhost:5432/sonarqube

sonar.web.javaAdditionalOpts=-javaagent:/opt/SonarQube/sonarqube-9.8.0.63668/extensions/plugins/sonarqube-community-branch-plugin-1.14.0.jar=web
sonar.ce.javaAdditionalOpts=-javaagent:/opt/SonarQube/sonarqube-9.8.0.63668/extensions/plugins/sonarqube-community-branch-plugin-1.14.0.jar=ce
```


### 7-) Create a systemd service file to run SonarQube as a system service.


### 7-) SonarQube'u sistem servisi olarak çalıştırmak için bir systemd servisi dosyası oluşturalım.


• For the root user ;
```
 vim /etc/systemd/system/sonarqube.service
```
• For the other user ;
```
 sudo vim /etc/systemd/system/sonarqube.service
```


```

[Unit]

Description=SonarQube service

After=syslog.target network.target


[Service]

Type=forking


ExecStart=/opt/SonarQube/sonarqube-9.8.0.63668/bin/linux-x86-64/sonar.sh start

ExecStop=/opt/SonarQube/sonarqube-9.8.0.63668/bin/linux-x86-64/sonar.sh stop


User=sonarqube

Group=sonarqube

Restart=always


LimitNOFILE=65536

LimitNPROC=4096


[Install]

WantedBy=multi-user.target


```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/476005c8-6353-48c9-af1d-3c8889e0ab7b)


```
wq!
```


### 8-) Let's grant the necessary permissions through the firewall.


### 8-) Güvenlik duvarı üzerinden gerekli izinleri verelim.


• For the root user ;
```
 ufw allow http
```
```
 ufw allow https
```
```
 ufw allow 9000
```
• For the other user ;
```
 sudo ufw allow http
```
```
 sudo ufw allow https
```
```
 sudo ufw allow 9000
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/b777b1e0-4fa5-433a-b9f1-9b5faf7faf14)



### 9-) Let's enable and start the services.


### 9-) Servisi etkinleştirip ve başlatalım.


• For the root user ;
```
 systemctl enable sonarqube
```
```
 systemctl start sonarqube
```
• For the other user ;
```
 sudo systemctl enable sonarqube
```
```
 sudo systemctl start sonarqube
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/a4ff04f3-e985-4989-8ec4-a85eabe43a09)


















