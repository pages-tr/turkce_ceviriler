ISIM
====

zaman-zaman basit bir komut veya kaynak kullanımı vermek

ÖZET
========
**time [**\ *options*\ **]**\ *command*\ **[**\ *arguments...*\ **]**

AÇIKLAMA
===========

**time** komutu belirtilen program *komutunu* verilen argümanlarla çalıştırır. *komut* bittiğinde, **time** bu programın çalışması hakkında zamanlama istatistikleri veren standart hataya bir mesaj yazar. Bu istatistikler (i) çağrı ve sonlandırma arasındaki geçen gerçek zamanı, (ii) kullanıcı CPU zamanını ve (iii) sistem CPU zamanıdır.

Not: Bazı kabukları (ör **bash** \ (1)) zaman ve muhtemelen diğer kaynakların kullanımına ilişkin benzer bilgiler sağlayan bir dahili **time** komutu vardır. Gerçek komuta erişmek için yol adını belirtmeniz gerekebilir (*/usr/bin/time* gibi bir şey).

SEÇENEKLER
=======

 **-p**
    POSIX yerel ayarındayken, kesin geleneksel biçimi kullanın
::

      "real %f\nuser %f\nsys %f\n"
      %f için çıktıdaki ondalık sayıların belirtilmediği ancak saat tikleme doğruluğunu ve en az bir tanesini ifade etmek için yeterli olduğu saniye cinsinden (saniye cinsinden rakamlarla)
      
ÇIKIŞ DURUMU
===========

*komut* çağrıldıysa, çıkış durumu *komut* durumudur.
Aksi takdirde, *komut* bulunamazsa 127, bulunabiliyor ancak çağırılamıyorsa 126 ve başka bir şey ters giderse sıfırdan farklı bir değer (1-125) olur.

ÇEVRE
===========

Çıktının metni ve biçimlendirmesi için **LANG**, **LC_ALL**, **LC_CTYPE**, **LC_MESSAGES**, **LC_NUMERIC** ve **NLSPATH** değişkenleri kullanılır. **PATH**, *komut* aramak için kullanılır. Çıktının metni ve biçimlendirmesi için kalanlar.

GNU SÜRÜMÜ
===========

**time** GNU 1.7 versiyonunun açıklaması aşağıdadır. Yardımcı programın adını göz ardı ederek, GNU, yalnızca kullanılan zamanla ilgili değil, aynı zamanda bellek, G / Ç ve IPC çağrıları (varsa) gibi diğer kaynaklarda da birçok yararlı bilgi vermesini sağlar. Çıktı, *-f* seçeneği veya **TIME** ortam değişkeni kullanılarak belirtilebilen bir biçim dizesi kullanılarak biçimlendirilir.

Varsayılan biçim dizesi:

::

   %Uuser %Ssystem %Eelapsed %PCPU (%Xtext+%Ddata %Mmax)k
   %Iinputs+%Ooutputs (%Fmajor+%Rminor)pagefaults %Wswaps
   
*-p* seçeneği verildiğinde, (taşınabilir) çıktı biçimi kullanılır:

::

   real %e
   user %U
   sys %S
   
Biçim dizesi
-----------------

Biçim normal printf benzeri şekilde yorumlanır. Sıradan karakterler doğrudan kopyalanır, sekme, satırsonu ve ters eğik çizgi \\t, \\n ve \\\ kullanılarak kaçar, yüzde işareti %% ile gösterilir ve aksi takdirde % bir dönüşümü belirtir. **time** programı her zaman bir satırsonu ekler. Ardından dönüşümler yapılır. **tcsh** \ (1) tarafından kullanılanların tümü desteklenmektedir.


**Time**

**%E**
   Geçen gerçek zaman ([saat:] dakika: saniye olarak).

**%e**
   (**tcsh** \ (1) değerinde değildir.) Geçen gerçek zamanlı (saniye olarak).

**%S**
   İşlemin çekirdek modunda geçirdiği toplam CPU-saniye sayısı.

**%U**
    İşlemin kullanıcı modunda geçirdiği toplam CPU-saniye sayısı.

**%P**
    Bu işin aldığı CPU yüzdesi (%U + %S) / %E olarak hesaplanır.

**Memory**

**%M**
   Kbyte cinsinden  işlemin kullanım ömrü boyunca maksimum yerleşik ayarlanan boyutu.

**%t**
    Kbyte cinsinden (**tcsh** \ (1) içinde değil.) Sürecin ortalama yerleşik ayarlanan boyutu.

**%K**
   Kbyte cinsinden işlemin ortalama toplam (veri + yığın + metin) bellek kullanımı.

**%D**
   Kbytes cinsinden sürecin paylaşılmayan veri alanının ortalama boyutu.

**%p**
   (**tcsh** \ (1) içinde değildir.) İşlemin paylaşılmayan yığın alanının Kbytes cinsinden ortalama boyutu.

**%X**
   Kbytes cinsinden sürecin paylaşılan metin alanının ortalama boyutu.

**%Z**
   **tcsh** \ (1) içinde değildir.) Sistemin sayfa boyutu bayt olarak. Bu, sistem başına sabittir, ancak sistemler arasında değişiklik gösterir.

**%F**
    İşlem çalışırken meydana gelen ana sayfa hatalarının sayısı. Bunlar, sayfanın diskten okunması gereken arızalardır.

**%R**
   Küçük veya kurtarılabilir sayfa hatalarının sayısı. Bunlar, geçerli olmayan ancak diğer sanal sayfalar tarafından henüz talep edilmemiş sayfaların hatalarıdır. Bu nedenle sayfadaki veriler hala geçerlidir, ancak sistem tabloları güncellenmelidir.

**%W**
   İşlemin ana bellekten kaç kez değiştirildiği.

**%c**
   Sürecin istemsiz olarak içeriğe geçiş sayısı (zaman diliminin süresi dolduğundan).

**%w**
   Bekleme sayısı: örneğin bir G / Ç işleminin tamamlanmasını beklerken, programın içeriğe gönüllü olarak değiştirildiği süreler.

**I/O**

**%I**
    İşleme göre dosya sistemi girdilerinin sayısı.
    
**%O**
   İşleme göre dosya sistemi çıktılarının sayısı.

**%r**
   İşlem tarafından alınan soket mesajlarının sayısı.

**%s**
   İşlem tarafından gönderilen soket mesajlarının sayısı.

**%k**
   Prosese iletilen sinyal sayısı.

**%C**
   (**tcsh** \ (1) içinde değildir.) Zamanlanan komutun adı ve komut satırı bağımsız değişkenleri.

**%x**
     (**tcsh** \ (1) konumunda değildir.) Komutun durumundan çıkın.
     
GNU seçenekleri
-----------

**-f**\ *format*\ **, --format=**\ *format*
     Muhtemelen TIME ortam değişkeninde belirtilen formatı geçersiz kılan çıktı formatını belirtin.

**-p, --portability**
    Taşınabilir çıktı biçimini kullanın.

**-o**\ *file*\ **, --output=**\ *file*
    Sonuçları * stderr * 'a göndermeyin, ancak belirtilen dosyanın üzerine yazın.

**-a, --append**
   (-O ile birlikte kullanılır.) Üzerine yazmayın, ekleyin.

**-v, --verbose**
    Tüm program hakkında bildikleri çok ayrıntılı çıktılar verin.

**-q, --quiet**
    Anormal program sonlandırmasını (*komut* bir sinyalle sonlandırılır) veya sıfır olmayan çıkış durumunu bildirmeyin.

GNU standart seçenekleri
--------------------

**--help**
    Standart çıktıya bir kullanım mesajı yazdırın ve başarıyla çıkın.

**-V, --version**
   Standart çıktıya sürüm bilgilerini yazdırın, ardından başarıyla çıkın.
   
**--**
   Seçenek listesini sonlandır.
   
BÖCÜK
====

Tüm kaynaklar UNIX'in tüm sürümleri tarafından ölçülmez, bu nedenle bazı değerleri sıfır olarak bildirilebilir. Mevcut seçim çoğunlukla 4.2 veya 4.3BSD tarafından sağlanan verilerden esinlenmiştir.

GNU zaman sürümü 1.7 henüz yerelleştirilmemiştir. Bu nedenle, POSIX gereksinimlerini uygulamaz.

Ortam değişkeni **TIME** kötü seçildi. **autoconf** \ (1) veya **make** \ (1) gibi sistemlerin, kullanılacak yardımcı programı geçersiz kılmak için yardımcı programın adıyla ortam değişkenlerini kullanması olağandışı değildir. Program seçenekleri (program yol adları yerine) için DAHA FAZLA veya ZAMAN gibi kullanımlar zorluklara neden olma eğilimindedir.

*-o* 'un ekleme yerine üzerine yazması talihsiz görünüyor. (Yani, *-a* seçeneği varsayılan olmalıdır.)

GNU **time** için *bug-time@gnu.org* adresine posta önerileri ve hata raporları. Lütfen çalıştırabileceğiniz **time** sürümünü ekleyin.

::

   time --version
   
ve kullandığınız işletim sistemi ve C derleyicisi.

AYRICA BAKINIZ
========

**bash**\ (1), **tcsh**\ (1), **times**\ (2), **wait3**\ (2)
