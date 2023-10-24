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
sonar.jdbc.url=jdbc:postgresql://localhost:5432/sonarqube/sonarqube-9.9.0.65466
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/eab71f29-8469-4f1a-964f-09a24c9e321e)


## Edit the sonar script file and set RUN_AS_USER.


## Sonar komut dosyası dosyasını düzenleyin ve RUN_AS_USER'ı ayarlayın.


```
vim /opt/sonarqube/sonarqube-9.9.0.65466/bin/linux-x86-64/sonar.sh

```

```
 RUN_AS_USER="sonar"
```

![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/90537599-5eb3-4076-b363-b797dbbb17bd)







--------------------------------------------------------////////////////////////





















