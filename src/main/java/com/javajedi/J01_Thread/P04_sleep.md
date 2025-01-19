# Sleep Kavrami ve Örnekler
```java
public class Runner {
    public static void main(String[] args) {
        /**
         * Sleep([Long time : milisecond])
         * Thread.sleep(1000L) -> 1 saniye boyunca bekle
         */
        long start = System.currentTimeMillis();
        System.out.println("Uygulama Başladı");
        Thread.sleep(2400L);
        System.out.println("Uygulama Bitti");
        long end = System.currentTimeMillis();
        long duration = end -start;
        System.out.println("gecen sure: "+ duration );
    }
}
```
```java
public class Runner_Sleep_Ornek(){
    static long counter = 0;
    public static void main(String[] args) {
        // Thread ile counter'ı arrıtıroyruz.
        new Thread(()->{
            for (long i=0; i<200_000_0001L; i++) counter++;
        }).start();
        
        //burada da counter ilgili sayıyıa ulaşana kadar döngüyü çalıştırıyoruz.
        while(counter<200_000_0000L){
            System.out.println("While Döngüsü Devam eDiyor.");
            try {
                Thread.sleep(1000L);
            }catch (Exception e){
                
            }
        }
        // yukarıda biri counter sayısını arttırıyor diğer döngüde ise 200milyar
        //olana kadar döngüyü çalıştırıyor.
        System.out.println("Program sonlandı");
    }
}
```