# Thread Kullanimi
Bir thread oluşturmanın 2 yöntemi vardır;  
1- Thread sınıfını miras alarak runable bir sınıf oluşturmak.  
2- Runnable interface'ini kullanarak runnable bir sınıf oluşturmak  
Bu iki yöntemden 2. yöntem tercih edilmelidir. Çünkü, java da bir sınıfın tek  
inheritance şansı vardır. Bu nedenle bu kalıtım şekli interface olarak tercih edilmelidir.  

örnekler:
> Dikkat!!! Burada amaç bir sınıftan nesne yaratmak ve bu nesnenin referansını Runnable  
> sınıflar içerisine vermek  

Aşağıdaki örnekte Thread ile sayı arttırma ve eksiltme işlemi yapıyoruz.  
Burada 1milyon sayı azaltıp ve azaltıyoruz. iki thread'te başlatıyoruz ve sonucu görüyoruz.
```java
public class ThreadKullanimi {
    public static void main(String[] args) {

        Deger deger = new Deger();
        //Thread class değerinde constructor oluşturduktan sonra;
        Threadclass threadclass = new ThreadClass(deger);
        // Runnable implement ettiğimiz class'tan nesne yaratıyoruz
        RunnableClass runnableClass = new RunnableClass(deger);
        
        // Runnable bir class çalıştırılması için bir thread ihityacı duyar.
        threadclass.start(); // thread kendisi start yapabilir.
        //Runnable class çalıştırmak için bir thread oluşturmamız gerekir.
        Thread threadR = new Thread(runnableClass);
        threadR.start();
    }
}


// bir class tanımlayalım
class Deger{
    int sayi;
}

// bir class daha oluşturalım
class ThreadClass extends Thread{
    Deger deger;
    // nesne yaratırken constructrounda
    public ThreadClass(Deger deger){
        this.deger = deger;
    }
    public void run(){
        for (int i = 0; i<1_000_000; i++){
            deger.sayi++;
            System.out.println("Thread Deger: " + deger.sayi);
        }
    }
}

//Runnableclass oluşturalım
class RunnableClass implements Runnable{
    Deger deger;
    public RunnableClass(Deger deger){
        this.deger = deger;
    }
    @Override
    public void run(){
        for (int = 0; i<1_000_000; i++){
            deger.sayi--;
            System.out.println("Runnable Deger: "+ deger.sayi);
        }
    }
}
```