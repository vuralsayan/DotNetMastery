
<h1 align="center">
  <br>
  Asenkron & Multithread Programlama ve Temel Kavramlar
  <br>
</h1>

## Thread Nedir ?
**Thread'ler metotlar gibi program parçacıklarıdır. Yani delegate yapılanmasıyla tanımlamasını gerçekleştirdiğimiz parametreli ya da parametresiz metotlardır.**

> Bir program parçacıkları sadece belli bir görevi yerine getirdikten sonra işini bitirebildikleri gibi programınızın çalıştığı süre boyunca sürekli çalışarak belli başlı gçrevleri aralıksız yerine getirebilirler. 

> Bir yazılımın oluşturulması sürecinde ilk iş olarak thread oluşturulur. Biz buna ana thread deriz. Ana thread, programın akışını kontrol ederken, eş zamanlı olarak diğer thread'lerin de çalışmasını sağlamaktadır. 

Thread'i anlamak için öncelikle thread'ın çalıştığı yerin sınırlarını anlamalıyız. Bir bilgisayar programı, biligsayarın belleğine yüklendiği ve yürütülmeye başlandığında process(işlem) haline gelir. Bir process, bir veya birden fazla işlemci tarafından işlenebilir. <br>
Thread ise process içinde yürütülen talimatların dizisidir. Bir işletim sistemi içinde çalışan temel yürütme birimine thread yani iş parçacığı denir.

> Thread'ler kod akışındaki metot çağrımları, döngüler vs. gibi aksiyonlardan etkilenen yazılımsal birimlerdir. 

## Asenkron ve Senkron Nedir ?
**Asenkron ve senkron terimleri, programlama bağlamında işlemlerin zamanlama ve gerçekleşme şekillerini ifade eden kavramlardır.**

### Asenkron Nedir ?
<strong>Asenkron;</strong> bir işlemin başlatılmasıyla sonra ermesi arasında bir bağımlılığın olmadığı veya bu bağımlılığın zayıf olduğu durumu ifade etmektedir. Haliyle asenkron işlemlerde bir işlem sürerken diğer işlemlerin de bekletilmeksizin devam etmesine olanak tanımaktadır.

### Senkron Nedir ?
<strong>Senkron</strong> ise bir işlemin başlamasının bir önceki işlemin tamamlanmasına bağlı olduğu durumu ifade etmektedir. Aynı anda birden fazla işlem sürememekte, herhangi bir T zamanında sade ve sadece tek bir işlem gerçekleştirilebilmektedir.

## Asenkron ve Multithread Programlama Nedir ?
- **Asenkron Programlama**
    - Asenkron programlama, kod akış sürecinde işlemlerin birbirlerinden bağımsız olarak çalıştığı bir modeldir. Bir işlemin başlaması için farklı bir işlemin bitmesini beklemeye lüzum olmaması durumudur.
    - Asenkron programlama bir ya da birden fazla thread'le uygulanabilmektedir ve temel amacı kodun çalıştığı thread'i bloklatmaksızın si,sitemin işleyişini devam ettirmektedir.  
    - Düşük bellek kullanımı söz konusudur.
    - Kod akışları birbirlerinden bağımsız seyredeceği için eşzamanlılık problemleri yok denecek kadar azdır.
    - Web uygulamalarında, IO operasyonlarında yahut event-driven sistemlerde performans açısından oldukça etkilidir.
    - İşlemlerin birbirlerinden bağımsız olmasından dolayı debug süreci daha kolaydır.

- **Multithread Programlama**
    - Multithread programlamada ise kod akışını birden fazla thread üzerinden seyrettiği bir modeldir. Bu threadler aynı bellek alanını paylaşabilir ve birbirleriyle iletişimde bulunabilirler. 
    - Örnek olarak; 5 adet PDF dosyasının işleneceğini varsayarsak, bunların her birinin işlenmesi 10 saniye olsa, senkron davranışla totalde 5 x 10 = 50 saniyede bu işlemi halletmiş oluruz. Eğer ki multithread programlama ile işlersek her PDF dosyasını ayrı bir thread'e alarak ortalama 10 saniyede tüm işlemleri tamamlamış oluruz.
    - Her thread ayrı bir bellek ihtiyacı duyacaktır. Bundan dolayı bellek kullanımı açısından daha maliyetlidir.
    - Birden çok thread, aynı anda paylaşılan kaynaklara erişebileceğinden dolayı eşzamanlılık sorunları ister istemez söz konu olabilmektedir.
    - Çoklu işlemci sistemlerinde veya yoğun hesaplama gerektiren işlemlerde performans avantajı sağlayabilir.
    - Eşzamanlılık problemleri nedeniyle debug süreçleri karmaşık olabilmektedir.

    
> Sonuç olarak asenkron programlama ile multithread programlama aynı şey değildir. Asenkron programlama da amaç ana thred'i bloklamadan çalışma yürütmekken, multithread programlama da ise yapılacak operasyonların birden fazla thread üzerinde eş zamanlı olarak işlenmesidir.

## Task ile Thread Sınfıları Arasındaki Farklar Nedir ?
- **Task Sınıfı**
    - Task sınıfı, Task Parallel Library(TPL) içinde yer almakta ve yüksek seviyeli bir abstraction sağlayarak işlemler yürütmektedir. Paralel programlama ve asenkron operasyonlar için tasarlanmıştır. Kod yazımında async ve await keyword'lerini kullanarak asenkron programlamayı oldukça kolaylaştırmaktadır.
    - Task sınıfı, thread'leri .NET tarafından yönetilen bir thread pool'da çalıştırabilmektedir ve .NET'teki garbage collector gibi mekanizmaların avantajlarından yararlanabilir.
    - Task sınıfı, TPL aracılığıyla eşzamanlılık ve paralellik sağlamaktadır. Birden fazla işlemi eşzamanlı olarak yönetir ve paralel olarak çalıştırabilir.
    - Task sınıfında bekleme **async** ve **await** keyword'leri sayesinde oldukça kolaydır. **WhenAll**, **WhenAny** vs. gibi metotlar sayesinde de birden fazla görevin tamamlanmasını beklemek ve bunları yönetmekte süreci pek kolay kılmaktadır.

- **Thread Sınıfı**
    - Thread sınıfı, Task'a nazaran daha düşük seviyede bir abstraction sağlamakta ve doğrudan thread oluşturmayı ve yönetmeyi amaçlamaktadır. multithread programlamanın doğrudan uygulanmasını sağlamaktadır. Task'a nazaran daha fazla sorumluluk ve dikkat gerektirmektedir.
    - Thread sınıfı, thread'i doğrudan işletim sistemi tarafından oluşturulan bir iş parçacığında çalıştırır. Bu, .NET dışındaki yönetilmeyen kaynaklara daha fazla maruz kalmayı içerebilmekte ve daha fazla durumu söz konusu olabilmektedir.
    - Thread sınıfı, genellikle doğrudan iş parçacığı oluşturarak paralel işlemleri gerçekleştirmeyi amaçlar. 
    - Thread sınıfı, thread'in tamamlanmasını beklemek için genellikle daha düşük seviyeli bir bekleme mekanizması olan **Join** metodunu kullanır.

> Bu farklara bakıldığında Task sınıfı Thred'e nazaran daha modern'dir ve kullanım açısından da (özellikle asenkron programlamada) kolay bir yaklaşım sağlamaktadır. Ancak bu özellikle multithread programlama durumlarında Thread sınıfının daha fazla kontrol ve esneklik sağladığı gerçeğini inkar etmek anlamına gelmemektedir.

