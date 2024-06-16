
<h1 align="center">
  <br>
  Caching
  <br>
</h1>

## Caching Nedir ?
**Yazılım süreçlerinde verilere daha hızlı erişebilmek için bu verilerin bellekte saklanması olayına caching denmektedir.**

> Bilgisayar sistemlerinde kullanılan bellek türlerinin hız ve kapasite farkları mevcuttur. Misal olarak, sabit disk'e nazaran RAM anlık olarak işlem yapabilecek verilerin tutulduğu ortam olduğu için haliyle verilere erişimin söz konusu olduğu durumlarda daha hızlı bir davranış sergileyecektir. 

## Caching'in Yazılıma Katkıları Nelerdir ?

1. **Veri Erişimini Hızlandırır**
   - Caching, veri erişimini hızlandırır.

2. **Performans Artışı**
   - Özellikle veritabanı sorguları gibi yavaş ve maliyetli işlemlerde, verilerin önceden saklandığı cache'den alınması büyük performans farkları yaratabilir.

3. **Sunucu Yükünü Azaltır**
   - Caching, verileri önceden cache'de sakladığı için ihtiyaç dahilinde aynı verilerin tekrar tekrar elde edilme maliyetini sunucudan soyutlar ve böylece sunucunun iş yükünü  azaltır.

4. **Çevrimiçi Uygulamalar için Kritik Arz Eder**
   - Çevrimiçi uygulamalarda, kullanıcıların verilere hızlı bir şekildxe erişebilmeleri ve işlem yapabilmeleri önemlidir. Caching özellikle bu ihtiyacı karşılayan bir yaklaşımdır.

## Ne Tarz Veriler Cache'lenir ?
Cache'lenecek veriler, sıklıkla ve hızlı bir şekilde erişilecek veriler olmalıdır. Örneğin; sık ve sürekli kullanılan veritabanı sorguları neticesindeki veriler, konfigurasyon verileri, menü bilgileri, yetkiler vs, gibi yazılım tarafından sürekli ihtiyaç duyulacak verileri cache'lemekte fayda vardır.

Hatta resim ve video dosyaları gibi static yapılanmalarda cache'lenebilir.

> Ancak unutulmamalıdır ki, yazılım sürecinde kullanılan her veri cache'lenmemelidir! Misal olarak, sürekli güncellenen veya kişisel olan veriler cache'lenmemelidir. Ayrıca güvenlik açısından risk teşkil eden veriler de mümkün mertebe cache'lenmeksizin işlenmelidir. 
>
> **Cache'lenmeyecek verileri özetlersek eğer;**
> - Güncellenen veriler
> - Kişisel veriler
> - Güvenlik açısından risk teşkil eden veriler
> - Özel veriler
> - Geçici veriler <br>



## Bir Cache Mekanizmasının Temel Bileşenleri Nelerdir ?
Bir cache mekanizmasının temel bileşenleri; <strong>cache belleği, cache bellek yönetimi, ve cache algoritmasıdır.</strong>

- **Cache Belleği**
   - Verilerin saklandığı bellektir. Verileri hızlı bir şekilde erişilebilir hale getirmek için kullanılır.

- **Cache Bellek Yönetimi**
   - Cache belleğinde saklanan verileri yönetmek için kullanılır. Misal olarak; verilerin saklanma süreleri, silinme sıklıkları yahut güncellik durumları gibi yapılandırmalar sağlanabilir.

- **Cache Algoritması**
    - Verilerin cache belleğine nasıl eklenip silineceğini belirleyen algoritmadır.

## Caching Yaklaşımları Nelerdir?
Cache uygulamak için **In-Memory Caching** ve **Distributed Caching** olmak üzere iki farklı yaklaşım söz konusudur.

- **In-Memory Caching**
    - Verilerin uygulamanın çalıştığı bilgisayarın RAM'inde cache'leyen yaklaşımdır.

- **Distributed Caching**
    - Verileri birden fazla fiziksel makinede cache'leyen ve böylece verileri farklı noktalarda tutarak tek bir noktada saklamaktan daha güvenli bir davranış sergileyen yaklaşımdır. Bu yaklaşımla veriler bölünerek farklı makinelere dağıtılmaktadır. Haliyle büyük veri setleri için daha uygun ve ideal bir yaklaşımdır.

## Distributed Caching Yapıları Nelerdir ?

- **Redis**
    - Redis(Remote Dictionary Server); open source olan ve bellekte veri yapılarını yüksek performanslı bir şekilde cache'lemek için kullanılan bir veritabanıdır. Caching işlemlerinin yanında message broker olarak da kullanılabilmektedir. Yapısal olarak key-value veri modelinde çalışmaktadır ve NoSQL veritabanıdır.

- **Memcached**
    - Open source, key-value veri modelinde caching yazılımıdır.

- **Hazelcast**
    - Open source, key-value veri modelinde caching işlemleri yapan, Java tabanlı bir yazılımdır.

- **Apache Ignite**
    - Open source, key-value veri modelince caching yazılımıdır.

- **EHCache**
    - Open source, key-value veri modelinde caching işlemleri yapan, Java tabanlı bir yazılımdır.        
