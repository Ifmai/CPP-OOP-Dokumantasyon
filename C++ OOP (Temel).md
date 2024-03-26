# C++ OOP (Temel)

<aside>
💡 *Başlamadan önce sunu söylemek istiyorum. Bu dökümantasyon ortalama bir yazılım bilgisi olan ancak “OOP nedir?”, “Class ve obje nedir neyin nesidir abi bu OOP” gibi sorulara cevap niteliğinde olacaktır.*

</aside>

- ***Bu dökümantasoyunu okumaya başlamadan önce bilmeniz gerekenler***
    - Diziler, Pointerlar, Referans veri tipleri
    - Diziler veya Pointer Arrayler kullanmayı
    - Pointer ve Referans Arasında ki Farklar
    - Referans Kullanımının Avantajları
    - Fonksiyon türlerini ve tanımlamaları

*Şimdi OOP’ye girmeden önce C++ dilinde kullanılan “**namespace**” adında ki uzay boşluğumuzdan bahsedelim. [Buraya Tıklayarak Gidebilirsin.](https://www.notion.so/Namespace-40f15b2c78bc40b29e14000040095c13?pvs=21)*

Dip not : Eğer bu sayfayı daha önce okuduysan sayfanın sonundaki Page Db sayfasından veya [***şuraya***](https://www.notion.so/C-Page-DB-6787f893909a4dd384cf35cb2d5ea021?pvs=21) tıklayarak gidebilirsin. 

---

Şimdi OOP’ nedemek?

- OOP’nin açılımı Object-Oriented Programming (Nesne Tabanlı Programlama) anlamına gelmektedir.

Şöyle bir açıklama bulabilirisniz OOP hakkında.

> Yazılım geliştirme için bir programlama paradigmasıdır. OOP'nin temel amacı, yazılımın organizasyonunu ve tasarımını, gerçek dünyadaki nesnelerin modellenmesine dayandırmaktır "Paradigma," genel olarak bir teori, model veya örüntü anlamına gelir. (burada model anlamında kullanılmaktadır.)
> 

Şimdi OOP’de en çok duycağınız iki adet terim vardır.

1. Nesne (Obje)
2. Sınıf (Class)

### Nedir bu Nesne ve Sınıf (Class)?

### Nesne (Obje) 📦

Gerçek dünyadaki varlıkların (objelerin) yazılım tarafından temsil edilmesidir. Her nesne, veri (state) ve bu veri üzerinde işlem yapan metodları (behavior) içerir.

### Class (Sınıf)

Sınıflar, nesnelerin tasarım şablonlarıdır. Belirli bir sınıftan oluşturulan nesneler, aynı özelliklere (veri) ve davranışlara (metodlar) sahip olacaktır. Sınıflar, nesnelerin nasıl oluşturulacağını ve nasıl davranacaklarını tanımlar.

Yani şimdi bu terimsel açıklamayı şöyle bir örnek verelim hem de class oluşturmayı görelim.

```cpp
/* Şimdi bir proje grubu oluşturucağımızı düşünelim ve bu gruba katılmak için
adayların bulunduğunu düşünelim.

Bu adayların özellikleri ne olur?
İsim, Yaş, Cinsiyet, Meslek, Uzman oldukları konu.

Bu Adaylar katılmak için mülakata geldiğinde ne yaparlar?
Kendilerini tanıtırlar, Hangi alanda iyi olduklarını söylerler.

Şimdi Classlar bizim için bir nesnenin şablonları ise nesnenin özellikleri 
üye değişkenlerimiz olur.

Yaptıkları şey ise üye methodlarımız olur.

Şimdi Class yapımızı oluşturalım */

class Aday {
	private :
		std::string isim;
		int yas;
		std::string cinsiyet;
		std::string meslek;
		std::string uzman_alan;
	public :
		Aday(std::string isim, int yas, std::string cinsiyet, std::string meslek, std::string uzman_alan);
		void kendini_tanit();
		void uzman_alanin();
};

//Dip not : Aday methodu ve Private ve Public kısmına takılmayın onları
//birazcık ileride anlatacağım. Şuan önemli olan ana şablona ve konuya odaklanın :)
```

Şimdi bu gördüğünüz bizim için örnek bir class (sınıf). Bundan üreteceğimiz bir değişkene nesne diyoruz.

```cpp
int main(){
	Aday ifmai("Alp", 21, "Erkek", "Yazılım Mühendisi", "Backend");
}
// Burada ifmai adında Aday Sınıfında bir nesne üretmiş oluruz.
```

Kısa bir özetle OOP dediğimiz şey aslında budur. Gerçek hayattaki bir nesneyi programlama dilinde modelleme işlemidir.

Şimdi Class ve Nesne arasında ki farkı öğrendiğinize göre yukarda kullandığım “private / public”’ anahtar kelimelerinin ne olduğunu ve ne işe yaradıklarını öğrenelim.

Private

Private karakteri özel anlamına geliyor. Peki ne işe yarar bu anahtar kelime?

Bir Class içerisinde Private olarak tanımladığımız her şey dışarıdan ulaşılamaz hale gelir. Sadece class içerisinden ulaşım gerçekleştirilir.

Public

Public ingilizce çevirisi halk olarak geçmekle berber bunu yazılım dilindeki anlamı ise altında bulunan değişkenlerin veya methodların dışardan ulaşılabilir olduğu anlamına gelmektedir.

Protected

Sadece tanımını yapacağım çünkü bunu OOP’nin kalıtım miras alma kısmında kullanacağız.

Protected anahtar kelimesi altında tanımlanan şeyler kendinden kalıtım alarak üretilmiş classlar dışında ve kendi içerisinden hariç olmak üzere hiç bir yerden ulaşılamaz olmasıdır.

Gelin bunu bir örnekten yola çıkarak anlatalım.

```cpp
#include <iostream>
using namespace std;

class dikdortgen{
	public:
		int x;
		int y;
		void dikdortgen_alani();
};

class kare{
	private:
		int x;
	public:
		void kare_alani();
};

void kare::kare_alani(){
	std::cout << "Kare'nin alanı :" << x * x<< "'dir" << std::endl;
}

void dikdortgen::dikdortgen_alani(){
	std::cout << "Dikdörtgen'nin alanı :" << x * y << "'dir" << std::endl;
}

int main(){
	dikdortgen example_dikdortgen;
	example_dikdortgen.x = 10; // public olduğu için mainden ulaşabiliyorum.
	example_dikdortgen.y = 20;
	example_dikdortgen.dikdortgen_alani();

	kare example_kare;
	example_kare.x = 10; 
// ancak bu kod burada private olana bir değişkene ulaşmaya 
// çalıştığımdan ötürü hata vericektir.
	example_kare.kare_alani();
}
```

Peki şimdi ben bu nesnenin sadece class içinden ulaşabileceksem niye tanımlıyorum, dışardan kullanamıyorum erişemiyorum tanımlamaktaki amaç ne? sorusunu soruyor olabilirsin. 

**Sana bu sorunu şu şekilde cevaplayacağım.** 

- **Gizlilik ve Güvenlik** : Private değişkenler, dış dünyadan gelen müdahalelere karşı koruma sağlar. Bu sayede, bir class'ın iç mantığı ve verileri, dışarıdaki kod tarafından istenmedik şekillerde değiştirilip bozulmaktan korunur.

- **Kodun Bakımı ve Güncellenmesi :** Eğer bir değişken public veya protected olarak tanımlanmışsa ve bu değişkenle ilgili dışarıda çok sayıda kod varsa, bu değişkenin yapısının değiştirilmesi daha zor olabilir.

- **Kodun Anlaşılabilirliği:** Eğer bir değişkenin sadece belirli bir class içinde kullanılması gerekiyorsa, bu değişkeni private yapmak, kodun daha anlaşılabilir olmasına yardımcı olabilir. Bu sayede ekip olarak çalışırken diğer arkadaşların daha rahat kodu okuyup anlayabilirler.
- **Encapsulation (Kapsülleme) [Sakin ol aşağıda anlatıyorum hemen altta.]**

Şimdi bu nesnelere sınıf haricinde ulaşamadığın için onları kullanamıyor veya değiştiremiyor değilsin. Bunları yine yapabilirsin ancak bu durumda OPP’nin “**Kapsülleme ve Getter & Setter Methodları**” devreye girmekte.

- **Şimdi Kapsülleme Ne demek?**
    
    Encapsulation, yazılım geliştirmede bir tür "gizleme" işlemidir. Private değişkenler, sanki bir kutu içinde saklanıyormuş gibi düşünülebilir. Bu kutu, sadece o kutuyu oluşturan sınıfın içinden erişilebilen bir şeydir. Yani, bir class içindeki bazı bilgileri sadece o class'ın kendisinin kullanabilmesi için "private" olarak işaretleriz.
    
    Örneğin, bir sınıfın içinde bir değişkeni private yapmak, sanki o değişken sadece o sınıfın içindeki işlevlere aitmiş gibi davranmasını sağlar. Bu, başka kodlar o sınıfı kullanırken bu değişkenin iç yapısıyla doğrudan etkileşime girmesini engeller.
    
    Bunu bir örnekle düşünelim: Diyelim ki bir araba sınıfımız var ve bu arabada bir hız değişkeni var. Eğer hız değişkenini public yaparsak, dışarıdan herkes doğrudan bu hızı değiştirebilir. Ancak eğer hız değişkenini private yaparsak, sadece arabayı kontrol eden sınıfın içinde bu hıza müdahale edebiliriz. Bu, arabayla ilgili değişiklikler yaparken sadece arabanın iç yapısıyla uğraşmamıza ve başka kodları etkilememize izin verir, bu da kodun daha temiz, anlaşılır ve bakımı kolay olmasına yardımcı olur.
    
    Yani, encapsulation aslında "detayları gizleme" felsefesine dayanır ve bu da bir programın daha modüler ve sürdürülebilir olmasına katkıda bulunur.
    

```cpp
// Yukarıda Private Değeri olana bir kare class'ım vardı.
// Şimdi o class'ı alalım ve gettter & setter methodlarını yazalım.
#include <iostream>
using namespace std;

class Kare{
	private:
		int x;
	public:
		void kare_alani();
		int get_x();
		void set_x(int new_x);
};

int Kare::get_x(){
	return this->x;
}

void Kare::set_x(int new_x){
	this->x = new_x;
}

// Şimdi o private değişkenlerimize class üzerinden ulaşmış set ve get
// işlemlerimizi yapmış olduk.

// Hadi gel main'de nasıl kullanıyoruz görelim.

int main(){
	Kare a;
	
	a.set_x(10); // a nesnesi üzerinden set methodumuz ile x'in değerini 10 olarak
	// değiştirdik.
	cout << "a adında ki karenin x değeri : " << a.get_x() << endl;
	// Burada da a nesnesi üzerinden get methodumuz ile x değerini öğrendik
	// ve ekrana yazdırdık.
}
```

> Dip Not : Bazen bazı değişkenlerimizi class’için de oluşturduğumuz gibi değerlerini atarız ve sadece “Get” methodumuzu yazarız. Güvenlik ve kısıtlama yapmak isticeğimiz bazı zamanlarda “Set” methodunu es geçildiğini görebilirsiniz.
> 

Şimdi buraya kadar neler öğrendik?

- OOP’nin ne olduğunu ve tanımını anladık.
- Nesne ve Sınıf arasında ki farkı gördük.
- Bir class oluşturmayı ve bir classtan nasıl bir nesne oluştururuz.
- Method tanımları ve nasıl başka bir c dosyasında tanımlayabiileceğimizi gördük.
- Kapsülleme nedir? Neden kapsülleme yaparız? gibi soruların cevaplarını aldık.
- Obje üzerinden sınıfa ulaşmayı öğrendik.

Özetle temel seviyede Class ve nesneler ile nasıl basit şeyler yapabileceğimi gördük. 

Şimdi basit temel kısmı bitirdik. Burayı tamamen anladıysan bir sonraki kısma geçebiliriz. 😊

- ***C++ OPP Database***
    
    [C++ Page DB](https://www.notion.so/C-Page-DB-6787f893909a4dd384cf35cb2d5ea021?pvs=21)