# Zabbix-Http-Poller
Zabbix Http Poller 
[TR]
Zabbix İçin HTTP Poller Süreçlerini Optimize Etme

Amaç:
Zabbix sunucusunda karşılaşılan "Utilization of HTTP poller processes over 75%" uyarısı, HTTP poller süreçlerinin yoğun bir şekilde kullanıldığını gösterir. Bu rehberde, HTTP poller süreçlerini artırma adımları anlatılmaktadır.

HTTP Poller Süreçlerini Artırma

HTTP poller süreçlerini artırarak, Zabbix sunucunuzun HTTP tabanlı talepleri daha verimli bir şekilde işlemesini sağlayabilirsiniz.

Adımlar:

Zabbix Sunucu Yapılandırma Dosyasını Açın:
Aşağıdaki komutu kullanarak zabbix_server.conf dosyasını düzenlemek üzere açın:

sudo nano /etc/zabbix/zabbix_server.conf

StartHTTPPollers Parametresini Bulun veya Ekleyin:
Dosyada StartHTTPPollers satırını bulun. Eğer mevcut değilse, dosyaya aşağıdaki satırı ekleyin:

StartHTTPPollers=10

Varsayılan değer genellikle 5tir. Trafik yoğunluğuna göre bu değeri 10 veya daha yüksek bir sayı yapabilirsiniz.

Zabbix Sunucusunu Yeniden Başlatın:
Değişikliklerin etkin olması için Zabbix sunucusunu yeniden başlatın:

sudo systemctl restart zabbix-server

Değişikliklerin Etkisini Kontrol Edin:
HTTP poller süreçlerinin durumu ve kullanım oranını izlemek için Zabbix web arayüzünde şu yolu izleyin:

Monitoring > Processes > HTTP poller


[ENG]
Increasing HTTP Poller Processes

By increasing the number of HTTP poller processes, you can ensure your Zabbix server handles HTTP requests more effectively.

Steps:

Open the Zabbix Server Configuration File:
Use the following command to edit the zabbix_server.conf file:

sudo nano /etc/zabbix/zabbix_server.conf

Locate or Add the StartHTTPPollers Parameter:
Find the line containing StartHTTPPollers. If it does not exist, add the following line to the file:

StartHTTPPollers=10

The default value is typically 5. Depending on your traffic load, you can set it to 10 or a higher value.

Restart the Zabbix Server:
Restart the Zabbix server to apply the changes:

sudo systemctl restart zabbix-server

Verify the Changes:
To monitor the status and utilization of HTTP poller processes, navigate to the following in the Zabbix web interface:

Monitoring > Processes > HTTP poller
