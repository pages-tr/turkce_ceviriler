İSİM
====

sprof -paylaşılan nesne profili oluşturma verilerini okur ve görüntüler

ÖZET
====

::

   sprof [şeçenek]... paylaşılan-nesne-yolu [profil-veri-yolu]

AÇIKLAMA
========

**sprof** komutu, ilk komut satırı bağımsız değişkeni olarak belirtilen
paylaşılan nesne (paylaşılan kitaplık) için bir profil oluşturma özeti görüntüler.
Profil oluşturma özeti, (isteğe bağlı) ikinci komut satırı bağımsız değişkeninde
önceden oluşturulan profil oluşturma verileri kullanılarak oluşturulur.
Profil oluşturma veri yolu adı atlanırsa, **sprof**, paylaşılan dizinin son
adını kullanarak bu dizini geçerli dizinde *<soname>.profile* adında
bir dosya arayarak bulmaya çalışır.

SEÇENEKLER
==========

Aşağıdaki komut satırı seçenekleri, üretilecek profil çıktısını belirtir:

**-c**, **--call-pairs**
   Paylaşılan nesne tarafından dışa aktarılan arabirimler için çağrı
   yollarının çiftlerinin bir listesini ve her yolun kaç kez
   kullanıldığını yazdırın.

**-p**, **--flat-profile**
   Sayılan ve keneler ile, izlenen nesnedeki tüm işlevlerin düz
   bir profilini oluşturun.

**-q**, **--graph**
   Bir çağrı grafiği oluşturun.

Yukarıdaki seçeneklerden hiçbiri belirtilmezse, varsayılan davranış düz bir
profil ve bir çağrı grafiği görüntülemektir.

Aşağıdaki ek komut satırı seçenekleri kullanılabilir:

**-?**, **--help**
   Komut satırı seçenekleri ve bağımsız değişkenlerinin bir özetini görüntüleyin ve çıkın.

**--usage**
   Kısa bir kullanım özeti yazdırın ve çıkın.

**-V**, **--version**
   **sprof**  için sürüm numarasını, yazdırın.

UYUMLULUK
=========

**sprof** komutu, POSIX.1'de bulunmayan bir GNU parçasıdır.

ÖRNEKLER
========

Aşağıdaki örnek **sprof**'un kullanımını göstermektedir. Örnek, paylaşılan bir
nesnede iki işlevi çağıran bir ana programdan oluşur. İlk olarak, ana programın
kodu:

::

   $ cat prog.c
   #include <stdlib.h>

   void x1(void);
   void x2(void);

   int
   main(int argc, char *argv[])
   {
       x1();
       x2();
       exit(EXIT_SUCCESS);
   }

*x1*\ () ve *x2*\ () işlevleri, paylaşılan nesneyi oluşturmak için
kullanılan aşağıdaki kaynak dosyada tanımlanmıştır:
::

   $ cat libdemo.c
   #include <unistd.h>

   void
   consumeCpu1(int lim)
   {
       int j;

       for (j = 0; j < lim; j++)
   	getppid();
   }

   void
   x1(void) {
       int j;

       for (j = 0; j < 100; j++)
   	consumeCpu1(200000);
   }

   void
   consumeCpu2(int lim)
   {
       int j;

       for (j = 0; j < lim; j++)
   	getppid();
   }

   void
   x2(void)
   {
       int j;

       for (j = 0; j < 1000; j++)
   	consumeCpu2(10000);
   }

Şimdi paylaşılan nesneyi *libdemo.so.1.0.1* ve soname *libdemo.so.1* ile oluşturuyoruz:
::

   $ cc -g -fPIC -shared -Wl,-soname,libdemo.so.1 \
           -o libdemo.so.1.0.1 libdemo.c

Sonra kütüphane soname ve kütüphane linker ismi için sembolik bağlantılar kurarız:

::

   $ ln -sf libdemo.so.1.0.1 libdemo.so.1
   $ ln -sf libdemo.so.1 libdemo.so

Ardından, ana programı derleyerek paylaşılan nesneye bağlar ve programın dinamik
bağımlılıklarını listeleriz:

::

   $ cc -g -o prog prog.c -L. -ldemo
   $ ldd prog
   	linux-vdso.so.1 =>  (0x00007fff86d66000)
   	libdemo.so.1 => not found
   	libc.so.6 => /lib64/libc.so.6 (0x00007fd4dc138000)
   	/lib64/ld-linux-x86-64.so.2 (0x00007fd4dc51f000)

Paylaşılan nesne için profil oluşturma bilgileri almak üzere **LD_PROFILE**
ortam değişkenini kütüphanenin son adıyla tanımlarız:

::

   $ export LD_PROFILE=libdemo.so.1

Ardından **LD_PROFILE_OUTPUT** ortam değişkenini, profil çıktısının yazılması
gereken dizinin yol adıyla tanımlarız ve zaten yoksa bu dizini oluştururuz:

::

   $ export LD_PROFILE_OUTPUT=$(pwd)/prof_data
   $ mkdir -p $LD_PROFILE_OUTPUT

**LD_PROFILE** profil oluşturma çıktısının zaten varsa çıktı dosyasına
*eklenmesine* neden olur, bu nedenle önceden var olan profil oluşturma
verilerinin olmadığından emin oluruz:

::

   $ rm -f $LD_PROFILE_OUTPUT/$LD_PROFILE.profile

Daha sonra programı, **LD_PROFILE_OUTPUT** 'da belirtilen dizindeki bir dosyaya
yazılan profil oluşturma çıktısını üretmek için çalıştırırız:

::

   $ LD_LIBRARY_PATH=. ./prog
   $ ls prof_data
   libdemo.so.1.profile

Daha sonra sayım ve kenelerle düz bir profil oluşturmak için **sprof -p**
seçeneğini kullanırız:

::

   $ sprof -p libdemo.so.1 $LD_PROFILE_OUTPUT/libdemo.so.1.profile
   Flat profile:

   Each sample counts as 0.01 seconds.
     %   cumulative   self              self     total
    time   seconds   seconds    calls  us/call  us/call  name
    60.00      0.06     0.06      100   600.00           consumeCpu1
    40.00      0.10     0.04     1000    40.00           consumeCpu2
     0.00      0.10     0.00        1     0.00           x1
     0.00      0.10     0.00        1     0.00           x2


** sprof-q** seçeneği bir arama grafiği oluşturur:

::

   $ sprof -q libdemo.so.1 $LD_PROFILE_OUTPUT/libdemo.so.1.profile

   index % time    self  children    called     name

                   0.00    0.00      100/100         x1 [1]
   [0]    100.0    0.00    0.00      100         consumeCpu1 [0]
   -----------------------------------------------
                   0.00    0.00        1/1           <UNKNOWN>
   [1]      0.0    0.00    0.00        1         x1 [1]
                   0.00    0.00      100/100         consumeCpu1 [0]
   -----------------------------------------------
                   0.00    0.00     1000/1000        x2 [3]
   [2]      0.0    0.00    0.00     1000         consumeCpu2 [2]
   -----------------------------------------------
                   0.00    0.00        1/1           <UNKNOWN>
   [3]      0.0    0.00    0.00        1         x2 [3]
                   0.00    0.00     1000/1000        consumeCpu2 [2]
   -----------------------------------------------

Yukarıda ve aşağıda, "<UNKNOWN>" dizeleri profilli nesnenin dışındaki
tanımlayıcıları temsil eder (bu örnekte, bunlar *main()* örnekleridir).

**sprof -c** seçeneği, çağrı çiftlerinin bir listesini ve gerçekleşme
sayısını oluşturur:

::

   $ sprof -c libdemo.so.1 $LD_PROFILE_OUTPUT/libdemo.so.1.profile
   <UNKNOWN>                  x1                                 1
   x1                         consumeCpu1                      100
   <UNKNOWN>                  x2                                 1
   x2                         consumeCpu2                     1000

AYRICA BAKINIZ
==============

**gprof**\ (1), **ldd**\ (1), **ld.so**\ (8)
