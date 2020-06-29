NAME
====

memusage - bir programın profil belleği kullanımı

SYNOPSIS
========

**memusage** [*option*]... *program* [*programoption*]...

AÇIKLAMA
========

**memusage**, programın *program* bellek kullanımını profilleyen bir bash betiğidir. **libmemusage.so** kütüphanesini arayanın ortamına önceden yükler (**LD_PRELOAD** ortam değişkeni üzerinden; bkz. **ld.so**\ (8)). **libmemusage.so** kütüphanesi, **malloc**\ (3), **calloc**\ (3), **free**\ (3) ve **realloc**\ (3) çağrılarını keserek bellek ayırmayı izler ; isteğe bağlı olarak, **mmap**\ (2), **mremap**\ (2) ve **munmap**\ (2) çağrılarına da müdahale edilebilir.

**memusage**, toplanan verileri metin biçiminde çıktılayabilir veya **memusagestat**\ (1) kullanabilir (aşağıdaki **- p** seçeneğine bakın), grafik resmini içeren bir PNG dosyası oluşturmak için toplanan veri.

Bellek kullanımı özeti
----------------------

**memusage** tarafından "Bellek kullanım özeti" satır çıkışı üç alan içerir:

    **heap total** (**yığın toplamı**)
       Tüm **malloc**\ (3) çağrılarının *size* argümanlarının toplamı, tüm **calloc**\ (3) çağrılarının argümanlarının (*nmemb*\ \*\ *size*) toplamı ve toplamı *uzunluk* tüm **mmap**\ (2) çağrılarının argümanları. **realloc**\ (3) ve **mremap**\ (2) durumunda, bir tahsisatın yeni boyutu önceki boyuttan büyükse, tüm bu farklılıkların toplamı (yeni boyut eksi eski boyut ) eklenir.

    **heap peak** (**yığın zirvesi **)
       Tüm **malloc**\ (3) çağrılarının *size* argümanları, **calloc**\ (3)' in *nmemb*\ \*\ *size* tüm ürünleri, tüm *size* argümanları **realloc**\ (3), **mmap**\ (2) 'nin *uzunluk* argümanları ve **mremap**\ (2)' nin yeni boyut argümanları arasında en büyüğü olanıdır.

    **stack peak** (**yığının tepesi**)
       İzlenen herhangi bir işleve ilk çağrı yapılmadan önce, yığın işaretçisi adresi (temel yığın işaretçisi) kaydedilir. Her işlev çağrısından sonra, gerçek yığın işaretçi adresi okunur ve temel yığın işaretçisinden fark hesaplanır. Bu farklılıkların en büyüğü yığının tepe noktasıdır.

Bu özet satırının hemen ardından bir tablo, her bir yakalanan işlev için numara çağrılarını, ayrılan veya ayrılan toplam belleği ve başarısız arama sayısını gösterir. **realloc**\ (3) ve **mremap**\ (2) için, ek "nomove" alanı, bir bloğun adresini değiştiren yeniden tahsisleri ve ek "dec" alanı, boyutu azaltan yeniden tahsisleri gösterir blok. **realloc**\ (3) için, "free" ek alanı, bir bloğun serbest bırakılmasına neden olan yeniden tahsisleri gösterir (yani, yeniden tahsis edilen boyut 0'dır).

**memusage** tarafından gönderilen tablo çıktısının "boş/toplam bellek", **realloc** \ (3) öğesinin, bir bellek bloğunun öncekinden daha küçük bir boyuta yeniden tahsis edilmesi için kullanıldığı durumları yansıtmaz. Bu, tüm "toplam bellek" hücrelerinin ("boş" hariç) toplamının "boş/toplam bellek" hücresinden daha büyük olmasına neden olabilir.

Blok boyutları için histogram
-----------------------------

"Blok boyutları için histogram" çeşitli bellek boyutlarına bellek ayırmalarının dökümünü sağlar.

SEÇENEKLER
==========

**-n**\ *name*\ **, --progname=**\ *name*
   Profile program dosyasının adı.

**-p**\ *dosya*\ **, --png=**\ *dosya*
   PNG formatında grafik çizdirir ve onu *dosya* isimli dosyaya yazdırır.

**-d**\ *dosya*\ **, --data=**\ *dosya*
   Grafiği ikili formatta veri dosyasına aktarır ve onu *dosya* isimli dosyaya yazdırır.

**-u, --unbuffered**
   Çıktıyı arabelleğe alma.

**-b**\ *boyut*\ **, --buffer=**\ *boyut*
   Yazmadan önce *boyut* girişleri toplayın.

**--no-timer**
   Yığın işaretçi değeri zamanlayıcı tabanlı (**SIGPROF**) örneklemeyi devre dışı bırakın.

**-m, --mmap**
   Ayrıca **mmap**\ (2), **mremap**\ (2) ve **munmap**\ (2) öğelerini de izleyin.

**-?**, **--help**
  Bir kullanım özeti yazdırın ve çıkın.

**--usage**
  Kısa bir kullanım özeti yazdırın ve çıkın.

**-V**, **--version**
  **memusage** için sürüm numarasını, yazdırın.

Aşağıdaki seçenekler yalnızca grafik çıktısı oluşturulurken geçerlidir:

**-t, --time**
  Yatay eksende sınırlandırma ölçeği olarak belirli bir zamanı (işlev çağrılarının sayısı yerine) kullanın.

**-T, --total**
  Ayrıca toplam bellek tüketiminin bir grafiğini çizin.

**--title=**\ *isim*
  Grafiğin başlığı olarak *isim* değişkenini kullanın.

**-x**\ *boyut*\ **, --x-size=**\ *boyut*
  Çıktı grafiğini *boyut* piksel genişliğinde yapın.

**-y**\ *boyut*\ **, --y-size=**\ *boyut*
  Çıktı grafiğini *boyut* piksel yüksekliğinde yapın.


ÇIKIŞ DURUMU
============

Çıkış durumu, profilli programın çıkış durumuna eşittir.

BÖCEK
=====

Hata raporlama talimatları için lütfen şu adrese bakın:
`<http://www.gnu.org/software/libc/bugs.html>`__.

ÖRNEKLER
========

Aşağıda, bir bellek bloğunu daha önce zirveye yükselen döngüler halinde yeniden tahsis eden ve daha sonra belleği sıfıra dönen daha küçük bloklarda döngüsel olarak yeniden tahsis eden basit bir program bulunmaktadır. Programı derledikten ve aşağıdaki komutları çalıştırdıktan sonra, programın bellek kullanımının bir grafiği *memusage.png* dosyasında bulunabilir:

::

   $ memusage --data=memusage.dat ./a.out
   ...
   Memory usage summary: heap total: 45200, heap peak: 6440, stack peak: 224
           total calls  total memory  failed calls
    malloc|         1           400             0
   realloc|        40         44800             0  (nomove:40, dec:19, free:0)
    calloc|         0             0             0
      free|         1           440
   Histogram for block sizes:
     192-207             1   2% ================
   ...
    2192-2207            1   2% ================
    2240-2255            2   4% =================================
    2832-2847            2   4% =================================
    3440-3455            2   4% =================================
    4032-4047            2   4% =================================
    4640-4655            2   4% =================================
    5232-5247            2   4% =================================
    5840-5855            2   4% =================================
    6432-6447            1   2% ================
   $ memusagestat memusage.dat memusage.png

Program kaynağı
---------------

::

   #include <stdio.h>
   #include <stdlib.h>

   #define CYCLES 20

   int
   main(int argc, char *argv[])
   {
        int i, j;
        int *p;

        printf("malloc: %zd\n", sizeof(int) * 100);
        p = malloc(sizeof(int) * 100);

        for (i = 0; i < CYCLES; i++) {
            if (i < CYCLES / 2)
                j = i;
            else
                j--;

            printf("realloc: %zd\n", sizeof(int) * (j * 50 + 110));
            p = realloc(p, sizeof(int) * (j * 50 + 100));

            printf("realloc: %zd\n", sizeof(int) * ((j+1) * 150 + 110));
            p = realloc(p, sizeof(int) * ((j + 1) * 150 + 110));
        }

        free(p);
        exit(EXIT_SUCCESS);
   }


AYRICA BAKINIZ
==============

**memusagestat**\ (1), **mtrace**\ (1), **ld.so**\ (8)
