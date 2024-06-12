
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
