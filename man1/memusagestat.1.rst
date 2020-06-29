İSİM
====

memusagestat - bellek profili oluşturma verilerinden grafik oluşturur

ÖZET
====

**memusagestat** [*seçenekler*]... *datafile* [*outfile*]

AÇIKLAMA
========

**memusagestat**, *datafile* dosyasındaki bellek profili oluşturma verilerinin grafik temsilini içeren bir PNG dosyası oluşturur; bu dosya **memusage**\ (1) 'in *-d * (veya *--data*) seçeneği ile oluşturulur.

Grafikteki kırmızı çizgi yığın kullanımını (ayrılan bellek) ve yeşil çizgi yığın kullanımını gösterir. X ölçeği (yatay eksen), bellek işleme işlevi çağrılarının sayısı veya (*-t* seçeneği belirtilmişse) süresidir.

SEÇENEKLER
==========

**-o**\ *dosya*\ **, --output=**\ *dosya*
   Çıkış dosyasının adı.

**-s**\ *string*\ **, --string=**\ *string*
   *string* seçeneği grafik için başlık olarak kullanılır.

**-t, --time**
   Yatay eksende sınırlandırma ölçeği olarak belirli bir zamanı (işlev çağrılarının sayısı yerine) kullanın.

**-T, --total**
   Ayrıca toplam bellek tüketiminin bir grafiğini çizin.

**-x**\ *size*\ **, --x-size=**\ *size*
   Çıktı grafiğini *size* piksel genişliğinde yapın.

**-y**\ *size*\ **, --y-size=**\ *size*
   Çıktı grafiğini *size* piksel yüksekliğinde yapın.

**-?**, **--help**
   Bir kullanım özeti yazdırın ve çıkın.

**--usage**
   Kısa bir kullanım özeti yazdırın ve çıkın.

**-V**, **--version**
   **memusagestat** için sürüm numarasını, lisansı ve garanti reddini yazdırın.

BÖCEK
=====

Hata raporlama talimatları için lütfen şu adrese bakın:
`<http://www.gnu.org/software/libc/bugs.html>`__.

ÖRNEKLER
========

**memusage**\ (1) sayfasına bakınız.


AYRICA BAKINIZ
==============

**memusage**\ (1), **mtrace**\ (1)
