# Zabbix-Http-Poller
Zabbix Http Poller 
[TR]
# Zabbix HTTP Poller Processes Utilization Sorunu ve Çözümü

## 📖 Problem Tanımı
Zabbix server üzerinde "Utilization of HTTP poller processes over 75%" uyarısı, Zabbix'in HTTP poller süreçlerinin aşırı yüklendiğini ve kaynakların yetersiz kalmaya başladığını ifade eder. Bu durum, Zabbix'in HTTP tabanlı kontroller için yeterli poller sürecine sahip olmadığını gösterir. 

Bu sorun, aşağıdaki durumlarda ortaya çıkabilir:
- HTTP poller süreçlerinin sayısının yetersiz olması.
- İzlenen HTTP kontrollerinin sayısının hızla artması.
- Yanlış yapılandırılmış kontrol aralıklarının Zabbix server'ı gereksiz yere yorması.

---

## 🚀 Çözüm Adımları

### 1. HTTP Poller Süreçlerinin İzlenmesi
Zabbix Server log dosyalarını kontrol ederek HTTP poller süreçlerinde herhangi bir hata veya yetersizlik olup olmadığını doğrulayın:

tail -f /var/log/zabbix/zabbix_server.log

### 2. HTTP Poller Süreçlerini Artırın
Zabbix Server'ın konfigürasyon dosyasına erişerek, HTTP poller süreçlerini artırabilirsiniz:

sudo nano /etc/zabbix/zabbix_server.conf

Değiştirilecek satır:

StartHTTPPollers=5

Bu değeri mevcut yükünüze bağlı olarak artırabilirsiniz. Örneğin:

StartHTTPPollers=10

Değişiklikleri yaptıktan sonra Zabbix Server'ı yeniden başlatın:

sudo systemctl restart zabbix-server

### 3. HTTP Kontrol Aralıklarını Optimize Edin
Zabbix'te izlenen HTTP öğelerinin kontrol aralıklarını inceleyin. Gereksiz sık kontrolleri azaltarak server üzerindeki yükü hafifletin:

Zabbix arayüzüne giriş yapın.
HTTP öğelerini inceleyin ve gereksiz olanları optimize edin.
İzleme aralığını örneğin 60 saniyeden 120 saniyeye çıkarabilirsiniz.

### 4. Kaynak Kullanımını İzleyin
Değişiklik sonrası Zabbix -> Monitoring -> Queue sekmesini inceleyerek HTTP poller süreçlerinin durumu hakkında bilgi edinin. Hataların azalması gerektiğini göreceksiniz.

🛠 Örnek Komutlar
Aşağıdaki komutları kullanarak Zabbix süreçlerini kontrol edebilirsiniz:

Aktif poller süreçlerini kontrol etmek için:

ps aux | grep zabbix | grep poller

Zabbix yapılandırma dosyasında poller süreçlerini kontrol etmek için:

grep StartHTTPPollers /etc/zabbix/zabbix_server.conf

📋 Notlar
HTTP poller süreçlerinin gereksiz yere artırılması, sistem kaynaklarının gereksiz kullanımına neden olabilir. Bu nedenle süreçleri artırmadan önce mevcut iş yükünü analiz edin.
Sorunun sürekli tekrar etmesini önlemek için HTTP kontrolleri düzenli olarak gözden geçirilmeli ve optimize edilmelidir.

👩‍💻 Katkıda Bulunun
Eğer bu dokümanı geliştirmek veya bu sorunun çözümüne dair daha fazla öneri sunmak isterseniz, katkılarınızı bekliyoruz! Yeni bir "Pull Request" açarak veya bir "Issue" bildirerek bize ulaşabilirsiniz.



[ENG]
# Zabbix HTTP Poller Processes Utilization Issue and Solution

## 📖 Problem Description
The "Utilization of HTTP poller processes over 75%" warning in Zabbix indicates that the HTTP poller processes are overloaded, and the resources allocated are insufficient. This problem occurs when Zabbix cannot handle the number of HTTP checks within the available poller processes.

Common causes of this issue:
- Insufficient number of HTTP poller processes configured.
- Rapid increase in monitored HTTP checks.
- Misconfigured monitoring intervals that unnecessarily overload the Zabbix server.

---

## 🚀 Solution Steps

### 1. Monitor HTTP Poller Processes
Check the Zabbix server log file to identify errors or insufficient poller processes:

tail -f /var/log/zabbix/zabbix_server.log


### 2. Increase HTTP Poller Processes
Modify the Zabbix server configuration file to increase the number of HTTP poller processes:

sudo nano /etc/zabbix/zabbix_server.conf

Update the following line:

StartHTTPPollers=5

Increase the value based on your system's workload, e.g.:

StartHTTPPollers=10

Restart the Zabbix server to apply the changes:

sudo systemctl restart zabbix-server

### 3. Optimize HTTP Monitoring Intervals
Review and optimize the intervals for monitored HTTP items to reduce unnecessary load:

Log in to the Zabbix interface.
Check the HTTP items and adjust any overly frequent monitoring intervals.
For example, change the interval from 60 seconds to 120 seconds for less critical checks.

### 4. Monitor Resource Utilization
After making these changes, review the performance in the Zabbix -> Monitoring -> Queue section to verify that the HTTP poller utilization has improved and errors have decreased.

🛠 Example Commands
Use the following commands to check Zabbix processes:

To check active poller processes:

ps aux | grep zabbix | grep poller

To confirm the HTTP poller configuration:

grep StartHTTPPollers /etc/zabbix/zabbix_server.conf

📋 Notes
Increasing HTTP poller processes unnecessarily can lead to inefficient resource utilization. Analyze the workload before making adjustments.
Regularly review and optimize HTTP checks to prevent the issue from recurring.

👩‍💻 Contribute
If you'd like to improve this documentation or provide additional solutions for this issue, we welcome your contributions! Feel free to open a "Pull Request" or report an "Issue."

