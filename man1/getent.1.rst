İSİM
====

getent - İsim Hizmet Anahtarı (Name Service Switch) kitaplıklarından giriş alma

ÖZET
========

**getent [seçenek]... veritabanı anahtarı...**

AÇIKLAMA
===========

**getent** komutu, İsim Hizmeti Anahtarı kitaplıkları tarafından desteklenen ve */etc/nsswitch.conf*
içinde yapılandırılan veritabanlarındaki girdileri görüntüler. Bir veya daha fazla *anahtar değişken*
sağlanırsa, yalnızca verilen tuşlarla eşleşen girişler görüntülenir.

*veritabanı*, GNU C Kütüphanesi tarafından desteklenenlerden herhangi biri olabilir.
Desteklenen *veritabanları* aşağıda listelenmiştir:

   **ahosts**
      Herhangi bir *anahtar* verilmediği takdirde, 
      sunucu veritabanlarını dökümlemek için **sethostent**\ (3),
      **gethostent**\ (3), ve **endhostent**\ (3)
      komutlarını kullanın.
      
      Bu, **sunucular** için aynıdır. Bir veya daha fazla *anahtar* bağımsız değişkeni sağlandığında, her *anahtarını* arka arkaya **getaddrinfo**\ (3) **AF_UNSPEC** adres ailesiyle iletin ve döndürülen her yuva adresi yapısını numaralandırın.

   **ahostsv4**
      **ahosts** ile aynıdır, ancak **AF_INET** adres ailesini kullanır.
      
   **ahostsv6**
      **ahosts** ile aynıdır, ancak **AF_INET6** adres ailesini kullanır. Bu durumda **getaddrinfo**\ (3) çağrısı **AI_V4MAPPED** bayrağını içerir.
      
   **aliases**
      Komut için *anahtar* sağlanmadığında, takma ad veritabanını numaralandırmak için **setaliasent**\ (3), **getaliasent**\ (3) ve **endaliasent**\ (3) kullanın. Bir veya daha fazla *anahtar* bağımsız değişkeni sağlandığında, her *anahtar* değerini art arda **getaliasbyname**\ (3) öğesine iletin ve sonucu görüntüleyin.

   **ethers**
      Bir veya daha fazla *anahtar* argümanı sağlandığında, her *anahtar* değerini art arda sonuç elde edilene kadar **ether_aton**\ (3) ve **ether_hostton**\ (3) 'e geçirin ve sonucu görüntüleyin. Numaralandırma **ethers** üzerinde desteklenmediği için bir *anahtar* argüman sağlanmalıdır.

   **group**
      Hiçbir *anahtar* sağlanmadığında, grup veritabanını numaralandırmak için **setgrent**\ (3), **getgrent**\ (3) ve **endgrent**\ (3) kullanın. Bir veya daha fazla *anahtar* bağımsız değişkeni sağlandığında, her sayısal *anahtarı* **getgrgid**\ (3) üzerine ve sayısal olmayan her *anahtarı* **getgrnam**\ (3) üzerine iletin ve sonucu görüntüleyin.

   **gshadow**
      Hiçbir *anahtar* sağlanmadığında, gshadow veritabanını numaralandırmak için **setsgent**\ (3), **getsgent**\ (3) ve **endsgent**\ (3) kullanın. Bir veya daha fazla *anahtar* bağımsız değişkeni sağlandığında, her *anahtar* değerini arka arkaya **getsgnam**\ (3) öğesine iletin ve sonucu görüntüleyin.

   **hosts**
      Hiçbir *anahtar* sağlanmadığında, anasistem veritabanını numaralandırmak için **sethostent**\ (3), **gethostent**\ (3) ve **endhostent**\ (3) kullanın. 
      Bir veya daha fazla *anahtar* bağımsız değişkeni sağlandığında, **inet_pton**\ 'a bir çağrının yapılmasına bağlı olarak her *anahtarı* **gethostbyaddr**\ (3) veya **gethostbyname2**\ (3) öğesine iletin. 3) *anahtar*'ın bir IPv6 veya IPv4 adresi olduğunu veya olmadığını gösterir ve sonucu görüntüleyin.

   **initgroups**
      Bir veya daha fazla *anahtar* bağımsız değişkeni sağlandığında, her *anahtar*'ı arka arkaya **getgrouplist**\ (3) öğesine iletin ve sonucu görüntüleyin. **initgroup** öğesinde numaralandırma desteklenmediği için *anahtar* değer sağlanmalıdır.

   **netgroup**
      Bir *anahtar* sağlandığında, *anahtar* değeri **setnetgrent**\ (3) 'e geçirin ve **getnetgrent**\ (3) tuşunu kullanarak elde edilen dizeyi üçlü olarak getirin (*hostname*, *username*, *domainname*). Alternatif olarak, **innetgr**\ (3) aracılığıyla bir netgroup adıyla eşleşmek üzere *hostname*, *username* ve *domainname* olarak yorumlanan üç *anahtar* sağlanabilir. Numaralandırma **netgroup** üzerinde desteklenmediğinden, bir veya üç *anahtar* sağlanmalıdır.

   **networks**
      Hiçbir *anahtar* sağlanmadığında, ağ veritabanını numaralandırmak için **setnetent**\ (3), **getnetent**\ (3) ve **endnetent**\ (3) kullanın. Bir veya daha fazla *anahtar* bağımsız değişkeni sağlandığında, her sayısal *anahtar*'ı **getnetbyaddr**\ (3) 'e ve sayısal olmayan her *anahtar*'ı **getnetbyname**\ (3)' e iletin ve sonucu görüntüleyin.

   **passwd**
      Hiçbir *anahtar* sağlanmadığında, passwd veritabanını numaralandırmak için **setpwent**\ (3), **getpwent**\ (3) ve **endpwent** \ (3) kullanın. Bir veya daha fazla *anahtar* bağımsız değişkeni sağlandığında, her sayısal *anahtar*'ı **getpwuid**\ (3)'e ve sayısal olmayan her *anahtar*'ı **getpwnam**\ (3)' e iletin ve sonucu görüntüleyin.

   **protocols**
      Hiçbir *anahtar* sağlanmadığında, protokol veritabanını numaralandırmak için ** setprotoent ** \ (3), ** getprotoent ** \ (3) ve ** endprotoent ** \ (3) kullanın. Bir veya daha fazla * anahtar * bağımsız değişkeni sağlandığında, her sayısal * anahtarı * ** almak için ** getprotobynumber ** \ (3) ve sayısal olmayan her * anahtarı * almak için ** getprotobyname ** \ (3) ve sonucu görüntüleyin.

   **rpc**
      Hiçbir *anahtar* sağlanmadığında, rpc veritabanını numaralandırmak için **setrpcent**\ (3), **getrpcent**\ (3) ve **endrpcent**\ (3) kullanın. Bir veya daha fazla *anahtar* bağımsız değişkeni sağlandığında, her sayısal *anahtar*'ı **getrpcbynumber**\ (3) 'e ve sayısal olmayan her *anahtar*'ı **getrpcbyname**\ (3)' e iletin ve sonucu görüntüleyin.

   **services**
     Hiçbir *anahtar* sağlanmadığında, hizmetler veritabanını numaralandırmak için **setservent**\ (3), **getservent**\ (3) ve **endervent**\ (3) kullanın. Bir veya daha fazla *anahtar* bağımsız değişkeni sağlandığında, her sayısal *anahtarı* **getservbynumber**\ (3) ve sayısal olmayan her *anahtarı* **getservbyname**\ (3) olarak geçirin ve sonucu görüntüleyin.

   **shadow**
       Hiçbir *anahtar* sağlanmadığında, gölge veritabanını numaralandırmak için **setspent**\ (3), **getspent**\ (3) ve **endspent**\ (3) kullanın. Bir veya daha fazla *anahtar* argümanı sağlandığında, her *anahtarı* art arda **getspnam** \ (3) öğesine iletin ve sonucu görüntüleyin.
       
SEÇENEKLER
==========

**-s service**, **-service service **
   Belirtilen hizmetle **(service)** tüm veritabanlarını geçersiz kılın. (Glibc 2.2.5'den beri.)
   
**-s database:service**, **--service database:service**
   Yalnızca belirtilen hizmetle belirtilen veritabanlarını geçersiz kıl.Bu seçenek birden çok kez kullanılabilir, ancak her biri için yalnızca son hizmet veritabanını kullanılacaktır. (Glibc 2.4'ten beri.)

**-i**, **--no-idn**
   **ahosts**/**getaddrinfo**\ (3) aramalarında IDN kodlamasını devre dışı bırakır
   (Glibc-2.13'ten beri.)

**-?**, **--help**
   Bir kullanım özeti yazdırın ve çıkın.

**--usage**
   Kısa bir kullanım özeti yazdırın ve çıkın.

**-V**, **--version**
   İçin sürüm numarasını, lisansı ve feragatnameyi yazdırın
   **getent**.

ÇIKIŞ DURUMU
============

Aşağıdaki çıkış değerlerinden biri **getent** tarafından döndürülebilir:

   **0**
      Komut başarıyla tamamlandı.

   **1**
      Eksik argümanlar veya *veritabanı* bilinmiyor.

   **2**
      Bir veya daha fazla sağlanan *anahtar*, *veritabanı*'nda bulunamadı.

   **3**
      Numaralandırma bu *veritabanı*'nda desteklenmez.

AYRICA BAKINIZ
========

**nsswitch.conf**\ (5)
