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
• For the other user ;
```
 sudo apt install openjdk-11-jdk
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/62e84804-1e8e-4efc-8189-79c0269707df)


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/ec073f71-f837-4bbf-8b01-44cc7375b2ea)


### 2-) Run the following command to download the latest version of SonarQube.


### 2-) SonarQube'un en son sürümünü indirmek için aşağıdaki komutu çalıştırın.


```
 wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-10.1.0.73491.zip
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/abcf4a0d-f2b5-40dd-aeb2-c104bd846384)


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/26b9e670-4d4f-42ea-860a-c8f0ca67e07b)


### 3-) Extract the downloaded file from the zip archive.


### 3-) İndirilen dosyayı zip arşivinden çıkarın. 


```
unzip sonarqube-10.1.0.73491.zip
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/e7112e93-842f-43b6-a969-fc0c339604d2)


### 4-) Let's create a new folder named 'sonarqube' under the '/opt' directory.


### 4-) '/opt' dizini altında 'sonarqube' adında yeni bir klasör oluşturalım.


```
mkdir opt/sonarqube
```


### 5-) Move the 'sonarqube-10.1.0.73491' folder to the 'sonarqube' folder that we created.


### 5-) 'sonarqube-10.1.0.73491' klasörünü oluşturduğumuz 'sonarqube' klasörüne taşıyın.


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/e842a41a-72fc-416d-8c43-3d6f0b2bb345)


• For the root user ;
```
 mv sonarqube-10.1.0.73491 /opt/sonarqube
```
• For the other user ;
```
 sudo mv sonarqube-10.1.0.73491 /opt/sonarqube
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/d1f81040-56a5-4128-8457-b3691aadc783)


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-20.04/assets/93924485/c3e8d5d7-e1da-4063-8628-02d98a30610e)



### 6-) Let's create a user for SonarQube.


### 6-) SonarQube için bir kullanıcı oluşturalım.


• For the root user ;
```
 adduser --system --no-create-home --group sonarqube
```
```
 chown -R sonarqube:sonarqube /opt/sonarqube
```
• For the other user ;
```
 sudo adduser --system --no-create-home --group sonarqube
```
```
 sudo chown -R sonarqube:sonarqube /opt/sonarqube
```















