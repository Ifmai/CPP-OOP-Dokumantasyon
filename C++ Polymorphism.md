# C++ : Polymorphism

Şimdi **Polymorphism nedir? Sorusu ile ilk adımı atalım.**

<aside>
❕ Polimorfizm, C++ gibi birçok programlama dilinde bulunan bir kavramdır ve "çok biçimlilik" anlamına gelir. Bu kavram, farklı nesne veya veri tiplerinin aynı arabirim üzerinden çalışabilmesini sağlar. Polimorfizm, programların daha esnek, modüler ve genişletilebilir olmasını sağlar.

</aside>

Şimdi nedir bu çok biçimlilik nasıl kullanırız bunu kodda sorularına gelmeden önce bu konuyu daha netleştirelim.

Bunun için kedigiller ailesini örnek alalım. Kedi ırkı içerisinde kedi dediğimizde ilk aklımıza gelen sokaktaki tatlı canlılardan sonra kaplarlar ve çitalar gelebilir. Ancak hepsinin çıkardığı ses farklı. 

Bir sınıf tanımladığımızı düşünelim. Her sınıf için ayrı ayrı sınıflardan önce bir base sınıf inşa ederiz demi? 

```cpp
class Kedigiller{
	public:
		void ses(void);
};
```

Bu base sınıfımızı miras alan kaplan,kedi,çita vb. sınıflarımız olur. 

```cpp
class Kedi : public Kedigiller{};
class Aslan : public Kedigiller{};
class Cita : public Kedigiller{};
```

Normal inharetence’a göre hepsine ses methodunu yazarak override edebiliriz. Görelim.

```cpp
#include <iostream>

class Kedigiller{
	public:
		void ses(void){
			std::cout << "Base kedigiller" << std::endl;
		}
};

class Kedi : public Kedigiller{
	public:
		void ses(void){
			std::cout << "Kedi Miyavladı." << std::endl;
		}	
};
class Aslan : public Kedigiller{
	public:
		void ses(void){
			std::cout << "Aslan Kükredi." << std::endl;
		}
};
class Cita : public Kedigiller{
	public:
		void ses(void){
			std::cout << "Çita miyavladı." << std::endl;
		}
};

int main(){
	Kedigiller	b;
	Kedi		k;
	Aslan		a;
	Cita		c;
	b.ses();
	k.ses();
	a.ses();
	c.ses();

}
```

Nasıl bir ekran çıktısına sahip oluruz ?

Base kedigiller
Kedi Miyavladı.
Aslan Kükredi.
Çita miyavladı.

Şimdi bu yaptığımız  **Çok Şekillilik ( Polymorphism )** değil. Bu normal bir inheritance ve alt sınıfların üst sınıfın fonksiyonunu ezmeleri (override) örneğidir.

Bunun polymorphism olması için aynı arayüz üzerinden çalıştırılmaları gerekmektedir.

```cpp
int main(){
	Kedigiller *b[3];

	Kedi		k;
	Aslan		a;
	Cita		c;

	b[0] = &k;
	b[1] = &a;
	b[2] = &c;

	b[0]->ses();//kedi.
	b[1]->ses();//aslan.
	b[2]->ses();//cita.
}
```

Şimdi bu şekilde kullandığımız da polymorphism kullanmış oluyoruz. Aynı arayüz üzerinden çok şekillilik yapmış oluyoruz. Ancak bu kodda bir problem var eğer yukarıda ki main ile değiştirip çalıştırırsanız ekranda 3 defa “Base Kedigiller” yazısı görüceksiniz. Bunun nedeni artık burada işlerin değişmiş olduğudur.

Şimdi burada ki sorunu çözmek için kedigiller sınıfında ki ses methodunu sanallaştırmamız gerekiyor.

```cpp
class Kedigiller{
	public:
		virtual void ses(void){
			std::cout << "Base kedigiller" << std::endl;
		}
};
```

Bu şekilde yaptığımızda istediğimiz ekran çıktısını elde edebileceğiz.

Şimdi gelelim fasulyenin faydalarına bu işlem nasıl oluyor? (İnanın dökümantasyon yazmak çok zor bir şey yüz yüze şu durum çok rahat açıklarım ama yazıya dökmek zor işmiş.)

Bu olayı anlamak için iki şeyi iyi biliyor olmanız gerkeiyor. 

1. sanal fonksiyonlar 
2. dinamik bağlama (dynamic binding)

- Sanal Fonksiyonlar
    - Sanal fonksiyonlar, bir sınıf hiyerarşisinde alt sınıflar tarafından yeniden tanımlanabilecek fonksiyonlardır.
    - Bir üst sınıfta (bazen temel sınıf olarak da adlandırılır) tanımlanan bir fonksiyonun alt sınıflar tarafından aynı imzada (isim ve parametre listesi) yeniden tanımlanması durumunda, bu fonksiyon sanal fonksiyon olarak tanımlanabilir.
    - Sanal fonksiyonlar, genellikle **`virtual`** anahtar kelimesiyle tanımlanır.
    - Sanal fonksiyonların kullanılması, alt sınıfların temel sınıfın fonksiyonlarını ezerek kendi özel davranışlarını tanımlamasını sağlar.
    
    ```cpp
    class Base {
    public:
        virtual void func() {
            // Base sınıfının varsayılan implementasyonu
        }
    };
    
    class Derived : public Base {
    public:
        void func() override {
            // Derived sınıfının kendi implementasyonu
        }
    };
    ```
    
- Dynamic Binding
    - Dinamik bağlama, bir nesnenin hangi fonksiyonun çağrılacağının çalışma zamanında belirlenmesidir.
    - Polimorfik davranışı gerçekleştirmek için sanal fonksiyonlar ve dinamik bağlama birlikte kullanılır.
    - Eğer bir fonksiyon sanal (virtual) olarak tanımlanmışsa ve bu fonksiyon bir nesne üzerinden çağrılıyorsa, hangi fonksiyonun çağrılacağı o nesnenin türüne bağlı olarak çalışma zamanında belirlenir.
        - Bizim örneğimizde ise Kedigiller base sınıf olup ancak içerisinde kedi/aslan/çita herhangi birini barındırıyor. Bu durumda dynamic binding ve virtual fonksiyonlar sayesinde kedigiller base sınıfı içerisinde ki ses methodu yerine kedi/aslan/çita hangisini işaret ediyorsa onun ses methodunu çalıştırıyor.
    
    ```cpp
    // Bizim kodumuzdan örnek bir main.
    int main(){
    	Kedigiller *b = new Kedi;
    	b->ses();
    }
    ```