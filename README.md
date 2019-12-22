## STRUCTURAL TASARIM DESENİ

## PROXY TASARIM DESENİ 
 
Proxy modelinde, sınıf başka bir sınıfın işlevselliğini temsil eder. Bu tip tasarım deseni yapısal desen altındadır. Proxy modelinde, işlevselliğini dış dünyaya arayüzlemek için orijinal nesneye sahip nesne yaratırız. 
 
## ÖRNEK UYGULAMA 
Bir Image arayüzü ve Image arayüzünü uygulayan somut sınıflar oluşturacağız. ProxyImage, RealImage nesnesi yüklemesinin bellek kapladığı alanı azaltmak için kullanılan bir proxy sınıfıdır.Demo sınıfımız olan ProxyPatternDemo, bir Image nesnesini yüklemek ve gerektiğinde görüntülemek için ProxyImage kullanacaktır. 
 
## CLASS DİYAGRAMI :  
 
 ![Image of Class](https://github.com/ronahiay/yazilimmimarisi/blob/master/classdiagramproxy.PNG)
 
1.ADIM  : 
Yeni bir interface oluşturuyoruz. 
Dosya adı : image.java 
```java
Public interface Image { 
Void display(); 
} 
```
 
2.ADIM : 
Aynı arayüzü uygulayan somut sınıflar oluşturuyoruz. 
Dosya adı : RealImage.java 
```java
Public class RealImage implements Image { 
Private String dosyaismi; 
Public RealImage(String dosyaismi){ 
This.dosyaismi = dosyaismi; 
LoadFromDisk(dosyaismi); 
} 
 
@Override 
Public void display(){ 
System.out.println(“durdur” + dosyaismi); 
} 
Private void loadFromDisk(String dosyaismi){ 
System.out.println(“devam” + dosyaismi); 
} 
} 
Dosya adı : proxyImage.java 
Public class ProxyImage implements Image{ 
 
Private RealImage realImage; 
Private String dosyaismi; 
 
Public ProxyImage(String dosyaismi){ 
This.dosyaismi = dosyaismi; 
} 
 
@Override  
Public void display(){ 
  If()realImage == null){ 
RealImage = new RealImage(dosyaismi); 
} 
RealImage.display(); 
} 
} 
 ```
3.ADIM : 
Gerrektiğinde RealImage sınıfının nesnesini almak için ProxyImage kullanır. 
Dosya ismi : ProxyPatternDemo.java 
```java
Public class ProxyPatternDemo { 
 
Public static void main(String[] args) { 
Image image = new ProxyImage(“deneme_10mb.jpg”); 
// resimi diskten yüklemek  için  
image.display(); 
System.out.println(“”); 
 
//resim diskten yüklenmeyecekse  
image.display(); 
} 
} 
 ```
4.ADIM : 
Bu adımda çıktıyı doğrularız.
```java 
Devam deneme_10mb.jpg 
Durdur deneme_10mb.jpg 
. 
Durdur deneme_10mb.jpg 
```
## BEHAVORIAL TASARIM DESENİ
## ITERATOR TASARIM DESENİ  
Yineleyici desen, Java ve .Net programlama ortamında çok yaygın olarak kullanılan tasarım modelidir. Bu desen, bir koleksiyon nesnesinin öğelerine, altta yatan temsilini bilmeye gerek kalmadan sıralı bir şekilde erişmek için bir yol elde etmek için kullanılır.Yineleyici pattern davranışsal pattern kategorisine girer. 
 
## ÖRNEK UYGULAMA 
 
Gezinme yöntemini anlatan bir Yineleyici arabirimi ve yineleyiciyi yeniden ayarlayan bir Konteyner arabirimi oluşturacağız. Konteyner arayüzünü uygulayan somut sınıflar, Yineleyici arayüzünü uygulamak ve kullanmaktan sorumlu olacaktır. IteratorPatternDemo, demo sınıfımız NamesRepository'de koleksiyon olarak saklanan Adları yazdırmak için somut bir sınıf uygulaması olan NamesRepository'yi kullanacaktır. 
 
## CLASS DİYAGRAMI : 
 
 ![Image of Class](https://github.com/ronahiay/yazilimmimarisi/blob/master/Iteratortasarımdeseni.PNG)
 
1.ADIM :  
Arayüzünü oluşturuyoruz. 
Dosya ismi  : Iterator.java 
 ```java
Public interface Iterator { 
Public boolean hasNext(); 
Public Object next(); 
} 
 
Dosya ismi : Container.java 
Public interface Container { 
  Public Iterator getIterator(); 
} 
 ```
 
2.ADIM :  
Container arayüzünü uygulayarak somut sınıf oluşturun. Bu sınıf, Iterator arabirimini uygulayan iç sınıf NameIterator'a sahiptir. 
Dosya ismi : NameRepository.java 
```java
public class NameRepository implements Container { 
   public String names[] = {"Robert" , "John" ,"Julie" , "Lora"}; 
 
@Override 
   public Iterator getIterator() { 
      return new NameIterator(); 
   } 
 
private class NameIterator implements Iterator { 
 
int index; 
 
@Override 
      public boolean hasNext() {       
if(index < names.length){ 
            return true; 
         } 
return false; 
      } 
@Override 
      public Object next() {       
         if(this.hasNext()){      
       return names[index++]; 
} 
         return null; 
      } 
   } 
} 
 ```
 
3.ADIM : 
Yineleyici ve baskı adları almak için NameRepository'yi kullanın. 
Dosya ismi : NameRepository.java 
```java
public class NameRepository implements Container { 
   public String names[] = {"Robert" , "John" ,"Julie" , "Lora"}; 
 
@Override 
   public Iterator getIterator() { 
      return new NameIterator(); 
   } 
 
private class NameIterator implements Iterator { 
 
int index; 
 
@Override 
      public boolean hasNext() {       
if(index < names.length){ 
            return true; 
         } 
return false; 
      } 
@Override 
      public Object next() {       
         if(this.hasNext()){      
       return names[index++]; 
} 
         return null; 
      } 
   } 
} 
```
 
4.ADIM : 
Çıktıyı doğruluyoruz. 
```java
 Name : Robert 
Name : john 
Name : Julie 
Name : lora 
```
