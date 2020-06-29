İSİM
====

çatal - alt işlem oluştur

ÖZET
========

| **#include <sys/types.h>**
| **#include <unistd.h>**

**pid_t fork(void);**

AÇIKLAMA
===========

**fork**\ () çağrı sürecini çoğaltarak yeni bir süreç oluşturur. Yeni işleme *child* işlemi denir. Çağıran işlem *üst* işlem olarak adlandırılır.

Alt işlem ve üst işlem ayrı bellek alanlarında çalışır. **fork**\ () sırasında her iki bellek alanı da aynı içeriğe sahiptir. İşlemlerden biri tarafından yapılan bellek yazma işlemleri, dosya eşlemeleri (**mmap**\ (2)) ve eşleştirmeler (**munmap**\ (2)) diğerini etkilemez.

Alt süreç, aşağıdaki noktalar dışında ana sürecin tam bir kopyasıdır:

- Çocuğun kendine özgü bir işlem kimliği vardır ve bu PID, varolan herhangi bir işlem grubunun (**setpgid**\ (2)) veya oturumun kimliğiyle eşleşmez.

- Çocuğun üst işlem kimliği, üst öğenin işlem kimliğiyle aynı.
- Çocuk ebeveyninin bellek kilitlerini devralmaz (**mlock**\ (2), **mlockall**\ (2)).

- İşlem kaynağı kullanımları (**getrusage**\ (2)) ve CPU zaman sayaçları (**kez**\ (2)) çocukta sıfırlanır.

- Çocuğun beklemede olan sinyaller kümesi başlangıçta boştur (**işaretleme **\ (2)).

- Çocuk semafor ayarlamalarını üst öğesinden devralmaz (**semop**\ (2)).

- Çocuk, işlemle ilişkili kayıt kilitlerini üst öğesinden devralmaz (**fcntl**\ (2)). (Öte yandan, **fcntl**\ (2) açık dosya açıklama kilitlerini ve **sürü**\ (2) kilitlerini üst öğesinden devralır.)

- Çocuk zamanlayıcıları üst öğesinden devralmaz (**setitimer**\ (2), **alarm**\ (2), **timer_create**\ (2)).

- Çocuk olağanüstü eşzamansız G / Ç işlemlerini üst öğesinden (**aio_read**\ (3), **aio_write**\ (3)) miras almaz veya üst öğesinden herhangi bir eşzamansız G / Ç bağlamını devralmaz (bkz. **io_setup**\ (2)).

Yukarıdaki listedeki işlem özniteliklerinin tümü POSIX.1'de belirtilmiştir. Ebeveyn ve çocuk ayrıca aşağıdaki Linux'a özgü işlem özelliklerine göre farklılık gösterir:

- Çocuk dizin değişiklik bildirimlerini üst öğesinden devralmaz (dnotify) (**fcntl**\ (2) içindeki **F_NOTIFY** açıklamasına bakın).

- **prctl**\ (2) **PR_SET_PDEATHSIG** ayarı sıfırlanır, böylece üst öğe sona erdiğinde çocuk bir sinyal almaz.

- Varsayılan zamanlayıcı gevşeme değeri, ebeveynin geçerli zamanlayıcı gevşeme değerine ayarlanır. **prctl**\ (2) içindeki **PR_SET_TIMERSLACK** açıklamasına bakın.

- **madvise**\ (2) **MADV_DONTFORK** bayrağıyla işaretlenmiş bellek eşlemeleri **çatal**\ () üzerinden devralınmamıştır.

- Adres aralıkları ile işaretlenmiş bellek
   **madvise**\ (2) **MADV_WIPEONFORK** bayrağı **çatal**\ () sonrasında çocukta sıfırlanır. (**MADV_WIPEONFORK** ayarı, çocuktaki bu adres aralıkları için yerinde kalır.)

- Çocuğun sonlandırma sinyali daima **SIGCHLD** (bkz. **klon**\ (2)).

- **ioperm**\ (2) tarafından ayarlanan bağlantı noktası erişim izni bitleri çocuk tarafından miras alınmaz; çocuk **ioperm**\ (2) kullanarak ihtiyaç duyduğu tüm parçaları açmalıdır.

Aşağıdaki hususlara dikkat edin:

- Alt işlem, tek bir iş parçacığıyla oluşturulur; bu işlem **çatal**\ () olarak adlandırılır. Ebeveynin tüm sanal adres alanı, mutekslerin durumu, koşul değişkenleri ve diğer pthreads nesneleri dahil olmak üzere çocukta çoğaltılır; **pthread_atfork**\ (3) kullanımı, bunun neden olabileceği sorunların çözümünde yardımcı olabilir.

- Çok iş parçacıklı bir programdaki **fork**\() sonrasında çocuk, çağrılıncaya kadar yalnızca zaman uyumsuz sinyal güvenliği işlevlerini (bkz. **sinyal güvenliği**\ (7)) güvenle arayabilir **execve**\ (2) uygulayın.

- Çocuk, üst öğenin açık dosya kümesinin kopyalarını devralır
   Tanımlayıcılar. Alt öğedeki her dosya tanımlayıcı, üst dosyadaki ilgili dosya tanımlayıcı ile aynı açık dosya tanımına (bkz. **açık**\ (2)) başvurur. Bu, iki dosya tanıtıcısının açık dosya durum bayraklarını, dosya ofsetini ve sinyale dayalı G / Ç özniteliklerini paylaştığı anlamına gelir (**fcntl**\ (2) içindeki **F_SETOWN** ve **F_SETSIG** açıklamasına bakın) ).

- Çocuk, üst öğenin açık ileti kuyruğu tanımlayıcı kümesinin kopyalarını devralır (bkz. **mq_overview**\ (7)). Alt öğedeki her dosya tanımlayıcı, üst öğedeki ilgili dosya tanımlayıcıyla aynı açık ileti kuyruğu açıklamasına başvurur. Bu, iki dosya tanıtıcısının aynı bayrakları paylaştığı anlamına gelir (*mq_flags*).

- Çocuk, üst öğenin açık dizin akışı kümesinin kopyalarını devralır (bkz. **opendir**\ (3)). POSIX.1, üst ve alt öğedeki *ilgili dizin akışlarının* dizin akışı konumunu paylaşabileceğini söylüyor; Linux / glibc üzerinde bunu yapmazlar.

GERİ DÖNÜŞ DEĞERİ
============

Başarılı olduğunda, alt sürecin PID'si üst öğede döndürülür ve 0 alt öğede döndürülür. Başarısızlık durumunda üst öğeye -1 döndürülür, alt işlem oluşturulmaz ve *errno* uygun şekilde ayarlanır.

HATALAR
======

**EAGAIN**
   İş parçacığı sayısı üzerinde sistem tarafından belirlenen bir sınırla karşılaşıldı. Bu hatayı tetikleyebilecek birkaç sınır vardır:

   - **RLIMIT_NPROC** yazılım kaynağı sınırı (üzerinden ayarlanır
      gerçek bir kullanıcı kimliği için işlem ve iş parçacığı sayısını sınırlayan **RLIMIT_NPROC** yazılım kaynağı sınırına (**setrlimit**\ (2) üzerinden ayarlanmıştır) ulaşılmıştır;

   - çekirdeğin sistem genelinde işlem sayısı ve iş parçacığı sayısı sınırına ulaşıldı, */proc/sys/kernel/threads-max* (bkz. **proc**\ (5));

   - maksimum PID sayısına (*/proc/sys/kernel/pid_max*) ulaşılmıştır (bkz. **proc**\ (5));

   - "işlem numarası" (PID'ler) denetleyicisi tarafından uygulanan PID sınırına (*pids.max*) ulaşıldı.

**EAGAIN**
   Arayan kişi **SCHED_DEADLINE** zamanlama politikası altında çalışmaktadır ve çatal üzerinde sıfırlama bayrağı ayarlanmamıştır. Bkz. **zamanlama**\ (7).

**ENOMEM**
   **çatal**\ () gerekli çekirdek yapılarını tahsis edemedi
   çünkü bellek dar.

**ENOMEM**
   "İnit" işlemi sona erdirilmiş bir PID ad alanında bir alt işlem oluşturulmaya çalışıldı. Bkz. **pid_namespaces**\ (7).

**ENOSYS**
   **fork**\ () bu platformda desteklenmez (örneğin, Bellek Yönetim Birimi olmayan donanım).

**ERESTARTNOINTR** (Linux 2.6.17'den beri)
   Sistem çağrısı bir sinyal ile kesildi ve yeniden başlatılacak. (Bu sadece bir iz sırasında görülebilir.)


UYGUN
=============

POSIX.1-2001, POSIX.1-2008, SVr4, 4.3BSD.

NOTLAR
=====

Linux altında, **fork** \ () yazma üzerine kopyalama sayfaları kullanılarak uygulanır, bu nedenle maruz kaldığı tek ceza, üst sayfa sayfalarını çoğaltmak ve çocuk.

C kütüphanesi / çekirdek farklılıkları
----------------------------

Sürüm 2.3.3'ten bu yana, çekirdek **fork** \ () sistem çağrısını çağırmak yerine, NPTL iş parçacığı uygulamasının bir parçası olarak sağlanan glibc ** fork ** \ () sarmalayıcısı **klon** \ (2) geleneksel sistem çağrısı ile aynı etkiyi sağlayan bayraklarla. (**fork** \ () çağrısı, *bayrakları* yalnızca **SIGCHLD** olarak belirten **klon** \ (2) çağrısına eşdeğerdir.) Glibc sarıcı, kullanılmış çatal işleyicilerini çağırır **pthread_atfork** \ (3) kullanılarak kurulmuştur.

ÖRNEKLER
========

Bkz. **pipe** \ (2) ve **wait** \ (2).

AYRICA BAKINIZ
========

**clone**\ (2), **execve**\ (2), **exit**\ (2), **setrlimit**\ (2),
**unshare**\ (2), **vfork**\ (2), **wait**\ (2), **daemon**\ (3),
**pthread_atfork**\ (3), **capabilities**\ (7), **credentials**\ (7)
