# Thread Kullanım Şekilleri
1. Kural:  ayrı bir iş parçacığında kod çalıştırmak istiyorsanız.  
mutlaka new Thread(); oluşturmalıyız.  
2. Thread çalıştırabileceğiniz kodu functional bir interface olan Runnable tipinde  
talep eder. Bu neden ya new Runnable() sınıf yada bir lambda function veriririz ()->

örnek:  
```java
public class Runner_Thread_KullanimSekilleri{
    public static void main(String[] args) {
        // 1.kural
        new Thread(()->System.out.println("Lambda Function")).start();
        
        // 2.kural
        new Thread(()->{
            int sayi =5;
            sayi = sayi*5;
            System.out.println("say'nin 5 katı: " + sayi);
        }).start();
        
        Runnable rn1 = ()-> System.out.println("MErt");
        Runnable rn2 = ()-> {
            System.out.println("Yeni Runnable Method");
            System.out.println(":))))");
        };
        Thread th1 = new Thread(rn1);
        Thread th2 = new Thread(rn2);
        th1.start();
        th2.start();
    }
}
```
> Runnable kullanmak daha mantıklıdır.
