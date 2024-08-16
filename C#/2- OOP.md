
<h1 align="center">
  <br>
    Object Oriented Programming
  <br>
</h1>

## Class Nedir?
Nesne yönelimli programlamada (OOP) kullanılan ve bir nesnenin özelliklerini ve davranışlarını tnaımlayan bir yapıdır. 
- Referans tiplidir ve bu yüzden RAM'de hesap üzerinde tutulur.
- Class'lar kalıtım (inheritance) destekler.
- Class'larda, varsayılan constructor (yapıcı metot) bulunur ve bu metot ile nesne oluşturulabilir.
- Garbage Collection (Çöp Toplama) mekanizması ile yönetilir.

```csharp
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
    
    public void DisplayInfo()
    {
        Console.WriteLine($"Name: {Name}, Age: {Age}");
    }
}
```

## Struct Nedir?
Struct, küçük ve basit nesneler oluşturmak için kullanılan, gneellikle değer tipli olarak kullanılan bir veri yapısıdır. 
- Struct'lar değer tiplidir ve RAM'de stack üzerinde tutulur
- Structl'lar kalıtım desteklemez, ancak arabirimleri (interface) uygulayabilirler.
- Struc'larda parametresiz constructor kullanılamaz. Ancak parametreli constructor tanımlanabilir.
- Struct'lar genellikle hafif veri yapıları oluşturmak için kullanılır.

```csharp
public struct Point
{
    public int X { get; set; }
    public int Y { get; set; }

    public Point(int x, int y)
    {
        X = x;
        Y = y;
    }

    public void DisplayPoint()
    {
        Console.WriteLine($"X: {X}, Y: {Y}");
    }
}
```

## Class ve Struct Arasındaki Farklar

| Özellik                   | Class                                   | Struct                                 |
|---------------------------|-----------------------------------------|----------------------------------------|
| **Veri Tipi**             | Referans tipi                           | Değer tipi                             |
| **Bellek Konumu**         | Heap                                    | Stack                                  |
| **Kalıtım**               | Evet (inheritance destekler)            | Hayır (inheritance desteklemez)        |
| **Varsayılan Constructor**| Varsayılan parametresiz constructor     | Parametresiz constructor yoktur        |
| **Garbage Collection**    | Evet (çöp toplama mekanizması ile yönetilir) | Hayır (otomatik olarak yönetilir)  |
| **Kullanım Alanı**        | Karmaşık ve büyük veri yapıları         | Küçük ve hafif veri yapıları           |
| **Performans**            | Bellek tahsisi daha maliyetli olabilir  | Bellek tahsisi daha hızlıdır           |
| **Mutable/Immutable**     | Hem mutable hem de immutable olabilir   | Genellikle immutable (değişmez) olarak kullanılır |
| **Parametreli Constructor**| Evet                                   | Evet                                   |

## Nested Type Nedir?
Nested type, bir sınıfın, yapının veya arabirimin içinde tanımlanan türlerdir. Yani bir türü, başka bir türün içine yuvalanmış (nested) olarak tanımlayabilirsiniz. Bu türlere iç içe geçmiş türler veya nested types denir. <br>

Nested types, kapsayıcı türün (outer type) üyesi olarak davranır ve genellikle kapsayıcı tür ile mantıksal bir ilişkiyi temsil ederler. Nested types, içerdikleri türlerin kapsayıcı türün üyeleri gibi davranmasına olanak tanır.

```csharp
public class OuterClass
{
    // Nested class
    public class NestedClass
    {
        public void NestedMethod()
        {
            Console.WriteLine("Bu bir nested class metodudur.");
        }
    }
    
    public void OuterMethod()
    {
        Console.WriteLine("Bu bir outer class metodudur.");
    }
}

class Program
{
    static void Main()
    {
        // Nested class örneği oluşturma
        OuterClass.NestedClass nestedObject = new OuterClass.NestedClass();
        nestedObject.NestedMethod();
        
        // Outer class örneği oluşturma
        OuterClass outerObject = new OuterClass();
        outerObject.OuterMethod();
    }
}
```