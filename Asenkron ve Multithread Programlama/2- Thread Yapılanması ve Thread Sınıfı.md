
<h1 align="center">
  <br>
  Thread Yapılanması ve Thread Sınıfı
  <br>
</h1>

## Thread Sınıfının Temellerine Giriş
**C# dilinde, multithread programlama, bir programın aynı anda birden fazla thread tarafından yürütülmesini sağlayan yaklaşımdır** <br> <br>
Thread ise bir işlem içinde bağımsız olarak çalışabilen en küçük yürütme birimidir. Bir program çalışırken öncelikle **main thread**  olarak adlandırılan bir thread bulunur. Main thread'den sonra ek olarak yardımcı thred'ler oluşturulabilir ve bunlara **worker thread** denmektedir. <br> <br>
İşte bizler bu worker thred'ler arasında paralel ve eş zamanlı çalışmalar sağlayabilir ve multithread yaklaşımını sergileyebiliriz. C#'ta multithread yaklaşımını sergileyebilmek için **System.Threading** namespace'i altında **Thread** sınıfı sunulmuştur. Bizler bu sınıf ile main thread'in dışında, yeni thread'ler oluşturabilir ve kontrol edebiliriz.

```csharp
class Program
{
    static void Main(string[] args)
    {
        for (int i = 0; i < 999; i++)
        {
            Console.WriteLine($"Main Thread {i}");
        }

        Thread thread = new (() =>
        {
            for (int i = 0; i < 999; i++)
            {
                Console.WriteLine($"Worker Thread {i}");
            }
        });

        thread.Start();
    }
}
```

Yukarıda görüldüğü üzerine Main fonksiyonu içerisinde yaptığımız işlemlerimiz **Main Thread** olarak adlandırılır, kendimiz oluşturduğumuz Thread'ler ise worker thread olarak tanımlanır. Bir worker thread oluşturduktan sonra **Start** metodu ile çağırılarak başlatılmalıdır.


### Thread Id <hr>
C#'ta oluşturulan her bir thread esasında arkaplanda bir kimlikle ilişkilendirilir. Bizler bu kimliği kullanarak trace ve debug işlemlerini daha rahat yürütebilmekte, thread'ler arası hedefsel haberleşmeyi dağlayabilmekte ve kaynak yönetimi gibi türlü işlemleri gerçekleştirebilmekteyiz. <br>
Thread'lerin id değerlerine erişebilmek için aşağıdaki yöntemlerden birini kullanabiliriz.

```csharp
System.Environment.CurrentManagedThreadId;
Thread.CurrentThread.ManagedThreadId;
```

### IsBackground Property'si <hr>
IsBackgorund property'si ile bir thread'in arkaplanda çalışıp çalışnmayacağı belirlenebilir. Ve arkaplanda çalışacak olan bir thread main thred'e bağlı bir şekilde davranışını sürdürecektir. Yani main thred sona erdiğinde arkaplandaki thread de otomatik sonlandırılacaktır. Bu demektir ki, arkaplanda çalışmayan bir thread(foreground thread) ise main thread sona erse bile devam edecektir. <br>

```csharp
 Thread thread = new(() =>
 {
    
 });
 thread.IsBackground = false;
 thread.Start();
```

Main thread, worker thread bitene kadar bekler. Eğer ki bu thread tamamlanmazsa uygulama sonlanmaz! <br>
Yok eğer true değer verilmiş olsaydı o taktirde de main thread, worker thread'i beklemeyeceği için sonlandığı an worker thread'de sonlanıyor olacaktı.

### Thread State'i <hr>
Oluşturulan thread'ler, mevcut durumlarını ifade etmek için State bilgisi barındırmaktadırlar. Bu bilgi ThreadState türündedir ve bir thread'in şu anda hangi durumda olduğunu belirten bir state verisidir. ThreadState aşağıdaki değerlere sahiptir;


- **Running** => Thread'in çalıştığını ifade eder.
- **StopRequested** => Thread'in durdurulması istenmiştir.
- **SuspendRequested** => Thread'in askıya alınması istenmiştir.
- **Background** => Arkaplanda çalışan thread'i ifade eder.
- **Unstarted** => Thread henüz başlatılmamıştır.
- **Stopped** => Thread sonlandırılmıştır.
- **WaitSleepJoin** => Thread ya başka bir thread'i beklemekte veya uykudadır.
- **Suspebded** => Thread askıda bekletilmektedir.
- **AbortRequested** => Thread'in sonlandırılması talep edilmiştir.
- **Aborted** => Thread aniden sonlandırılmıştır.






<!-- ## Asenkron ve Senkron Nedir ?
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

> Bu farklara bakıldığında Task sınıfı Thred'e nazaran daha modern'dir ve kullanım açısından da (özellikle asenkron programlamada) kolay bir yaklaşım sağlamaktadır. Ancak bu özellikle multithread programlama durumlarında Thread sınıfının daha fazla kontrol ve esneklik sağladığı gerçeğini inkar etmek anlamına gelmemektedir. -->

