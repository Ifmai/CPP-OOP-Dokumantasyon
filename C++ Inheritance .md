# C++ : Inheritance

Evet herkesin kafasını karıştıran konuya geldik. Korkmaya gerek yok aslında basit bir konu. Sadece ilk defa yazılımda böyle bir felsefe gördüğünüz için garip gelebilir başta.

Eğer lise düzeyince biyoloji bilginiz varsa gayet kolayca anlayabileceğiniz bir şey. Bir anne bir baba düşünün ve bu iki insanın bir çocuğu olduğunu düşünelim. Bu çocuk annesinden ve babasından belirli özellikler alın gen aktaramı sayesinde. Mesela gözleri annesine, saçları babasına vb. şeklinde bu örneği uzatabiliriz. İşte yazılımda ki kalıtımda aynı mantıkta ilerliyor. Ancak yazılımda ki fark şudur Ata sınıf dediğimiz kalıtım alınan sınıf atasının tüm özelliklerini barındırır. (Çekingen gen filan yok burada hepsi baskın.)

Şimdi aşağıda ki gibi bir ata sınıf oluşturalım örnek olarak.

```jsx
#include <iostream>
using namespace std;
class Human {
    private :
        string tc;
        string name;
        string surname;
    public :
        Human(string tc, string name, string surname):tc(tc),name(name),surname(surname){}
        void setTc(string inputTC){this->tc = inputTC;}
        void setIsim(string inputName){this->name = inputName;}
        void setSurname(string inputSurname){this->surname = inputSurname;}

        string getTc(){return tc;}
        string getName(){return name;}
        string getSurname(){return surname;}
};

int main(){
    Human alp("12312321321", "Alp","Özdemir");
    cout << "TC: " << alp.getTc() << " \nIsım: " << alp.getName() << " \nSoyisim: " << alp.getSurname() << endl;
}
```

Normal bir insanda herkes de bulunabilecek özellikleri bu sınıfta tanımladık. Şimdi bu sınıftan bir öğrenci class’ı oluşturalım. (Kalıtım olarak öğrenci sınıfı oluşturualım.)

Neden?

Böyle bir şeyi yapma nedenimiz şu bir sürü class tanımlayabiliriz bir projede. Mesela Human sınıfı üstünden bir öğrenci, öğretmen, yazılımıcı, vb. devam edebiliriz ve hepsinin ortak özelliği bir tc’si, ismi, soyismi barındırması. Bu şekilde ata class’tan üretmek bizim için daha avantajlı.

Şimdi bir classın diğer bir classtan nasıl miras alıyor görelim.

```cpp
class Ogrenci : public Human {
	private : 
		string ogrenciNo;
	public :
		Ogrenci(string ogrenciNo, string tc, string name, string surname) : ogrenciNo(ogrenciNo), Human(tc,name,surname){}
		void setNo(string ogrenciNo){this->ogrenciNo = ogrenciNo;}
		string getNo(){return this->ogrenciNo;}
};
```

Burada ilk gördüğümüz şey

```cpp
class Ogrenci : public Human
```

Burada ki “:” işareti bize bu class’ın Human class’ından üretildiğini ve onun özelliklerinin hepsini taşıdığını gösteriyor.

- Member Initializer List
    
    Burada gördüğümüz ikinci farklı şey ise
    
    ```
    	Ogrenci(string ogrenciNo, string tc, string name, string surname) : ogreciNo(ogrenciNo), Human(tc,name,surname){}
    ```
    
    Burada ise ogrenci no ataması normal bir şekilde atama yapıyoruz ancak Human class’ının Constructor’ını kulllanaraktan ona ait olan özelliklerin atama işlemlerini yapıyoruz. 
    
    Peki bu sistem nasıl çalışıyor? Şimdi şöyle ilk başta bu şekil tanımlamaya “***member initializer list veya kısaca initializer list***” denmekte. Bize “{}” içerisine girmeden sınıfa ait üyelere değer atamamızı sağlıyor. 
    
    Burada normal bir şekilde “***ogrenciiNo(ogrenciNo)***”  ******kısmında “:” sonra geldiğinde parantez dışında olanın sınıfın üyesi parantez içerisindeki ise paremetremiz olduğunu c++ anlamakta ve buna göre atama yapmaktadır.
    
    Şimdi Human kısmına gelicek olursak. Ogrenci Human class’ından miras alınarak üretilmiş bir sınıf bu sayede Human sınıfının yapıcısını kullanarak atama işlemlerini buradan yapabiliyoruz. 
    

<aside>
❓ Dip Not : Miras alınan sınıfa Taban Sınıf ondan üretilmiş olan sınıfa ise Türetilmiş Sınıf denmektedir.

</aside>