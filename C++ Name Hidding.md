# C++ : Name Hidding

Şimdi çok kısa bir konu anlatacağım. Miras konusunu okuduysan orada Human sınıfından miras alarak Ogrenci sınıfını yazıyoruz.

```cpp
int main(){
	cout << sizeof(string) << endl;
	cout << sizeof(Human) << endl;
	cout << sizeof(Ogrenci) << endl;
}
```

Şimdi böyle bir main yazıcak olursak. String’in 8byte yer tuttuğunu görebilirsiniz ramde. Human ise 3 adet string barındırdığı için 24 byte yer kaplayacaktır. 

Ogrenci sınıfı ise içerisinde sadece ogrenciNo barındırmaktadır ancak sizeof sonucu 32 byte çıkıcaktır. Human sınıfınıda içerisinde barındırdığından ötürü toplamda 4 string barındırmış oluyor. Bu yüzde 4 * 8 = 32 byte yer tutmuş oluyor ramde. Burada name hidding olayı ise Human adına olmaktadır. Human sınıfını gizlemiş oluyoruz bir nevi. Bu olaya name hidding adı veriliyor. 🙂 

![./pngs/namehidding.png](./pngs/namehidding.png)