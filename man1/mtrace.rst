İSİM
====

mtrace - malloc izleme günlüğünü yorumlar

ÖZET
====

**mtrace** [*option*]... [*binary*] *mtracedata*

AÇIKLAMA
========

**mtrace**, içeriği **mtrace** \ (3) tarafından üretilen *mtracedata* dosyasında bulunan izleme günlüğünün okunabilir çıktılarını yorumlamak ve sağlamak için kullanılan bir Perl betiğidir. *İkili* sağlanırsa, **mtrace** çıktısı ayrıca sorunlu konumlar için satır numarası bilgileri içeren kaynak dosya adını da içerir (*ikilinin* hata ayıklama bilgileri ile derlendiği varsayılarak).
**mtrace** \ (3) işlevi ve **mtrace** komut dosyası kullanımı hakkında daha fazla bilgi için bkz. **mtrace** \ (3).

SEÇENEKLER
==========

**--help**
   Yardımı yazdırın ve çıkın.

**--version**
   Sürüm bilgilerini yazdırın ve çıkın.

BÖCEK
=====

Hata raporlama talimatları için lütfen şu adrese bakın:
`<http://www.gnu.org/software/libc/bugs.html>` __.

AYRICA BAKINIZ
==============

**memusage**\ (1), **mtrace**\ (3)
