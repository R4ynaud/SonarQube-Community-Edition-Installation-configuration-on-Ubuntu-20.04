# SonarQube 8.9 Community Edition Installation & Configuration On Ubuntu 22.04


Guide to SonarQube 8.9 Community Edition Installation & Configuration On Ubuntu 22.04


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


## Support for MySQL has been removed in SonarQube. Please increase vm.max_map_count, file descriptors, and ulimit at runtime for the existing session.


## SonarQube için MySQL Desteği kaldırıldı. Çalışma zamanında mevcut oturum için vm.max_map_count çekirdeğini, dosya tanımlayıcısını ve ulimit'i artırın.


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/f3b705fc-40a9-403b-8215-0c5453f872ba)


```
sysctl -w vm.max_map_count=524288
```
```
sysctl -w fs.file-max=131072
```
```
ulimit -n 131072
```
```
ulimit -u 8192
``` 


## To permanently increase vm.max_map_count, file descriptors, and ulimit, open the configuration file below and add the following value as shown below.


## Vm.max_map_count çekirdeğini, dosya tanımlayıcısını ve ulimit'i kalıcı olarak artırmak için. Aşağıdaki yapılandırma dosyasını açın ve aşağıdaki değeri aşağıda gösterildiği gibi ekleyin.


```
vim /etc/security/limits.conf
```
```
sonarqube   -   nofile   65536
sonarqube   -   nproc    4096
```
```
:wq!
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/ef86034a-6020-4df6-ac9f-6cb5fa66b783)


## Before installing, Lets update and upgrade System Packages.


## Kurulumdan önce Sistem Paketlerini güncelleyelim.


```
apt-get update
```

```
apt-get upgrade
```


## Install wget and unzip package.


## Wget'i yükleyin ve paketi çıkartın.


```
apt-get install wget unzip -y
```

![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/67ebdb4b-5855-4687-87e5-de0fcdd62f22)


## Install OpenJDK and JRE 11 using following command. 


## Aşağıdaki komutu kullanarak OpenJDK ve JRE 11'i yükleyin.


```
apt-get install openjdk-17-jdk -y
```

```
apt-get install openjdk-17-jre -y
```

```
 java -version
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/a688d78d-4318-43d4-81e5-41a9466437f6)


## Run the following commands to install PostgreSQL 10 for SonarQube.


## SonarQube için PostgreSQL 10'u yüklemek üzere aşağıdaki komutları çalıştırın.


```
sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'
```

```
wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | sudo apt-key add -
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/323f2cd5-be03-474a-80df-1ff5925fba75)


## Install the PostgreSQL database server using the following command.


## Aşağıdaki komutu kullanarak PostgreSQL veritabanı sunucusunu kurun.


```
apt-get -y install postgresql postgresql-contrib
```

![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/e43b1108-87c7-4558-bc02-3d5546b53ee9)


## Start the PostgreSQL database server using the following command.


## Aşağıdaki komutu kullanarak PostgreSQL veritabanı sunucusunu başlatın.


```
systemctl start postgresql
```
```
systemctl enable postgresql
```

![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/457b505c-6aa4-49bf-a3af-d43ac8a4948a)


## Change the password for the default PostgreSQL user.


## Varsayılan PostgreSQL kullanıcısının şifresini değiştirin.


```
passwd postgres
```

![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/cc3cdf47-6b0c-4a70-a98d-0a1a56471501)


## Switch to the postgres user.


## Postgres kullanıcısına geçin.


```
su - postgres
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/29234b22-6650-4b2d-acbe-1d7d8b0b061c)


## Create a new user by running the following commands.


## Aşağıdaki komutları çalıştırarak yeni bir kullanıcı oluşturun.


```
createuser sonar
```

```
psql
```

```
ALTER USER sonar WITH ENCRYPTED password '1';
```

```
CREATE DATABASE sonarqube OWNER sonar;
```

```
grant all privileges on DATABASE sonarqube to sonar;
```

```
\q
```

```
exit
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/bbbc4e09-3c7c-4349-9a25-3b76b14772f9)


## Run the following command to download SonarQube.


## SonarQube'u indirmek için aşağıdaki komutu çalıştırın.


```
cd /tmp
```

```
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.9.0.65466.zip
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/f5488de1-971c-468c-a8e5-2e4f45689cbc)


## Run the following command to download SonarQube.


## SonarQube'u indirmek için aşağıdaki komutu çalıştırın.


```
unzip sonarqube-9.9.0.65466.zip -d /opt
```
```
mkdir /opt/sonarqube
```
```
mv /opt/sonarqube-9.9.0.65466 /opt/sonarqube
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/eb9f8b00-9642-4095-a799-bebc55bbfb8c)



## Follow the steps below to configure SonarQube on our Ubuntu 22.04 operating system.


## Ubuntu 22.04 işletim sistemimizde SonarQube'u yapılandırmak için aşağıdaki adımları izleyin.


```
groupadd sonar
```
```
useradd -c "user to run SonarQube" -d /opt/sonarqube/sonarqube-9.9.0.65466 -g sonar sonar 
```
```
chown sonar:sonar /opt/sonarqube/sonarqube-9.9.0.65466 -R
```


## Open the SonarQube configuration file using Vim.


## Vim'i kullanarak SonarQube yapılandırma dosyasını açın.


```
vim /opt/sonarqube/sonarqube-9.9.0.65466/conf/sonar.properties
```


## Find the following lines.


## Aşağıdaki satırları bulun.


```
#sonar.jdbc.username=
#sonar.jdbc.password=
```


## Uncomment and Type the PostgreSQL Database username and password which we have created in above steps and add the postgres connection string.


## Yukarıdaki adımlarda oluşturduğumuz PostgreSQL veritabanı kullanıcı adını ve şifresini yazın ve Postgres bağlantı dizesini ekleyin.


```
sonar.jdbc.username=sonar 
sonar.jdbc.password=1
sonar.jdbc.url=jdbc:postgresql://localhost:5432/sonarqube (#sonar.jdbc.url=jdbc:postgresql://localhost/sonarqube?currentSchema=my_schema)
sonar.log.level=INFO
sonar.path.logs=logs


```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/aa6a3a95-1c99-448f-ab49-a8fd0f4ce2f2)



## Edit the sonar script file and set RUN_AS_USER.


## Sonar komut dosyası dosyasını düzenleyin ve RUN_AS_USER'ı ayarlayın.


```
vim /opt/sonarqube/sonarqube-9.9.0.65466/bin/linux-x86-64/sonar.sh

```

```
 RUN_AS_USER="sonar"
```

![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/90537599-5eb3-4076-b363-b797dbbb17bd)


## Now to start SonarQube we need to do following: Switch to sonar user


## Şimdi SonarQube'u başlatmak için aşağıdakileri yapmamız gerekiyor: Sonar kullanıcısına geçiş yapın


```
sudo su sonar

```

```
 cd /opt/sonarqube/sonarqube-9.9.0.65466/bin/linux-x86-64
```

```
./sonar.sh start
```
```
./sonar.sh status
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/c9927fc0-70db-4a26-8a3a-824df5a96e12)



## To check sonarqube logs, navigate to /opt/sonarqube/sonarqube-9.9.0.65466/logs/sonar.log directory.


## SonarQube loglarını kontrol etmek için /opt/sonarqube/sonarqube-9.9.0.65466/logs/sonar.log dizinine gidin


```
tail /opt/sonarqube/sonarqube-9.9.0.65466/logs/sonar.log

```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/1cfb4f34-4ea1-4929-87ad-14d6093653be)


## Configure Systemd service.


## Systemd hizmetini yapılandırma.


```
cd /opt/sonarqube/sonarqube-9.9.0.65466/bin/linux-x86-64
```

```
./sonar.sh stop
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/84b08532-9d92-476d-bac1-8ffe85c5598e)


## Create a systemd service file for SonarQube to run as System Startup.


## SonarQube'un Sistem Başlangıcı olarak çalışması için bir systemd servis dosyası oluşturun.


```
vim /etc/systemd/system/sonar.service
```

```
[Unit]
Description=SonarQube service
After=syslog.target network.target

[Service]
Type=forking

ExecStart=/opt/sonarqube/sonarqube-9.9.0.65466/bin/linux-x86-64/sonar.sh start
ExecStop=/opt/sonarqube/sonarqube-9.9.0.65466/bin/linux-x86-64/sonar.sh stop

User=sonar
Group=sonar
Restart=always

LimitNOFILE=65536
LimitNPROC=4096

[Install]
WantedBy=multi-user.target

```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/c2694fed-edee-4781-9764-51cc9c700283)



## Start the SonarQube service by running the following commands.


## Aşağıdaki komutları çalıştırarak SonarQube servisini başlatın.


```
systemctl start sonar
```
```
systemctl enable sonar
```
```
systemctl status sonar
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/ba2140e6-0f62-4a66-b3f2-c8b05e6f87a1)


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/fe8b4ba8-cedc-4817-91f8-d7d241d9381f)



![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/fa5117db-4782-4f1d-8e2f-fefc5db50457)


## What Is An Nginx ? 


• Nginx, an open-source web server and reverse proxy server software. Nginx is used to create high-performance, fast, reliable, and scalable web servers. 


### 1-) Web Server: Nginx serves as an HTTP server used to deliver websites. It receives requests from clients' browsers and serves the corresponding web pages or content.


## Nginx Nedir ? Ne İşe Yarar ?


•




## Run the following commands to install Nginx.


## Nginx'i yüklemek için aşağıdaki komutları çalıştırın.


```
apt update
```

```
apt install nginx
```

![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/b7f50e4c-757b-4f54-90d7-6a2b9d46d2de)

```
nginx -v

```
![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/fe7d87d1-4994-4d1e-8628-01a6d084bb27)

```
systemctl enable nginx
```
```
systemctl start nginx
```
```
systemctl status nginx
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/123376a0-bcb1-4b95-9411-25a5aab0afe0)


## To check Nginx, run the following command.


## Nginx'i kontrol etmek için aşağıdaki komutu çalıştırın.


```
 curl -i 127.0.0.1
```

![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/a73a48e4-ccfa-4223-85ed-68f341400c68)


## Auto remove command !


```
apt autoremove nginx --purge
```


## To redirect Nginx to a custom domain, we need to create a 'DNS Zone' through the 'Azure Portal'.


## Nginx'i özel bir etki alanına yönlendirmek için 'Azure Portal' aracılığıyla bir 'DNS Bölgesi' oluşturmamız gerekiyor.



## Azure portalında 'Kaynaklar' sekmesine tıklayalım.


## Let's click on the 'Resources' tab in the Azure portal.



![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/3603c1b3-492e-4714-b08e-872d5bf73914)




## Let's click on the 'DNS Zone' tab in the Marketplace.


## Marketplace'te 'DNS Zone' sekmesine tıklayalım.


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/cb10f60b-144e-4faa-a01c-55eed5c991a6)


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/c9dca7b7-330b-4f44-8cb2-7ba22f1fcb85)


## After clicking the 'Create' button, select the resource group where SonarQube & Nginx are installed from the 'Subscription' field, and finally click on the 'Review Create' tab.


## 'Create' butonuna bastıktan sonra 'Subscription' alanından 'Resource Group' alanına SonarQube & Ngnix'in kurulu olduğu resource group'u seçip son olarak 'Review Create' sekmesine tıklıyoruz.


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/c965e81f-9096-4d5e-921b-df7ed8516516)



![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/4ca5232c-51aa-4083-aa68-489289767f8e)



# Azure DevOps configuration


# Azure DevOps konfigürasyonu.


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/a84b7241-0918-43db-be55-bb9595d4f53e)


## We are adding the SonarQube extension from the Marketplace.


## Marketplace'den SonarQube eklentisini ekliyoruz.

## 1-)
![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/ed9bda2b-51db-479b-8aeb-7e9302855697)

## 2-)
![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/b0e31c06-dd5b-4a14-8123-8eb32f4f6484)

## 3-)
![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/7cc40f70-37e8-4192-b709-d5395015fd87)

## 4-)
![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/a6dd6bd6-c99c-4b41-a8b9-eca76c0923a0)


## And We will generate a token for SonarQube.


## Ve SonarQube için bir token üreteceğiz.



SonarQube → Administrator → MyAccount → Security 


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/9606aa2e-1b1a-4358-aa1d-fe80728dd500)


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/45075f33-d701-41fe-a215-07c8bac08d5a)


## We will name the token to be used for Azure DevOps and click “Generate” button. We will use this token for Azure Devops soon so make sure you save this token. 


## Azure DevOps için kullanılacak tokena isim vereceğiz ve “Oluştur” butonuna tıklayacağız. Bu belirteci yakında Azure Devops için kullanacağız, bu nedenle bu belirteci kaydettiğinizden emin olun.


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/850bf5b2-97a3-439a-90f0-8942029a7570)


## Now we will configure Azure DevOps.


## Şimdi Azure DevOps'u yapılandıracağız. 


Project Settings → Service Connections → New service connection→ SonarQube 


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/5bfd99d4-8721-4438-b05c-baf4a451a970)


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/05704a13-f528-4854-b8da-e17770f274ec)


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/08f266ef-aa64-4f71-a99d-beea7d84cd6d)


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/5de9c820-bddb-40d8-a9f7-23d765ed490b)


## We are opening our .yml file to integrate SonarQube.


## SonarQube entegrasyonu için .yml dosyamızı açıyoruz. 


## 1-) 
![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/8eefdee1-34b9-48e9-be51-75e70b1e3c4c)


## 2-)
![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/f38c9504-d60f-4226-8eb2-fe1eb7622151)


## We add 'SonarQube' from the 'Search' field by clicking the 'Add Task' button in the Task field.


## Task alanından " Add Task " butonuna tıklayarak " Search " alanından 'SonarQube' ekliyoruz.


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/30581413-653e-4bc6-9b4c-440ccc4edb60)

















