# C++: Inheritance Erişim Belirteçleri

Şimdi c++ ‘da nasıl bir sınıf oluşturuacağımızı nasıl bir sınıftan miras alarak yeni bir türemiş sınıf oluşturucağımızı öğrendik. Buraya kadar c++ temelde gösterdiğim bir konunun üstünden geçiceğiz

Erişim Belirteçleri (Public - Private - Protected)

Public’i anladığınızı düşünüyorum. Bu yüzden sadece Private Protected arasında ki farktan bahsedeceğim.

Şimdi Private yaparsak eğer bir sınıf içerisindeki üyeleri ondan miras alarak türetilen sınıflarda taban sınıfın üyeleri direk ulaşım sağlayamayız. Bu durumda get/set/constructor methodlarını kullanmak zorunda kalırız. İlk Inheritance örneğimizde olduğu gibi.

Şimdi ise protected’da ise fark şudur.

- Taban sınıf üyelerine private’ta olduğu gibi sınıf dışarısından ulaşım engellenir.
- Taban sınıftan türetilmiş bir nesne taban sınıfın üyelerine direk erişim sağlayabilir.
- Protected erişim belirteçi kendin türetilmiş sınıflara erişim imkanı vermektedir.

Private :

```cpp
include <iostream>
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

class Ogrenci : public Human {
	private : 
		string ogrenciNo;
	public :
		Ogrenci(string ogrenciNo, string tc, string name, string surname) : ogrenciNo(ogrenciNo), Human(tc,name,surname){}
		void setNo(string ogrenciNo){this->ogrenciNo = ogrenciNo;}
		string getNo(){return this->ogrenciNo;}
};
```

Protected:

```cpp
include <iostream>
using namespace std;
class Human {
    protected :
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

class Ogrenci : public Human {
	private : 
		string ogrenciNo;
	public :
		Ogrenci(string ogrenciNo, string tc, string name, string surname) : ogrenciNo(ogrenciNo){
			this->tc = tc;//Direk Human sınıfının nesnelerine ulaşım sağlayabiliyorum.
			this->name = name;//Private'ta ise böyle bir imkanımız yok.
			this->surname = surname;	
}
		void setNo(string ogrenciNo){this->ogrenciNo = ogrenciNo;}
		string getNo(){return this->ogrenciNo;}
};
```