🛡️ OWASP Juice Shop: SQL Injection & Docker Lab

![Kali Linux](https://img.shields.io/badge/OS-Kali%20Linux-557C94?style=for-the-badge&logo=kalilinux&logoColor=white)
![Docker](https://img.shields.io/badge/Infrastructure-Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![OWASP](https://img.shields.io/badge/Target-OWASP%20Juice%20Shop-000000?style=for-the-badge&logo=owasp&logoColor=white)

📌 Proje Özeti
Bu çalışma, web uygulama güvenliği zafiyetlerini güvenli ve izole bir ortamda analiz etmek amacıyla gerçekleştirilmiştir. **OWASP Juice Shop** projesi, **Docker** konteynerizasyon teknolojisi kullanılarak Kali Linux üzerinde ayağa kaldırılmış ve **SQL Injection (SQLi)** saldırı vektörü ile kimlik doğrulama mekanizması (Authentication Bypass) test edilmiştir.

Bu laboratuvar ortamı, bir **DevSecOps** yaklaşımıyla, zafiyetlerin sömürülmesini (exploit) ve bu zafiyetlere karşı alınacak önlemleri anlamak için kurulmuştur.

---

🛠️ Kullanılan Teknolojiler ve Araçlar

İşletim Sistemi: Kali Linux (Virtual Machine)
Konteyner Altyapısı: Docker
Hedef Uygulama: OWASP Juice Shop (v17.1.1)
Saldırı Türü: SQL Injection (Broken Authentication)

---

🚀 Kurulum Adımları (Laboratuvar Ortamı)

Proje, yerel makinede herhangi bir bağımlılık sorunu yaşamamak ve sistemi izole etmek için Docker üzerinde çalıştırılmıştır.

1. Docker İmajının Çekilmesi
Öncelikle OWASP Juice Shop'un resmi Docker imajı pull edildi:

sudo docker pull bkimminich/juice-shop

2. Konteynerin Başlatılması

Uygulama, 3000 portu üzerinden yayınlanacak şekilde başlatıldı:

sudo docker run --rm -p 3000:3000 bkimminich/juice-shop
Komut çalıştırıldıktan sonra tarayıcı üzerinden http://localhost:3000 adresine gidilerek uygulamaya erişildi.

⚔️ Zafiyet Analizi: SQL Injection
Senaryo: Uygulamanın giriş (Login) sayfasında, kullanıcı girdilerinin veritabanı sorgusuna dahil edilmeden önce yeterince sterilize edilmediği (sanitization) test edilmiştir.

Uygulanan Adımlar:

Keşif: Login sayfasına gidildi (/login).

Payload Denemesi: E-posta alanına klasik bir SQLi payload'u girildi.

Payload: ' or 1=1 --

Parola: (Rastgele herhangi bir karakter, örn: admin)

Sonuç: Sistem, ' karakteri ile e-posta sorgusunu kapattı ve OR 1=1 koşulu her zaman DOĞRU (TRUE) döndürdüğü için veritabanındaki ilk kullanıcı (genellikle Administrator) olarak oturum açılmasına izin verdi.

Erişim: Admin yetkileriyle sisteme giriş yapıldı ve normal kullanıcıların erişemeyeceği yönetim paneli ile hassas verilere ulaşıldı.

⚠️ Yasal Uyarı (Disclaimer):

Bu proje ve dokümantasyon tamamen eğitim amaçlıdır. Burada gösterilen teknikler, yalnızca sahibi olduğunuz veya test izniniz olan sistemler üzerinde (Laboratuvar ortamları, Bug Bounty programları vb.) kullanılmalıdır. İzinsiz sistemlere saldırı yapmak suçtur.

🔗 İletişim:
Berat Özkan - Cloud Computing & DevSecOps Student
ozknnberat7@gmail.com

LinkedIn Profilim:
https://www.linkedin.com/in/ozknnberat/
