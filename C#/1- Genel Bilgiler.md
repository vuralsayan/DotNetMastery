
<h1 align="center">
  <br>
    C# Genel Bilgiler
  <br>
</h1>

## C# Nedir ?
- C#, Microsoft tarafından .NET çatısı altında geliştirilen ve gelişen modern programlama dilidir.
- Açık kaynak ve ücretsizdir.
- OOp'yi ve OOP'nin gelişimini destekleyen orta seviyeli bir dildir.


## .NET Nedir ?
- .NET Microsoft'un developerlar için geliştirdiği teknolojileri sunduğu bir çatıdır.
- .NET Framework windows ekosistemine yönelik çalışmalar için kullanılır.
- .NET Core ise cross platform'dur. Çeşitli işletim sistemindeki uygulamaları destekler (Windows, MACOS, Linux).

## Erişim Belirleyici (Access Modifier) Nedir ?
Erişim belirleyici (access modifier), bir sınıfın, metodun veya değişkenin erişim seviyesini belirleyen bir anahtar kelimedir. Erişim belirleyicileri, bir programın farklı bölümleri arasındaki erişim düzeylerini kontrol ederek, kodun daha güvenli ve düzenli olmasını sağlar. <br>

C# dilinde kullanılan erişim belirleyiciler ve anlamları şunlardır:

### 1. `public`
- **Açıklama**: Her yerden erişilebilir.
- **Özellikler**: Bu belirleyiciyle işaretlenmiş bir üye, herhangi bir sınıf veya metot tarafından erişilebilir.

### 2. `private`
- **Açıklama**: Sadece tanımlandığı sınıf içinde erişilebilir.
- **Özellikler**: Bu belirleyiciyle işaretlenmiş bir üye, sınıf dışından erişilemez.

### 3. `protected`
- **Açıklama**: Tanımlandığı sınıf içinde ve o sınıfı miras alan (türeten) sınıflar tarafından erişilebilir.
- **Özellikler**: Bu belirleyiciyle işaretlenmiş bir üye, miras alma yoluyla erişime izin verir ancak sınıf dışından doğrudan erişilemez.

### 4. `internal`
- **Açıklama**: Aynı proje (assembly) içinde herhangi bir yerden erişilebilir.
- **Özellikler**: Bu belirleyiciyle işaretlenmiş bir üye, proje dışından erişilemez.

### 5. `protected internal`
- **Açıklama**: Aynı proje içinde veya o sınıfı miras alan sınıflar tarafından erişilebilir.
- **Özellikler**: Bu belirleyici, hem `internal` hem de `protected` erişim seviyelerini birleştirir.

### 6. `private protected`
- **Açıklama**: Sadece tanımlandığı sınıf içinde ve o sınıfı miras alan sınıflar tarafından erişilebilir, ancak bu erişim yalnızca aynı projede geçerlidir.
- **Özellikler**: Bu belirleyici, hem `private` hem de `protected` erişim seviyelerini birleştirir.

<br>

> Bir class veya enum tanımlarken erişim belirleyicisi belirtmezsek, varsayılan olarak `internal` olarak kabul edilir. <br>
  Bir class içinde bir field, property veya metot tanımlarken erişim belirleyicisi belirtmezsek, varsayılan olarak `private` olarak kabul edilir.

## Boxing / Unboxing Nedir ?
### Boxing
Boxing, değer tiplerinin (value types) referans tiplerine (reference types) dönüştürülmesi işlemidir. Bu işlem sırasında, değer tipi bir object veya herhangi bir interface tipine dönüştürülür. Bu, değer tipinin heap'te bir nesne olarak saklanması anlamına gelir.

```csharp
int num = 123; // Değer tipi (value type)
object obj = num; // Boxing işlemi
```
> Yukarıdaki örnekte num isimli bir integer değişkeni obj isimli bir object değişkenine dönüştürülmektedir. Bu işlem sırasında num değer tipi heap'te bir nesne olarak saklanır.

### Unboxing
Unboxing, referans tiplerinin (reference types) tekrar değer tiplerine (value types) dönüştürülmesi işlemidir. Bu işlem, boxed nesnenin (boxed object) aslındaki değer tipine geri dönüştürülmesini içerir.

```csharp
object obj = 123; // Boxing işlemi
int num = (int)obj; // Unboxing işlemi
```
> Yukarıdaki örnekte obj isimli bir object değişkeni, tekrar integer değer tipine dönüştürülmektedir. Bu işlem sırasında obj referans tipi stack'te bir değer olarak saklanır.

## is ve as Operatörleri Ne İşe Yarar ?
### is operatörü
**is** operatörü bir nesnenin belirli bir türde olup olmadığını kontrol eder ve boolen bir değer döner. Eğer nesne belirtilen türe atanabiliyorsa `true`, atanamıyorsa `false` döner. Bu operatör, tür kontrolü yaparken güvenli bir şekilde kullanılır.

```csharp
object obj = "Hello, world!";
if (obj is string)
{
    Console.WriteLine("obj is a string");
}
```

### as operatörü
**as** operatörü, bir nesneyi belirli bir türe dönüştürmeye çalışır ve başarılı olursa dönüştürülen nesneyi döner, başarısız olursa `null` döner. **as** operatörü **is** operatöründen farklı olarak dönüşüm işlemi yapar ve dönüşüm başarısız olduğunda bir hata vermek yerine `null` döner.

```csharp
object obj = "Hello, world!";
string str = obj as string;

if (str != null)
{
    Console.WriteLine("obj was successfully cast to a string");
}
else
{
    Console.WriteLine("obj is not a string");
}
```

> `is operatörü:` Tür kontrolü yapar ve boolean bir değer döner (true veya false). Dönüşüm yapmaz. <br>
  `as operatörü:` Tür dönüşümü yapmaya çalışır ve başarılı olursa dönüştürülen nesneyi, başarısız olursa null döner.

## const ve readonly Arasındaki Fark Nedir ?
### const
- const anahtar kelimesi ile tanımlanan sabitler, derleme zamanında (compile-time) değeri bilinen ve değiştirilemeyen değerlerdir.
- const ile tanımlanan değişkenler yalnızca ilkel veri tiplerinde (int, double, char, vb.) ve string türünde olabilir.
- const değişkenleri sınıf (class) veya yapının (struct) herhangi bir üyesi olabilir, fakat mutlaka tanımlandıkları anda başlatılmalıdır.
- const değişkenleri static'dir ve sınıfın örneği olmadan erişilebilirler.

```csharp
public class MyClass
{
    public const int MyConst = 10;
}
```

### readonly
- readonly anahtar kelimesi ile tanımlanan alanlar, yalnızca tanımlandıkları anda veya ilgili sınıfın yapılandırıcı metodunda (constructor) başlatılabilirler.
- readonly alanlar çalışma zamanında (run-time) değer alabilirler ve değiştirilemezler.
- readonly alanlar ilkel veri tiplerinde olabileceği gibi karmaşık veri tiplerinde (class, struct) de olabilirler.
- readonly alanlar static olarak da tanımlanabilirler.

```csharp
public class MyClass
{
    public readonly int MyReadonlyField;

    public MyClass(int value)
    {
        MyReadonlyField = value;
    }
}
```