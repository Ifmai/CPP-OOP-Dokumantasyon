# C++ :  Const

Sabit Methodlar ve Sabit Nesneler. Const C++’da önemlidir. Bir söz vardır const olmaması gereken şeyler dışında her şey const olmalıdır. 

Const değişkenler bildiğiniz üzere değerin değişmesini engelliyor. Bir değişkeni const yaparsak değerini sabitlemiş oluruz ancak bunu bir nesne üzerinde denersek ne olur?

```cpp
int main(){
	const Kare a(4);
} 
```

Const bir nesne oluşturduğumuz da o nesneye ait hiç bir methodu kullanamazsınız ve hiç bir public değişkenede atama/değer değiştirme işlemi yapamazsınız.

Bunu copy constructor da görmüşsünüzdür veya assigment operator= overloading işleminde. En basit kullanım örneğini oradan verebilirim. Çünkü copy veya eşitleme esnasında kopyalayacağımız nesnenin üyelerinin değerlerinin değişme uğramasını istemeyiz.

Bir Sınıfa ait bir method nasıl const yapılı? Yapılırsa ne olur?

```cpp
class Kare{
	private:
		int x;
	public:
		void set_x(int _x);
		int get_x() const; // Bir methodu bu şekilde const olduğunu belirtiyoruz.
}
```

Eğer bir methodu const yaparsak eğer o method içerisinde o sınıfa ait hiç bir değişkenin değerini değiştiremeyiz. Mesela set_x methodunu const yapmıyoruz çünkü içerisinde x değerinin değerini değiştireceğiz. Bu durumdan ötürü set_x const olarak belirtilemez ancak get sadece bize x’in değerini geri döndüren bir method olduğu için rahat bir şekilde const olarak belirleyebilirz.

Bunun başlıca nedeni karmaşıklığı önlemektir. Örneğin bir sınıf üyeniz bir method içerisinde değeri değiştiği için hatalı sonuç alıyorsunuz ancak hangi method olduğunu bilmiyorsunuz. Burada eleme yapabiliyoruz.

<aside>
💡 Dip Not : Bir methodu const yapmak aynı zamanda farklı bir overloading yöntemidir.

```cpp
class Kare{
	private:
		int x;
	public:
		void set_x(int _x);
		int get_x();
		int get_x() const; // Bir methodu bu şekilde const olduğunu belirtiyoruz.
}
```

</aside>