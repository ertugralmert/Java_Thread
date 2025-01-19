# Sleep kavramında karşımıza çıkacak bir hata örneği
```java
// bir önceki kod'u kullanabiliriz.
public class Runner_Sleep_Error{ 
    private static long counter = 0;
public static void main(String[] args) {
    final var mainThread = Thread.currentThread();
   
    new Thread(()->{
        for (long i=0; i<200_000_0001L; i++) counter++;
        mainThread.interrupt();
    }).start();

    while(counter<200_000_0000L){
        System.out.println("While Döngüsü Devam eDiyor.");
        try {
            Thread.sleep(1000L);
        }catch (Exception e){
            System.out.println("Beklenmeyen bir hata olustu"+ e);

        }
    }
    
    System.out.println("Program sonlandı");
}
}
```
* çakışmadan doalyı hata fırlatabilirler
* başka bir thread manipilasyonun yapılmasıyla da hata fırlatabilirler