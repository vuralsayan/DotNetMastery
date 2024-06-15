
<h1 align="center">
  <br>
  SOLID Prensipleri
  <br>
</h1>
<h4 align="left">Yazılım prensipleri; durumuna göre en ideal davranışları ortaya koymanı sağlayan genel kodlama ahlakını sağlar.</h4>
<p align="left">SOLID prensiplerini anlamadan önce bilmemiz gereken iki tane kavram vardır bunlar <strong>Tight Coupling(Sıkı Bağlantı)</strong> ve  <strong>Loose Coupling (Gevşek Bağlantı)</strong> konularıdır.</p> 

## Tight Coupling Nedir?
Tight Coupling, bir sınıfın veya modülün başka bir sınıfa veya modüle doğrudan bağımlı olması durumudur. Bu tür bağlantı, yazılımın esnekliğini ve sürdürülebilirliğini azaltır. Sıkı bağlı bileşenler arasında değişiklik yapmak zordur, çünkü bir bileşende yapılan bir değişiklik, diğer bağlı bileşenlerde de değişiklik yapılmasını gerektirebilir.<br>
Basit bir örnek vermek gerekirse, günlük hayatımızda sürekli karşılaştığımız Otomobil ve Sürücü ikilisi üzerinden örnek verebiliriz.

## Loose Coupling Nedir?
Loose Coupling, sınıfların veya modüllerin birbirlerine minimum düzeyde bağımlı olması durumudur. Bu tür bağlantı, yazılımın esnekliğini ve sürdürülebilirliğini artırır. Gevşek bağlı bileşenler arasında değişiklik yapmak daha kolaydır ve bileşenler daha bağımsız bir şekilde çalışabilir. Sıkı bağımlılıkların azaltılması için interfaceler ya da abstract sınıflar kullanılır. Bu sayede sürücü tek bir araç kullanmak yerine birden çok araç kullanabilir hale gelmektedir. 

<h3>SOLID Konu Başlıkları</h3>
- <a href="#single-responsibility-principle">Single Responsibility​ Principle</a> <br>
- <a href="#openclosed-principle">Open/Closed Principle</a> <br>
- <a href="#liskov-substitution-principle">Liskov Substitution Principle</a> <br>
- <a href="#interface-segregation-principle">Interface Segregation Principle</a>


## Single Responsibility​ Principle
Single Responsibility Principle, OOP tasarımlarında bir sınıfı mümkün mertebe tek bir sorumluluğa odaklı inşa edilmesi gerektiğini ilke olarak savunan bir prensiptir. <br>
Bir sınıfın, değiştirilmesi gereken birden fazla sebebi veya gerekçesi varsa işte bu durum ilgili sınıfın birden fazla sorumluluğu olduğu anlamına gelmektedir. <br> <br>
Yani SRP nin asıl savunduğu prensip  <strong>"Bir sınıfın değişmesi için yalnızca tek bir nedeni olması gerekmektedir."</strong> cümlesidir. <br><br>
Bir sınıf veya metot, işlevsel olarak birden fazla işi/operasyonu yürütüyorsa yani bir başka deyişle birden fazla sorumluluğu varsa bu istenmeyen bir durumdur. Günlük hayatta bir insan aynı anda birden fazla iş yükünü nasıl kaldıramıyorsa, kaldırmaya çalışssa da beklenen verim alınamıyorsa, ürettiğimiz kodlarımızda da birden fazla sorumluluğun tek bir yapıda toplanması doğru bir çalışma olmayacaktır. Ayrıca her yeni yapılanma için yeniden test ve bakım maliyetleri de haddinden fazla artacaktır.

## Open/Closed Principle 
Open Closed Principle, OOP tasarımlarında bir sınıfın gereksinimler doğrultusunda değiştirmeye gerek duyulmaksızın, genişletilebilir bir şekilde tasarlanmasını savunan bir prensiptir. <br>
<strong>Bir kod; genişletilmeye açık, değişime kapalı olduğu taktirde ideal koddur!</strong> <br> 

Open Closed Principle koda <strong> sürdürülebilirlik, genişletilebilirlik, yeniden kullanılabilirlik ve esneklik</strong> kazandırır. Böylece kodun gelen yeni gereksinimlere göre değişiklik direncini kıracak ve geliştiriciyi bu değişiklik süreçlerindeki maliyetlerin getirdği yığınlardan soyutlayacaktır.

## Liskov Substitution Principle
Liskov Substitution Principle, ortak bir referanstan türeyen nesnelerin hiçbir şeyi bozulmadan birbirleriyle değiştirilebilmesi gerektiğini yani birbirlerinin yerine geçebilmesi gerektiğini öneren bir prensiptir. 

Eğer bir sınıf, herhangi bir interface yahut abstract class ile sözleşme yapıyorsa o zaman bu sözleşmeyi karşılamalı ve gerekli tüm memberları içerisinde tanımlamalıdır. Lakin bu memberlardan boş ve işlevsiz olanlar varsa işte orada bir problem var demektir. <br>
Hiçbir alt sınıf uygulamış olduğu base class'ın metotlarını ihlal etmemelidir. Yani implement yahut override edilen hiçbir metot boş kalmamalı veya boş kalmasın diye Not Implemented Exception gibi hatalar döndürülmemelidir.

Yani LPS bize şunu söylemektedir; <strong>Ortak referanstan türeyen nesneler herhangi bir davranış değişikliğine gerek duyulmaksızın birbirlerinin yerine geçebilmelidirler.</strong>

## Interface Segregation Principle
Interface Segregation Principle, <strong>bir nesnenin yapması gereken her farklı davranışların, odavranışlara odaklanmış özel interface'ler ile eşleşmesini öneren prensiptir.</strong> <br> Böylece ihtiyaç olan davranışları temsil eden interface'ler eşliğinde ilgili sınıflara kazandırabilir ve hiçbir sınıfın kullanmadığı bir imzayı zorla implement etmek zorunda kalmaksızın inşa sürecine devam edebiliriz. 

Sınıflara ihtiyaç duymadıkları imzaları arayüzlerle zorlayarak işlevsiz metotlar eklemek ISP'ı ihlal etmek demektir. Yazılımdaki davranışları tek bir bütün olarak tutmaktansa, birbirlerinden bağımsız olacak şekilde birden çok parçaya bölmek ideal kod yapısını ortaya çıkarır.

ISP ihlali, doğrudan LSP ve SRP'ın da ihlaline sebebiyet vermektedir. <br>
ISP sınıf tarafından desteklenmeyecek metotların lüzumsuz yere tanımlanmamasına karşı odaklanırken, LSP ise benzer şekilde bu tarz işlevsiz metotların barındırıldığı sınıflardan olan nesnelerin kendi aralarında olan değişimleri sürecinde patlama ya da boşa çıkma riskini ortadan kaldırmaya odaklanmaktadır. <br>
SRP'da ise sınıfların değişmesi için yalnızca tek bir nedenin olması gerektiği söylenirken, ISP'de de hacmi büyük arayüzler yüzünden implemente edilmiş alakasız yöntemlerin değiştirilmesi gibi durumlarda ilgili sınıfta değişiklik gerekeceğinden, dolaylı yoldan sınıfların sadece tek bir değişim nedeni olmas desteklenmektedir.