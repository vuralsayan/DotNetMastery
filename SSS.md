
<h1 align="center">
  <br>
  Sıkça Sorulan Sorular
  <br>
</h1>

<h4 align="center">.Net Core Alanında Sıkça Sorulan Önemli Konular </h4>

## Dependency Injection Nedir?
Dependency Injection (Bağımlılık Enjeksiyonu) konusunu özetlemek gerekirse; <strong>bağımlılık oluşturacak parçaların ayrılıp bunların dışardan verilmesiyle sistem içerisindeki bağımlılığı minimize etme işlemidir.</strong> <br>
Temel olarak oluşturacağımız bir sınıf içerisinde başka bir sınıfın nesnesini kullanacaksanız <i>new</i> anahtar sözcüğüyle oluşturmamanız gerektiğini söyleyen bir yaklaşımdır. Gereken nesnenin ya Constructor'dan ya da Setter metoduyla parametre olarak alınması gerektiğini vurgulamaktadır. Böylece iki sınıfı birbirinden izole etmiş olduğumuzu savunmaktadır.

Yazılımı oluşturan kaçınılmaz olarak birbirleri ile ilişkilidir. Lakin bu ilişkinin bir bağa ve sınırlandırmaya sebep olmaması için mümkün mertebe ilişkiyi gevşek tutmak önemlidir. Biz buna Loosely Coupled yani Gevşek Bağlılık diyoruz. 


## DI Containers Nedir?

DI Containers, Dependency Injection (Bağımlılık Enjeksiyonu) işlemini yönetmek ve kolaylaştırmak için kullanılan yazılım bileşenleridir. Bu konteynerler, uygulamanın bağımlılıklarını yönetir ve ilgili bileşenleri birbirine enjekte eder. Bu sayede kod daha modüler, test edilebilir ve yönetilebilir hale gelir. .Net Core ile birlikte kullanılan bazı yaygın DI konteynerlerine göz atalım:

### Temel Kavramlar

1. **Dependency Injection (DI)**:
   - Bir sınıfın bağımlılıklarının, sınıfın içine değil dışarıdan sağlanması işlemidir.
   - DI, kontrolün tersine çevrilmesi (IoC - Inversion of Control) prensibinin bir uygulamasıdır.

2. **DI Container**:
   - Bağımlılıkları otomatik olarak çözümlemek ve enjekte etmek için kullanılan bir yapı.
   - Genellikle servislerin ömür sürelerini (Lifetime) yönetir: Transient, Scoped, Singleton.

### DI Container Kullanımının Avantajları

1. **Modülerlik ve Esneklik**:
   - Kodun daha modüler ve esnek olmasını sağlar.
   - Bağımlılıkları değiştirirken kodda minimum değişiklik yapma imkanı sunar.

2. **Test Edilebilirlik**:
   - Bağımlılıkların kolayca mock'lanabilmesi sayesinde birim testlerini yazmak daha kolay hale gelir.

3. **Bakım Kolaylığı**:
   - Bağımlılıkların merkezi bir yerden yönetilmesi kodun daha okunabilir ve bakımı kolay olmasını sağlar.

### .Net Core'da DI Container

.Net Core, yerleşik bir Dependency Injection Container ile gelir. Bu, uygulama başlangıcında yapılandırılır ve bağımlılıkları yönetir. Aşağıda .Net Core'da DI Container kullanımına dair temel bir örnek bulunmakta:

1. **Servis Arayüzü ve Uygulaması**:
```csharp
public interface IGreetingService
{
    string Greet(string name);
}

public class GreetingService : IGreetingService
{
    public string Greet(string name)
    {
        return $"Hello, {name}!";
    }
}
```

2. **Startup.cs Dosyasında Bağımlılık Kayıtları**:
```csharp
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        // IGreetingService servisini kayıt ediyoruz.
        services.AddTransient<IGreetingService, GreetingService>();
    }

    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        // ... diğer yapılandırmalar ...
    }
}
```

3. **Servisin Kullanımı**:
```csharp
public class HomeController : Controller
{
    private readonly IGreetingService _greetingService;

    public HomeController(IGreetingService greetingService)
    {
        _greetingService = greetingService;
    }

    public IActionResult Index()
    {
        var message = _greetingService.Greet("World");
        return Content(message);
    }
}
```

### DI Container Türleri ve Ömür Süreleri

.Net Core'da servislerin yaşam süreleri üç ana türde tanımlanır:

1. **Transient**:
   - Her istek yapıldığında yeni bir örnek oluşturulur.
   - Kısa ömürlü ve hafif bağımlılıklar için kullanılır.

2. **Scoped**:
   - Her istek başına bir örnek oluşturulur.
   - Web uygulamalarında her HTTP isteği için bir örnek anlamına gelir.

3. **Singleton**:
   - Uygulama yaşam döngüsü boyunca tek bir örnek oluşturulur.
   - Ağır ve nadiren değişen bağımlılıklar için kullanılır.

### Kayıt Örnekleri

```csharp
services.AddTransient<ITransientService, TransientService>();
services.AddScoped<IScopedService, ScopedService>();
services.AddSingleton<ISingletonService, SingletonService>();
```
