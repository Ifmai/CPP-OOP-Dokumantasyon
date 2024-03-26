# C++ : Diamond Problem

Çoklu kalıtımı öğrendik. Şimdi bu çoklu kalıtımı kullanırken ortaya çıkan bir “***Diamond Problemi***” olduğunu söylemiştik. Şimdi bu diamond problemi nedir? Nasıl çözülür? bunları görelim.

İlk başta Diamon Problemi neden olur?

![Ekran Resmi 2024-03-10 17.09.13.png](C++%20Diamond%20Problem%20a4f91cc7d3184697a1eb79d80f814acc/Ekran_Resmi_2024-03-10_17.09.13.png)

D sınıfı içerisinden A sınıfına ait bir üyeyi kullanırsanız diamond problemi dediğimiz soruna neden olmaktadır. Bu sorun neden kaynaklanır?

Şimdi D sınıfından A sınıfında bir üyeye erişmeye çalıştığımız da nasıl bir yol izlenir?

1. B üzerinden A’ya ulaşmak.
2. C üzerinden A’ya ulaşmak.

Ancak burada program ikisi üzerinden de gitmeye çalışıcaktır ve burada A sınıfından kullancağımız üyeden 2 tane ortaya çıkmış olucaktır ve bunun sonucunda karmaşıklığa neden olucaktır. Diamond Problemini kısıca bu şekilde anlatabiliriz. 

Resmi bir dille açıklama okumak istiyorsan :

<aside>
❕ Diamond problem", bir sınıf hiyerarşisinde iki farklı yol kullanılarak aynı üst sınıfın birden fazla kopyasına erişilmesi durumudur.

</aside>

Peki bu diamond problemini nasıl çözebiliriz?

```cpp
class A {}

class B : virtual public A{}
class C : virtual public A{}

class D : public B, public C {}
```

Önce resmi :

<aside>
❕ Sanal kalıtım (virtual inheritance), çoklu kalıtım (multiple inheritance) durumunda oluşabilecek çakışmaları (ambiguities) ve tekrarlanan üyeleri (repeated members) önlemek için kullanılan bir C++ özelliğidir.

Normal kalıtımda (non-virtual inheritance), bir alt sınıf, üst sınıfın tüm veri üyelerini ve işlevlerini kopyalar. Ancak çoklu kalıtım durumunda, bir sınıf, birden fazla üst sınıftan türetilirse ve bu üst sınıflar aynı üst sınıftan (örneğin, soyut bir sınıf) türetilmişse, alt sınıf, her bir üst sınıfın kopyasını tutar. Bu durumda, birden fazla yol aracılığıyla aynı üst sınıfa erişim mümkün olur ve "diamond problem"i (elmas problemi) ortaya çıkarır.

Sanal kalıtım, bu çakışmaları önlemek için kullanılır. Sanal kalıtım, üst sınıfın bir tek kopyasının alt sınıfa aktarılmasını sağlar. Böylece, elmas problemi ortadan kalkar ve programın tutarlılığı korunur.

</aside>

Şimdi biz B ve C sınıflarından A ya ulaşabiliyoruz. D sınıfı B ve C sınıfını aynanda miras aldığında bu durum sıkıntı çıkarıyor. Bunu çözmek için virtual anahtar kelimesini kullanıyoruz. Virtual olmadan burada 2 tane A sınıfı oluştuğundan kaynaklı Diamond problemini ile karşılaşıyorduk ancak virtual anahtar kelimesini kullandığımızda D sınıfı B ve C sınıflarını ne kadar miras alsada sadece bir tanesi üzerinden A sınıfı oluşturulur ve Diamond problemi ortadan kalkmış olur.