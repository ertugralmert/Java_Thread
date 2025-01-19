# Thread Safewty 
Çoklu thread işlemlerde güvenli  bir şekilde işlem yapmak için kullanırız.  
Özellikle Listeler üzerinde işlem yaparken mutlaka karşımıza çıkacaktır.  
Mesela bir nese içinde bir değerler toplamı almak istiyoruz bunu primitive  
değer ile yapamayızz.  

şimdi bunu anlamak için bir örnek yapalım.  
Önce bir öğrenci class oluşturup diğer sınıfta kullanalım.  
```java
public class Ogrenci(){
    String ad;
    String adres;
    int yas;
    
    public Ogrenci(String ad,String adres, int yas){
        this.ad = ad;
        this.adres = adres;
        this.yas = yas;
    }
    // getter setter ve to string yapın!!
    
}
```

```java
import java.util.List;
import java.util.concurrent.atomic.AtomicInteger;

public class Runner_ThreadSafewty() {
    public static void main(String[] args) {
        List<Ogrenci> ogrenciList = List.of(
                new Ogrenci("Mert", "Ankara", 21),
                new Ogrenci("Selim", "Ankara", 18),
                new Ogrenci("Ayşe", "Ankara", 20),
                new Ogrenci("Fatma", "Ankara", 24),
                new Ogrenci("Deniz", "Ankara", 19),
                new Ogrenci("Emel", "Ankara", 17)
        );
        // Şimdi burada yaşların toplamını almak istersek primitive degerlerle yapamayız.
        //foreach döngüsünde AtomicInteger kullanmamız gerekir.
        AtamicInteger yasToplami = new AtomicInteger(0);
        ogrenciList.forEach(ogrenci ->{
            yasToplami.set(yasToplami.get().ogrenci.getYas());
        });
        System.out.println("Toplam Yas: " + yasToplami.get());

        /**
         * Diğer kullanacağımız methodları paylaşayım:
         * yasToplami.incrementAndGet(); -> ++value; önce arttırıyor sonra kullanıyor.
         * yasToplami.decrementAndGet(); -> --value; 
         * yasToplami.get(); -> value
         * yasToplami.set(value);
         * yasToplami.getAndIncrement -> value++;   value arttırıyor sonra kullanıyor
         * yasToplami.getAndDecrement -> value--;  azaltıyor sonra kullanıyor
         */
    }
}
```
> kitleme işlemini volatile ile de çözebiliriz. Mesela  
> volatile int sayi;  
* Volatile ilgili not: 
> Volatile her zaman beklendiği gibi çalışmaz, çoklu ve farklı threadlerin  
> çalışmasında sorunlar çıkartabilir. Burada temel sorun,  
> farklı çekirdeklerden alınan verinin senkron bir şekilde işlenmemesi   
> mesela bir thread bir çekirdekte veriyi çekebilir ve aynı anda kilitlenme  
> olmadan veriyi çekebilir. Burada volatile farklı cache belleklerde tutulan  
> verinin senkron olmasını sağlarken bu tarz kullanımlarda sorunu çözmeyebilir.  
> Bu neden senkronizasyon sorunu çıkartabilir.  
> Burada senkron method bloklarının kullanılması daha doğru olacaktırç
> 