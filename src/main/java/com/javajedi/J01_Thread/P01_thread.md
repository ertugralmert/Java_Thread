# Concurrency - Eşzamanlılık
Tüm PC kullanıcıları, bilgisayarın aynı anda bir çok işlemi  
yapmasını bekler. Örneğin müzik dinliyorken kod yazmak.  
Java dili, 5.0 sürümündne bu tarafa java.util.concurrecy kitaplığı  
ile bunu desteklemektedir.  
Multithread olarakta geçer.  
Çoklu iş parçacığı ile işlemleri senkron bir şekilde yapabiliriz.  
Kendi yazdığımız Java Runner uygulamalarını düşündüğümüzde de bu uygulamalar  
bir thread üzerinde çalışıyor olmalılar. İşte bu, java main programlarımız  
MainThread denilen thread üzerinde çalışırlar.  
Çok basit bir kavramda ifade edicek olursak.  
```java
public class Runner {
    public static void main(String[] args) {
        //Runable method ile Thread olarak çalıştıracağız 
        /**
         * new thread ile thread oluşturduk ve iki for döngüsü aynı anda
         * çalışmaya başladı. En alttaki for döngünü mainThread ile çalıştı
         * üstteki for yeni thread ile oluşturulup çalıştı.
         */
        new Thread(()->{
            for(int i = 0; i<10; i++){
                System.out.println("döngü: "+i);
                try{
                    Thread.sleep(500L);
                }catch (InterruptedException e){
                    throw new RuntimeException(e);
                }
            }
        }).start();
        
        
        for (int i = 0; i < 50; i++) {
            System.out.println("*" );
            Thread.sleep(700L);
        }
    }
}

```