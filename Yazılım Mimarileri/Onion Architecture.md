
<h1 align="center">
  <br>
  Onion Architecture | Soğan Mimarisi
  <br>
</h1>
<h4 align="left">Onion Architecture, klasik bilinene N Katmanlı Mimari yapılanmasındaki karşılaşılan zorlukları ve kaygıları ele alarak bunlara çözüm sağlamayı amaçlayan ve katmanlar arası gevşek bir bağımlılık kurularak mimariyi inşa etmemizi sağlayan bir yaklaşımdır. Onion Architecture 2008 yılında Jeffrey Palermo tarafından tasarlanmıştır.</h4>

## Onion Architecture Nedir?
`Onion Architecture`, yazılım projelerinde kullanılmak üzere tasarlanmış, bağımlılıkların merkezdeki çekirdekten (core) dış katmanlara doğru olduğu, özellikle uygulamanın iş mantığını ve altyapıyı net bir şekilde ayırmayı amaçlayan, bağımlılıkların daha iyi yönetilmesini sağlayan, test edilebilir, esnek ve modüler bir mimari desendir. Bu yapı, uygulamanın çekirdeğini dış dünyadan izole ederek daha sürdürülebilir ve değiştirilebilir bir yapı oluşturur. <br>

Şimdi projelerimizde kullanacağımız Onion Architecture'ın tasarımsal açıdan nasıl çalıştığını aşağıdaki görsel üzerinden inceleyelim.

<div style="display: flex; align-items: flex-start;">
  <div style="flex: 1; margin-right: 10px;">
    <p>Görüldüğü üzere Onion Architecture’da katmanlar iç içe dairesel şekilde seyretmektedir. Görüntüsü Onion’a yani Soğan’a benzediği için bu ismi almıştır. Hatta görüntüden ziyade işlevsel açıdan her bir katmanın sadece bir içteki katmana bağımlılık göstermesi gözde soğan anatomisini canlandırdığı için bu şekilde sıfatlandırılmıştır diyebiliriz.</p>
    <p>Onion Architecture’da her katmanın daha merkezi katmanlara bağlılığı temel ilkedir. Bu durum merkezi katmanların dıştaki katmanlara bağlılık sergilememesini gerektirir. Yani bağlılık yine tek yönlüdür. Lakin bu sefer içe doğrudur. Bu da, herhangi bir katmanda yapılan değişikliğin içe doğru bir bağlayıcılığı olmadığı için merkeze doğru olan katmanları etkilemeyeceği lakin dıştaki katmanları etkileyeceği anlamına gelecektir.</p>
    <h3>Onion Architecture Katmanları</h3>
    - <a href="#domain-katmanı">Domain Entities / Domain / Core Katmanı</a> <br>
    - <a href="#openclosed-principle">Application / Repository & Service Interfaces</a> <br>
    - <a href="#liskov-substitution-principle">Persistence</a> <br>
    - <a href="#interface-segregation-principle">Infrastructure</a> <br>
    - <a href="#dependency-inversion-principle">Presentation</a>
  </div>
  <div>
    <img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*0Pg6_UsaKiiEqUV3kf2HXg.png" width="450px" height="350px" />
  </div>
</div>


## Domain Katmanı
Mimarinin merkezi katmanıdır. Tüm uygulama için olan Domain ve veritabanı entity’leri bu katmanda oluşturulur.
- `Entities` (*ORM araçları tarfından kullanılan ve veritabanındaki tabloları temsil eden sınıflardır.*)
- `Value Object` (*Kimliksiz ve immutable(değişmez) olan nesnelerdir*)
- `Enumeration` 
- `Exceptions` (*Domain için oluşturulan exception sınıflarıdır.*)

## Application Katmanı
Bu katman, Domain katmanı ile uygulamanın iş/business/service katmanı arasında bir soyutlama katmanıdır. Repository olsun, service olsun tüm arayüzler burada tanımlanır. Amaç veri erişiminde Gevşek Bağlı(Loose Coupling) bir yaklaşım sergilemektir. Domain katmanını referans eder. Gerekli arayüzlerle birlikte uygulamanın geneline hitap edecek tüm objeler bu katmanda tanımlanır.

- `Custom Exception` (*Kişiselleştirilmiş exception sınıflarıdır.*)
- `Response Object`
- `Request Parameters Object`
- `DTO Objects`
- `ViewModels Objects`
- `Interfaces(Repository, UnitOfWork)`
- `Mapping` (*CQRS tasarım kalıbı kullanılır.*)
- `Validators`

> *Onion Architecture’da Application (Repository) & Service Interfaces katmanı bir bütün olarak Application isminde nitelendirilebilmektedir. Aynı şekilde, Domain ve Application katmanlarıda bütünsel olarak Core yani çekirdek katmanı olarak nitelendirilmektedirler.*

## Persistence Katmanı
DbContext, migration ve veritabanı konfigürasyon işlemleri bu katmanda gerçekleştirilir. Ayrıca Application katmanındaki interface’ler burada implemente edilir. En dış katman olduğu için bu katmana herhangi bir katman bağımlılık göstermeyecektir.

- `DbContext`
- `Migrations`
- `Configurations`
- `Seeding`
- `Interface Implementation`

## Infrastructure Katmanı
Esasında Persistence katmanı bu katmanla bütünleşik olarak kullanılmaktadır. Genellikle sisteme eklenecek dış/external yapılanmalar bu katmanda dahil edilir. Haliyle bu katmanda diğer en dış katman olduğu için herhangi bir katman tarafından bağlılık olmamalıdır.

- `Email/Sms`
- `Notification`
- `Payment`

## Presentation Katmanı
Kullanıcının uygulama ile ileitşime geçtiği katmandır.

- `Console App`
- `Web App`
- `MVC`
- `Web API`

> *Onion Architecture, Clean Architecture uygulayabilmek için kullanılan tasarım kalıplarından biridir.*


## Onion Architecture'ın Avantajları
- Onion Architecture, uygulama katmanlarının mimarisel olarak sadece iç katmana olan bağımlılığı sayesinde `Tightly Coupling(Sıkıca Bağlanma)'ya` son vermekte ve `Loosely Coupling(Gevşek Bağlanma)'yı` sağlamaktadır.
- Sorumluluklarına göre projeyi katmanlara ayırmasından dolayı da Separation of Concerns (SoC) prensibine de uygundur. SoC yazılım geliştirmede kullanılan temel prensiplerden biridir. Bu prensip, bir yazılım sisteminin farklı bileşenlerinin veya modüllerinin, birbirlerinden bağımsız olarak ele alınabilecek farklı sorumluluk alanlarına sahip olması gerektiğini savunur.
- Katmanlar ilişkisel olarak içe doğru bağımlıdırlar. Dolayısıyla bu durum maintain etmesini kolaylaştırmaktadır.
- Birim testleri uygulamanın diğer modüllerinin etkisi olmaksızın ayrı katmanlar için oluşturulabileceğinden dolayı daha iyi test edilebilirlik sağlar.

> *Onion Architecture'da, geleneksel mimarinin aksine veri katmanı (Persistence Katmanı) en iç katman olarak değil, en dış katman olarak belirlenmiştir. Böylece uygulamada verinin nereden geldiğinden bağımsız olarak geliştirme yapılabilmektedir.*

> [Kaynak: Onion Architecture - Gençay Yıldız](https://www.gencayyildiz.com/blog/nedir-bu-onion-architecture-tam-teferruatli-inceleyelim/)