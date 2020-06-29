ADI
====

ldd - paylaşılan nesne bağımlılıklarını yazdır

ÖZET
========

**ldd** [*seçenek*] ... *dosya* ...

AÇIKLAMA
===========

**ldd**, her program için gereken paylaşılan nesneleri (paylaşılan kütüphaneler) veya komut satırında belirtilen paylaşılan nesneyi yazdırır. Kullanımı ve çıktısının bir örneği aşağıdadır:

::

   $ ldd /bin/ls
           linux-vdso.so.1 (0x00007ffcc3563000)
           libselinux.so.1 => /lib64/libselinux.so.1 (0x00007f87e5459000)
           libcap.so.2 => /lib64/libcap.so.2 (0x00007f87e5254000)
           libc.so.6 => /lib64/libc.so.6 (0x00007f87e4e92000)
           libpcre.so.1 => /lib64/libpcre.so.1 (0x00007f87e4c22000)
           libdl.so.2 => /lib64/libdl.so.2 (0x00007f87e4a1e000)
           /lib64/ld-linux-x86-64.so.2 (0x00005574bf12e000)
           libattr.so.1 => /lib64/libattr.so.1 (0x00007f87e4817000)
           libpthread.so.0 => /lib64/libpthread.so.0 (0x00007f87e45fa000)

Normal durumda, **ldd**, **LD_TRACE_LOADED_OBJECTS** ortam değişkeni 1 olarak ayarlandığında standart dinamik bağlayıcıyı (bkz. **ld.so** \ (8)) çağırır. Bu, dinamik bağlayıcının programın dinamikini denetlemesine neden olur (**ld.so** \ (8)) bölümünde açıklanan kurallara göre bulun ve bu bağımlılıkları sağlayan nesneleri yükleyin. Her bağımlılık için, **ldd** eşleşen nesnenin konumunu görüntüler ve (onaltılık) adresin yüklendiği adres. (*linux-vdso* ve *ld-linux* paylaşılan bağımlılıkları özeldir; bkz. **vdso** \ (7) ve **ld.so** \ (8 )).

Güvenlik
--------

Bazı durumlarda (örneğin, programın * ld-inux.so * dışında bir ELF yorumlayıcısı belirttiği durumlarda), ** ldd ** 'nin bazı sürümlerinin, programı doğrudan yürütmeye çalışarak bağımlılık bilgilerini almaya çalışabileceğini unutmayın. bu da programın ELF yorumlayıcısında tanımlanan kodların yürütülmesine ve belki de programın kendisinin yürütülmesine yol açabilir. (2.27'den önceki glibc sürümlerinde, yukarı dağıtım ** ldd ** uygulaması bunu yaptı, ancak çoğu dağıtımda değiştirilmemiş bir sürüm sağlandı.)

Bu nedenle, rastgele kod çalıştırılmasına neden olabileceğinden, güvenilir olmayan bir yürütülebilir dosya üzerinde * hiçbir zaman * ldd ** kullanmamalısınız. Güvenilmeyen yürütülebilir dosyalar ile uğraşırken daha güvenli bir alternatif:

::

   $ objdump -p /path/to/program | grep NEEDED
   
OPTIONS
=======

**--version**
   **ldd** sürüm numarasını yazdırın.

**-v**, **--verbose**
   Sembol sürüm bilgisi dahil tüm bilgileri yazdırın.
   
**-u**, **--unused**
   Kullanılmayan doğrudan bağımlılıkları yazdırın. (Glibc 2.3.4'ten beri.)

**-d**, **--data-relocs**
   Yer değiştirme yapın ve eksik nesneleri rapor edin (yalnızca ELF).

**-r**, **--function-relocs**
   Hem veri nesneleri hem de işlevler için yer değiştirme gerçekleştirin ve eksik nesneleri ya da işlevleri rapor edin (yalnızca ELF).

**--help**
    Kullanım bilgileri.

BÖCEK
====

**ldd**, a.out paylaşılan kitaplıklarında çalışmaz.

**ldd**, derleyici sürümlerine **ldd** desteği eklenmeden önce oluşturulmuş bazı son derece eski a.out rogramları ile çalışmaz. Bu programlardan birinde **ldd** kullanırsanız, program *argc* = 0 ile çalışmayı dener ve sonuçlar tahmin edilemez olur.

AYRICA BAKINIZ
========

**pldd**\ (1), **sprof**\ (1), **ld.so**\ (8), **ldconfig**\ (8)
