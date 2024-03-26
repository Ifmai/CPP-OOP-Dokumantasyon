# Namespace

## *Namespace nedir?*

*Namespace’i bir küme gibi düşünebiliriz. Kullandığımız değişkenleri, fonksiyonları, sınıfları vb. gruplamamızı sağlar ve aynı isme sahip olan değişken/fonksiyon/sınıflar çakışmasını önler.*

*Bu sayede aynı ismi taşıyan öğeler, farklı namespace'ler içinde birbirinden bağımsız olabilirler.*

```cpp
//Örnek bir namespace tanımı

namespace Template_1{
	int a = 5;
	int b = 7;
	int topla(int, int);
/* Eğer burada aşağıda ki gibi tanımlarsak "inline/macro function" olarak geçicektir.
(Bir sürü yerde kullanıcaksak eğer hızlı çalışacaktır ancak execute dosya boyutu
yükselecektir.)
[inline/macro function ne olduğunu bilmiyorsanız 2dk da aratarak hızlıca öğrenebilirisniz]
**int topla(int x, int y)**{
		return x+y;
}*/
}

namespace Template_2{
	int a = 10;
	int b = 20;
	int topla(int, int);
}

```

*Burada gördüğünüz örnekte 2 tane namespace oluşturduk. İki aynı değişkene sahipler ve aynı zamanda bir aynı isme sahip foksiyonları var. Çalışma sırasında bir birlerini etkilemezler veya çakışmazlar.*

*Bu ne için kullanılır?*

- *Örneğin 4-5 kişilik bir grup proje hazırlıyor diyelim ve herkes parça parça yazıyor ve en son birleştiricekler. ancak anyı isme sahip global değişkenler/fonksiyonlar kullanabilirler ve bunun sonucunda kodda çakışmaya neden olacağından ötürü hataya neden olacaktır.*

*Bunu nasıl çözebiliriz?*

- *Namespace kullanabilirsiniz. Her programcı kendi ksımına ait bir namespace oluşturur ve bu namespaceler üzerinden değişkenlerini/fonksiyonlarını kullanarak bu sorunu çözmüş olacaklardır.*
- *Class kullanabiliriz ancak nesneye ait olmayacak özellikleri çakışmaması için bir class’ta tutmak gereksiz ve kirli olucaktır (Ayrıca kesinlike mantıklı bir hareket değildir.). [ Bunu sakın yapmayın int main yerine void main yazmak gibi bir hareket yapmış olursunuz.]*

```cpp
//Namespace içinde ki fonksiyonları Scope dışında tanımlama.

int Template_1::topla(int x, int y){
	return x + y;
}

int Template_1::topla(int x, int y){
	return x + y;
}
```

*Burada kural şu şekilde işliyor*

> *Geriye_Dönüş_Tipi    Ait_Olduğu_Namespace_Adı::Fonksiyon_İsmi(Parametreler)*
> 

*Şimdi fonksiyon tanımlamayı biliyorsunuz ancak C++’da ki **“::”** bu arkadaş ne işe yarıyor?*

- *Bunun adı erişim operatörü (scope resolution operator) olarak geçiyor.*
- *Bu Class / Namespace alanındaki üyelerine/elemanlarına erişim sağlamak için kullanılır.*

```cpp
//Örnek bir main yazalım ve daha iyi anlayalım.

int main(){
		Template_1::a = 42; // yukarıda atadağım değerleri main üzerinde değiştirmiş oldum
		Template_1::b = 42;
// Template_1 isim alanındaki değişkenlere ve fonksiyona erişim
    std::cout << "Template_1::a + Template_1::b = " << Template_1::topla(Template_1::a, Template_1::b) << std::endl;
// Template_2 isim alanındaki değişkenlere ve fonksiyona erişim
    std::cout << "Template_2::a + Template_2::b = " << Template_2::topla(Template_2::a, Template_2::b) << std::endl;
// Farklı namespaceler üzerindeki değişkenleride toplayabiliriz.
		std::cout << "Template_1::a + Template_2::b = " << Template_2::topla(Template_1::a, Template_2::b) << std::endl;
// Ben burada Template_2'ye ait olan bir toplama işlemini kullandım ancak siz isterseniz 1'i kullanabilirsiniz.
// Sonuç olarak ikisde aynı işlemi yapcak sonuç değişmeyecek.
}
```

*Name Space Konusu Bu Kadar. :) Kendiniz örnekler yazarak daha iyi anlayabilirsiniz.*

### ***Yazmanız için bir örnek bırakayım.***

- *2 Adet Namespace Oluşturun.*
    - *Birinci Namespace’de değişkenleriniz bulunsun.*
    - *İkinci Namespacede ise fonksiyonlaırnız bulunsun.*
- *Birinci Namespace 2 adet int sayı tanımlayın.*
- *İkinci Namespace ise*
    - *Bir adet toplama fonksiyonu (Erişim operatörü ile scope dışında tanımlayın.)*
    - *Bir adet çıkarma fonksiyonu (inline bir şekilde tanımlayın.)*
- *Bu namespaceleri çalıştırmanız için bir main yazın.*
    - *İlk namespacede ki birinci int değerinize namespace içinde bir değer verin.*
    - *İkinci int değerinizi ise mainde atama işleme yapın.*