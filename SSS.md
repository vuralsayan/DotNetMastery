
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