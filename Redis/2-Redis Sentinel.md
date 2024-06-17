<h1 align="center">
  <br>
  Redis Sentinel
  <br>
</h1>

<p>Redis, her ne kadar cache amacıyla kullandığımız bir veritabanı olsa da yoğun operasyonların söz konusu olduğu mimarisel tasarımlarda kesintisiz hizmet verebilme ihtiyacı hissedilebilmekte ve bu ihtiyaca karşın ölçeklendirme yaklaşımları sergilenebilmektedir.</p>

<strong>Redis Sentinel yapılanması, Redis veritabanı için yüksek kullanılabilirlik sağlamak amacıyla geliştirilmiş yönetim servisidir diyebiliriz.</strong>

## Redis Sentinel'i Hangi Durumlarda Kullanırız
- **Redis sunucusunun arızlanması durumunda**
    - Redis sunucusu arızalandığı taktirde Redis Sentinel servisi ile farklı bir sunucu üzerinden Redis çalışmalarına devam edebilir ve böylece kesintisiz hizmet vermeyi sürdürebiliriz.

- **Bakım ve güncelleme süreçlerinde**    
    - Bakım ve güncelleme süreçlerinde Redis sunucusunun geçici olarak çalışmaz hale gelmesi durumunda Sentinel ile farklı bir sunucu üzerinden hizmetin kesintisiz verilmesi sağlanabilir.

- **Yüksek trafik**
    - Yüksek trafiğin olduğu durumlarda Redis sunucusunun performansı yetmeyebilir ve Redis gelen taleplere gecikmeli sonuçlar dönebilir. Böyle durumlarda Sentinel ile daha performanslı çalışmalar gerçekleştirilebilir.    

- **Yedekleme ve geri yükleme**    
    - Sentinel servisi ile yedekleme ve geri yükleme süreçleri sorunsuz bir şekilde tamamlanması sağlanabilir.

## Redis Sentinel Yapısının Temel Kavramları Nelerdir ?
Redis Sentinel, master/slave replikasyon sistemi üzerine çalışan bir yönetim servisidir. Sentinel, Redis veritabanının sağlığını izler ve herhangi bir problem/kesinti vs. meydana geldiği taktirde otomatik olarak failover(yük devretme) işlemlerini gerçekleştirerek farklı bir sunucu üzerinden Redis hizmetinin kaldığı yerden devam etmesini sağlar. 

>Redis Sentinel'de; **Master, Slave, Sentinel ve Failover** olmak üzere dört kritik kavram vardır.

### Master
<hr>
Redis veritabanının ana sunucusudur. Tüm yazma ve okuma işlemleri bu sunucu üzerinde gerçekleşir. <br>
Yani o anda aktif olan Redis sunucusunun rolünü ifade eder. Bu ana bilgisayar, diğer yedek Redis bilgisayarından(slave) daha öncelikli konumdadır ve bundan dolayı veri yazma ve okuma işlemleri için kullanılır.<br>
Sentinel ise master olan Redis sunucusunun sağlıklı olup olmadığını sürekli olarak izleyecek ve sorun olduğu taktirde başka bir yedek Redis sunucusunu otomatik master olarak işaretleyecektir.

### Slave
<hr>
Redis veritabanının yedek sunucularını ifade eder. Master sunucunun verilerinin replikasyonunu alır ve biryandan da okuma işlemi için kullanılabilir. Yani slave için Redis master sunucusunun yedeklenmiş bir kopyasıdır diyebiliriz.<br>
Redis sentinel yapılanmasının uygulandığı bir mimaride, herhangi bir t zamanda 'master' sunucu yalnızca bir tane olurken slave ise birden fazla olabilir.

### Sentinel
<hr>
Redis veritabanının sağlığını izleyen ve otomatik failover işlemlerini gerçekleştiren bir yönetim servisidir. <br>
Sentinel, Redis veritabanın yüksek kullanabilirliğini sağlamak ve herhangi bir kesintiye mahal vermeksizin sürdürülebilir kılmak için otomatik olarak çalışmakta ve Redis master sunucusunun sağlıklı olup olmadığını sürekli olarak gözlemlemektedir. Master sunucusunda bir problem ya da kesinti meydana geldiği taktirde sentinel sunucu yedek(slave) Redis sunuculardan birinin yükseltilmesi ve master yapılması işleminden sorumludur.<br>
Ayrıca Redis Sentinel, sisteme eklenen tüm slave sunucular hakkında bilgi toplamakta ve aralarından bir master seçmektedir. <br><br>

> Sentinel sunucusu, Redis Sentinel yapılanmasının merkezi bileşenidir. 

### Failover
<hr>
Master sunucusunun arızalanması durumunda Sentinel tarafından herhangi bir slave'in master olarak atanması işleminin terminolojik karşılığıdır. <br>
Ya da bir başka deyişle herhangi bir slave'in mevcut master yerine geçip master olmasına 'failover' denmektedir. <br>
Sentinel sunucusu, failover işlemi gerçekleştirdiği taktirde yeni master'ın IP değerini diğer slave'lere ileterek tüm sunucuların senkronize olmasını sağlamaktadır. <br><br>

> Failover işlemi sonrası mevcut master'da slave konumuna geçmektedir.

## Özet
- Redis Sentinel, Redis veritabanının master sunucusu düşmesi durumunda başka bir yedek sunucunun otomatik olarak yerine geçmesini ve veri hizmetlerinin kesintisiz devam etmesini sağlamaktadır.
- Sentinel, master sunucusunun durumunu izlemek ve değişikliklerini algılamak için diğer sentinel sunucularıyla birlikte çalışmaktadır.
- Sentinel mimarisinde birkaç sentinel sunucusuyla çalışılması önerilmektedir. Bu sentinel sunucularının da kesintisiz görevini yapmasını garanti haline getirecektir.