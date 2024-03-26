# C++ : Override(Ezme)

Şimdi overloading ile override çok fazla karıştırılıyor. Bu yüzden bunu yazma gereksinimi duyuyorum.

<aside>
❕ OVERRIDE ≠ OVERLOADING

</aside>

Şimdi bizim bir taban ve bir türemiş sınıfımız var olarak kabul edelim. Bu iki sınıftada aynı methodlar olabilir. Eğer aynı sınıf içerisinde bir methoddan aynısını varsa bu bu overloading işlemidir. Aşırı yükleme yapmış oluruz. Bir tabandan üretilmiş bir sınıfta aynı isimde bir method varsa bu sefer Override işlemi yapmış oluruz. Bir örnekle daha net anlıcağınızı düşünüyorum.

```cpp
#include <iostream>
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

        string getTc(){
			return tc;
			cout << "Human Sınıf get"<< endl;
		}
        string getName(){return name;}
        string getSurname(){return surname;}
};

class Ogrenci : public Human {
	private : 
		string ogrenciNo;
	public :
		Ogrenci(string ogrenciNo, string tc, string name, string surname) : ogrenciNo(ogrenciNo), Human(tc,name,surname){}
		void setNo(string ogrenciNo){this->ogrenciNo = ogrenciNo;}
		string getTc(){
			cout << "Ogrenci Sınıf get"<< endl;
			return this->tc;
		}
		string getNo(){return this->ogrenciNo;}
};

int main(){
	Ogrenci ifmai("12312312312", "12321321312", "ifmai", "github.com/ifmai");
	cout << ifmai.getTc() << endl; 
}
```

Yukarıya dikkatli bakarsanız hem Human sınıfı içerisinde getTC hem de Ogrenci sınıfının içerisinde getTc bulunmaktadır. Ancak burada program Ogrenci sınıfındakini kullanıcaktır yani taban sınıftaki getTc methodunu ezicektir.