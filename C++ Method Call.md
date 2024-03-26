# C++ : Method Call

Bu sayfada bir türemiş sınıftan taban sınıfın Constructor’larını kullanmayı vb. öğreneceğiz.

Şimdi bundan önce sınıflarda ki üye ve methodlar için kullandığımız erişim belirteçlerini anladınız. (Eksiğiniz varsa geriye dönebilirsiniz.) Şimdi miras alırkenki erişim belirteçlerinden biraz bahsedip devam ediceğim.

- Erişim Belirtçekleri Detay Bilgi (Biliyorsan geçebilirsin Bilmiyorsan Kenardan açıp okuyabilirsin.)
    
    ```cpp
    class a {
    	private :
    		std::string ad;
    	public :
    		std::string get_stringad();
    		void set_ad(std::string);
    }
    
    class b : private a{
    }
    class c: public a{
    }
    class d: protected a{
    }
    ```
    
    Şimdi bunlar arasında ki fark ne?
    
    Eğer bir sınıfı miras alırken “public” derseniz o nesneye ait olan tüm özellikleri olduğu gibi kopyalar yeni türemiş sınıf için. Olduğu gibiden kastım şu:
    
    Public Inheritance:
    
    - Public bir özellik public olarak aktarılır. (Private → Private , Protected → Protected).
    
    Private Inheritance:
    
    - Hepsi tamamen private olarak aktarılır ve türemiş sınıftan hiç bir methoda veya üyeye erişim sağlayamazsınız.
    
    Protected Inheritance:
    
    - Private özellikler private olarak aktarılır.
    - Protected → Protected.
    - Public → Protected olarak aktarılacaktır türemiş sınıfa.
    
    ![Ekran Resmi 2024-03-07 11.12.37.png](C++%20Method%20Call%203de95d3548ae4bb9a4838b6f9ba3be99/Ekran_Resmi_2024-03-07_11.12.37.png)
    
    ![Ekran Resmi 2024-03-07 11.12.09.png](C++%20Method%20Call%203de95d3548ae4bb9a4838b6f9ba3be99/Ekran_Resmi_2024-03-07_11.12.09.png)
    
    ![Ekran Resmi 2024-03-07 11.11.40.png](C++%20Method%20Call%203de95d3548ae4bb9a4838b6f9ba3be99/Ekran_Resmi_2024-03-07_11.11.40.png)
    

- Constructor Called
    
    Şimdi Türemiş bir sınıf oluşturduğunuzda Taban sınıfın Constructorları vb. bunları nasıl çalıştırdığımızı göstereceğim.
    
    ```cpp
    #include <iostream>
    
    using namespace std;
    class Human {
        protected :
            string tc;
            string name;
            string surname;
        public :
    		Human(){
    			cout << "Human Default Constructor Called" << endl;
    		}
            Human(string tc, string name, string surname):tc(tc),name(name),surname(surname){
    			cout << "Human Constructor Called" << endl;
    		}
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
    		Ogrenci(string ogrenciNo, string tc, string name, string surname) : ogrenciNo(ogrenciNo){
    			this->tc = tc;
    			this->name = name;
    			this->surname = surname;
    			cout << "Ogrenci Constructor Called" << endl;
    		}
    		void setNo(string ogrenciNo){this->ogrenciNo = ogrenciNo;}
    		string getTc(){
    			cout << "Ogrenci Sınıf get"<< endl;
    			return this->tc;
    		}
    		string getNo(){return this->ogrenciNo;}
    };
    
    int main(){
        //cout << "TC: " << alp.getTc() << " \nIsım: " << alp.getName() << " \nSoyisim: " << alp.getSurname() << endl;
    	Ogrenci ifmai("12312312312", "12321321312", "ifmai", "github.com/ifmai");
    	cout << ifmai.getTc() << endl; 
    	//cout << ifmai.getSurname() << endl;
    }
    ```
    
    - Şimdi konunun başından beri kullandığımız örneği kullanmaya devam edelim ancak burada bir kaç ekleme var. (Değişmiş kısımları fark etmediysen toggle list’i açabilirsin)
        
        <aside>
        ❕ 1→Artık human Class’ımız Protected olarak Miras Alınıyor.
        
        2→ Human(){
        			cout << "Human Default Constructor Called" << endl;
        } Default bir constructor eklmesi yaptık.
        
        3→Ogrenci(string ogrenciNo, string tc, string name, string surname) : ogrenciNo(ogrenciNo){
        			this->tc = tc;
        			this->name = name;
        			this->surname = surname;
        			cout << "Ogrenci Constructor Called" << endl;
        } 
        Protected olarak miras aldığımız için bu şekilde kullanabiliyoruz.
        
        </aside>
        
    
    Şimdi burada iki durum anlatıcağım.
    
    - Birinci durumda normal daha önce yazdığımız kodu inceleyeceğiz.
        - Kod
            
            ```cpp
            #include <iostream>
            using namespace std;
            class Human {
                protected :
                    string tc;
                    string name;
                    string surname;
                public :
                    Human(string tc, string name, string surname):tc(tc),name(name),surname(surname){
            			cout << "Human Constructor Called" << endl;
            		}
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
            		Ogrenci(string ogrenciNo, string tc, string name, string surname) : ogrenciNo(ogrenciNo), Human(tc,name,surname){
            			cout << "Ogrenci Constructor Called" << endl;
            		}
            		void setNo(string ogrenciNo){this->ogrenciNo = ogrenciNo;}
            		string getTc(){
            			cout << "Ogrenci Sınıf get"<< endl;
            			return this->tc;
            		}
            		string getNo(){return this->ogrenciNo;}
            };
            
            int main(){
                //cout << "TC: " << alp.getTc() << " \nIsım: " << alp.getName() << " \nSoyisim: " << alp.getSurname() << endl;
            	Ogrenci ifmai("12312312312", "12321321312", "ifmai", "github.com/ifmai");
            	cout << ifmai.getTc() << endl; 
            	//cout << ifmai.getSurname() << endl;
            }
            ```
            
        
        Şimdi buradaki durum ise biz ogrenci sınıfının içinde atama yapmak için daha önceden yazdığımız Human Constructor’ımızı çağırıyoruz. Bu sayede atama işlemlerimizi daha hızlı yapmış oluyoruz. İkinci durumda atama işlemlerini ogrenci sınıfı içerisinden yapacağız.
        
    
    - İkinci durum ise  eğer bir türemiş sınıf üretirseniz ve yukardaki gibi protected miras alıp atama işlemlerini Taban sınıfın constructor’ını kullanmadan yaparsanız veya bunu yapmak saçma olucaktır ancak Human sınıfına ait herhangi bir üye veya method kullanmasanız dahi Human sınıfını miras aldığımız için “***Taban sınıfa ait olan Default Constructor Çalışacaktır*** ” ve hatta bu kodun ekran çıktısında aşağıdaki gibi görüceksiniz.
        
        ![Ekran Resmi 2024-03-07 11.53.53.png](C++%20Method%20Call%203de95d3548ae4bb9a4838b6f9ba3be99/Ekran_Resmi_2024-03-07_11.53.53.png)
        
        Bunun nedeni ise sizin Ogrenci sınıfını üretebilmeniz için ilk başta Human sınıfına ihtiyacınız olamasıdır. Constructorlar bir sınıf üretilirken otomatik olarak çalışan methodlar olduğu için biz burada ne kadar ogrenci sınıfını üretmek istesekte Human Constructor da çalışacaktır. Aynı zamanda burada ***Human Default Constructor yazmak zorunludur.*** Yazmadığınızda şöyle bir hata ile karşılaşırsınız.
        
        ![Ekran Resmi 2024-03-07 11.59.13.png](C++%20Method%20Call%203de95d3548ae4bb9a4838b6f9ba3be99/Ekran_Resmi_2024-03-07_11.59.13.png)
        
        Biz burada Human sınıfından miras almış bir sınıf ürettiğimiz için Human sınıfına ait bir Constructor arıyor program. Default olmasada normal bir constructor’ımız var evet ama onu biz çağırmadığımız için default constructor’a yöneliyor.
        
- Copy Constructor Called
    
    Şimdi geldik base sınıfın Copy Constructor’ını nasıl çağırabileceğimize. Aslında çok fazla bir farkı bulunmamaktadır. Burada aynı zamanda **Shallow** ve **Deep** copy farkını göreceğiz.
    
    ```cpp
    # include <iostream> 
    using namespace std;
    
    class Base {
        public :
            int * a;
            Base (int i = 1){
                a = new int(i);
                cout << "Base Kurucu" << endl;
            }
            Base(const Base& copy){
                cout << "Base Copy" << endl;
                a = new int(*copy.a);
            }
    };
    
    class Derived : public Base {
        public :
            int *b;
            Derived(int j = 1){
                cout << "Derived Kurucu" << endl;
                b = new int(j);
            }
    
            Derived(const Derived& copy){
                cout << "Derived Copy" << endl;
                b = new int(*copy.b);
            }
    };
    
    int main(){
    /*     Base baseObject(5);
        cout << baseObject.a << "\t" << *baseObject.a << endl;
        Base baseCopyObject = baseObject;
    
        cout << baseCopyObject.a << "\t" << *baseCopyObject.a << endl; */
    
        Derived derivedObject(500);
        cout << "Base a : " << derivedObject.a << "\t" << *derivedObject.a << endl;
        cout << "Derived b : " << derivedObject.b << "\t" << *derivedObject.b << endl << endl;
    
        Derived derivedCopyObject(derivedObject);
        cout << "Base a : " << derivedCopyObject.a << "\t" << *derivedCopyObject.a << endl;
        cout << "Derived b : " << derivedCopyObject.b << "\t" << *derivedCopyObject.b << endl;
    
    }
    ```
    
    Şimdi buradaki olayı konuşalım neler oluyor?
    
    Burada olan şey şu normalde c++ da copy constructor default olarak vardır. (Bazı standartlarda yok bu yüzden manuel yazmanız gerekebiliyor. Örneğin 98 standartında.) Burada ki copy constructor’ı silerseniz aynı adreslere sahip olduklarını görüceksiniz. Ancak burada ki ekran çıktısında durum böyle değil. 
    
    ![Ekran Resmi 2024-03-08 ÖS 6.18.25.png](C++%20Method%20Call%203de95d3548ae4bb9a4838b6f9ba3be99/Ekran_Resmi_2024-03-08_OS_6.18.25.png)
    
    Burada gördüğünüz gibi adresler farklı gözükmektedir. Bunun nedeni kendi copy constructorımızı yazdığımız için yeni int ile yer ayırarak yeni bir adrese kaydediyoruz. Bu işlemede deep copy deniyor. Diğer türlü default copy constructor shallow copy dediğimiz işlemi yapmaktadır ve eğer ilk oluşturduğumuz nesne silinip içerisinde ki adress freelenirse copy constructor’da ki int pointerın tuttuğu adreste silinicektir ve hata alırız. Deep copy bu tür durumlarda kullanılan bir yöntemdir. Atama operatörüde yazsak yine aynı şekilde çalışacaktır. 
    
    İncelemeniz için bir örnek bırakıyorum. 
    
    ```cpp
    # include <iostream> 
    using namespace std;
    
    class Base {
        public :
            int *a;
            Base (int i = 1){
                a = new int(i);
                cout << "Base Kurucu" << endl;
            }
            Base(const Base& copy){
                cout << "Base Copy" << endl;
                a = new int(*copy.a);
            }
            Base& operator=(const Base& copy){
                cout << "Base Operator=" << endl;
                delete a;
                a = new int(*copy.a);
                return *this;
            }
    };
    
    class Derived : public Base {
        public :
            int *b;
            Derived(int j = 1){
                cout << "Derived Kurucu" << endl;
                b = new int(j);
            }
    
            Derived(const Derived& copy){
                cout << "Derived Copy" << endl;
                b = new int(*copy.b);
            }
    
            Derived& operator=(const Derived& copy) {
                Base::operator=(copy);
                delete b;
                b = new int(*copy.b);
                cout << "Derived Operator=" << endl;
                return *this;
            }
    };
    
    int main(){
    /*     Base baseObject(5);
        cout << baseObject.a << "\t" << *baseObject.a << endl;
        Base baseCopyObject = baseObject;
    
        cout << baseCopyObject.a << "\t" << *baseCopyObject.a << endl; */
    
        Derived derivedObject(250);
        cout << "Base a : " << derivedObject.a << "\t" << derivedObject.a << endl;
    
        Derived derivedCopyObject(5000);
        cout << "Base a : " << derivedCopyObject.a << "\t" << derivedCopyObject.b <<  endl;
    
        derivedCopyObject = derivedObject;
    
        cout << "Base a : " << derivedCopyObject.a << "\t" << derivedCopyObject.b << endl;
    
    }
    ```
    
- Destructor Called
    
    Sadece örnek kod bırakacağım. Buraya kadar okuduysanız bence artık bu kodu kendiniz okuyup yorumlayabileceğinizi düşünüyorum.
    
    ```cpp
    # include <iostream> 
    using namespace std;
    
    class Base {
        public :
            int *a;
            Base (int i = 1){
                a = new int(i);
                cout << "Base Kurucu" << endl;
            }
            Base(const Base& copy){
                cout << "Base Copy" << endl;
                a = new int(*copy.a);
            }
            Base& operator=(const Base& copy){
                cout << "Base Operator=" << endl;
                delete a;
                a = new int(*copy.a);
                return *this;
            }
            ~Base(){
                cout << "Delete A 'Base Destructor'" << endl;
                delete a;
            }
    };
    
    class Derived : public Base {
        public :
            int *b;
            Derived(int j = 1){
                cout << "Derived Kurucu" << endl;
                b = new int(j);
            }
    
            Derived(const Derived& copy){
                cout << "Derived Copy" << endl;
                b = new int(*copy.b);
            }
    
            Derived& operator=(const Derived& copy) {
                Base::operator=(copy);
                delete b;
                b = new int(*copy.b);
                cout << "Derived Operator=" << endl;
                return *this;
            }
            ~Derived(){
                cout << "Delete B 'Derived Destructor'" << endl;
                delete b;
            }
    };
    
    int main(){
    /*     Base baseObject(5);
        cout << baseObject.a << "\t" << *baseObject.a << endl;
        Base baseCopyObject = baseObject;
    
        cout << baseCopyObject.a << "\t" << *baseCopyObject.a << endl; */
    
        Derived derivedObject(250);
        cout << "Base a : " << derivedObject.a << "\t" << derivedObject.a << endl;
    
        Derived derivedCopyObject(5000);
        cout << "Base a : " << derivedCopyObject.a << "\t" << derivedCopyObject.b <<  endl;
    
        derivedCopyObject = derivedObject;
    
        cout << "Base a : " << derivedCopyObject.a << "\t" << derivedCopyObject.b << endl;
    
    }
    ```
    
    Aşağıda ki kod yanlıştır. Çalışmayacaktır.
    
    ```cpp
            ~Derived(): ~Base(){
                cout << "Delete B 'Derived Destructor'" << endl;
                delete b;
            }
    ```
    
    Böyle bir şeyi denerseniz c++ size dostum bunu ben zaten çalıştırıcağım senin bunu yapmana gerek yok diyecektir.