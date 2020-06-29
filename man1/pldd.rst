İSİM
====

pldd - bir sürece bağlı dinamik paylaşılan nesneleri görüntüler

ÖZET
====
::

   pldd pid
   pldd option

AÇIKLAMA
========

**pldd** komutu, sürece belirtilen işlem kimliğiyle (PID) bağlanan dinamik paylaşılan nesnelerin (DSO) bir listesini görüntüler. Liste, **dlopen** \ (3) kullanılarak dinamik olarak yüklenen kütüphaneleri içerir.

SEÇENEKLER
=======

**-?**, **--help**
  Bir yardım mesajı görüntüleyin ve çıkın.

**--usage**
     Kısa kullanım mesajı görüntüleyin ve çıkın.

**-V**, **--version**
    Program sürüm bilgilerini görüntüleyin ve çıkın.

ÇIKIŞ DURUMU
===========

Başarılı olduğunda, **pldd** 0 durumundan çıkar. Belirtilen işlem yoksa, kullanıcının dinamik paylaşılan nesne listesine erişme izni yoktur veya komut satırı bağımsız değişkeni sağlanmaz, **pldd** 1 durumu vardır. Geçersiz bir seçenek verilirse 64 durumundan çıkar.


SÜRÜMLER
========

**pldd**, glibc 2.15'ten beri kullanılabilir.

UYGUNLUK
=============

**pldd** komutu POSIX.1 tarafından belirtilmemiştir. Diğer bazı sistemlerde de benzer bir komut vardır.

NOTLAR
=====

Komut

::

   lsof -p PID

ayrıca bir sürece bağlanan dinamik paylaşılan nesneleri içeren çıktıyı da gösterir.

**gdb** \ (1) *info shared* komutu ayrıca bir işlem tarafından kullanılan paylaşılan kitaplıkları da gösterir, böylece aşağıdakiler gibi bir komut kullanarak **pldd** 'ye benzer çıktılar elde edilebilir ( *pid* ile belirtilen işlem):

::

   $ gdb -ex "set confirm off" -ex "set height 0" -ex "info shared" \
           -ex "quit" -p $pid | grep '^0x.*0x'

BÖCÜK
====

Glibc 2.19'dan 2.29'a, **pldd** kırıldı: yürütüldüğünde asıldı. Bu sorun glibc 2.30'da giderilmiştir ve düzeltme bazı dağıtımlarda önceki glibc sürümlerine bildirilmiştir.

ÖRNEKLER:
========

::

   $ echo $$               # Kabuğun PID'sini görüntüle
   1143
   $ pldd $$               # Kabuğa bağlı DSO'ları görüntüleme
   1143:   /usr/bin/bash
   linux-vdso.so.1
   /lib64/libtinfo.so.5
   /lib64/libdl.so.2
   /lib64/libc.so.6
   /lib64/ld-linux-x86-64.so.2
   /lib64/libnss_files.so.2

AYRICA BAKINIZ
========

**ldd**\ (1), **lsof**\ (1), **dlopen**\ (3), **ld.so**\ (8)
