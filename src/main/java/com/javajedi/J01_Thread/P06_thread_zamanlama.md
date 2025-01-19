# Zamanlama 
Java kodu üzerinden anlatmak daha doğru olur.

```java
import java.util.concurrent.ScheduledExecutorService;
import java.util.concurrent.ScheduledFuture;
import java.util.concurrent.TimeUnit;

public class Runner_Thread_Zamanlama {
    private static long start;

    public static void main(String[] args) {
        start = System.currentTimeMillis();
        Runnable rn1 = () -> {
            System.out.println("Görev-1 başladı");
            System.out.println("Görev-1 tamanlandı " + (System.currentTimeMillis() - start));

        };
        Runnable rn2 = () -> {
            System.out.println("Görev 2 başladı");
            System.out.println("Görev 2 tamamlandı " + (System.currentTimeMillis() - start));
        };

        // Bir kavramımız var.
        
        try(ScheduledExecutorService executorService = Executors.newSingleThreadScheduledExecutor()){
            ScheduledFuture<?> sc1 = executorService.schedule(rn1, 8, TimeUnit.SECONDS); // runnable, ne zaman sonra mı başlasın, zamanın cinsi
            ScheduledFuture<?> sc2 = executorService.schedule(rn2, 3, TimeUnit.SECONDS); // runnable, ne zaman sonra mı baise> executorService.schedule(rn2, 3, TimeUnit.SECONDS);

        }
        
    }
}
```