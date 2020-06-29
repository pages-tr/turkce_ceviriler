İSİM
====

iconv - metni bir karakter kodlamasından diğerine dönüştürür

ÖZET
========

** iconv ** [* seçenekler *] [-f *from-encoding*] [-t *to-encoding*]
[*inputfile*]...

AÇIKLAMA
===========

** iconv ** programı bir kodlamadaki metni okur ve başka bir kodlamadaki metni verir. Hiçbir giriş dosyası verilmezse veya kısa çizgi (-) olarak verilirse, ** iconv ** standart girişten okunur. Hiçbir çıktı dosyası verilmezse, ** iconv ** standart çıktıya yazar.

* From-encoding * belirtilmezse, varsayılan değer geçerli yerel ayarın karakter kodlamasından türetilir. * To-encoding * belirtilmezse, varsayılan değer geçerli yerel ayarın karakter kodlamasından türetilir.

SEÇENEKLER
=======

**-f**\ *from-encoding*\ **, --from-code=**\ *from-encoding*
   Giriş karakterleri için * from-encoding * kullanın.

**-t**\ *to-encoding*\ **, --to-code=**\ *to-encoding*
   Çıktı karakterleri için * -şifreleme * kullanın.

   ** // IGNORE ** dizesi * kodlamasına * eklenirse, dönüştürülemeyen karakterler atılır ve dönüştürme işleminden sonra bir hata yazdırılır.

   ** // TRANSLIT ** dizesi, * kodlamasına * eklenirse, dönüştürülmekte olan karakterler gerektiğinde ve mümkün olduğunda dönüştürülür. Bu, bir karakter hedef karakter kümesinde temsil edilemediğinde, bir veya birkaç benzer görünümlü karakterle yaklaşık olarak tahmin edilebilir. Hedef karakter kümesinin dışında olan ve harf çevirisi yapılamayan karakterler çıktıda bir soru işareti (?) İle değiştirilir.

** -l **, ** --list **
   Bilinen tüm karakter kümesi kodlarını listeler.

** -c **
   Bu tür karakterlerle karşılaştığında sonlandırmak yerine dönüştürülemeyen karakterleri sessizce atın.

**-o**\ *outputfile*\ **, --output=**\ *outputfile*
   Çıktı için * çıktıdosyası * kullanın.

**-s**, **--silent**
   Bu seçenek yok sayılır; yalnızca uyumluluk için sağlanmıştır.

**--verbose**
   Birden çok dosyayı işlerken standart hata ile ilgili ilerleme bilgilerini yazdırın.

**-?**, **--help**
   Bir kullanım özeti yazdırın ve çıkın.

**--usage**
   Kısa bir kullanım özeti yazdırın ve çıkın.

**-V**, **--version**
   ** iconv ** için sürüm numarasını, lisansı ve garanti reddini yazdırın.

ÇIKIŞ DURUMU
===========

Başarı sıfır, hatalar sıfır değil.

ÇEVRE
===========

Dahili olarak, ** iconv ** programı, bir karakter kümesine ve karakter kümesinden dönüştürmek için * gconv * modüllerini (dinamik olarak yüklenmiş paylaşılan kütüphaneler) kullanan ** iconv ** \ (3) işlevini kullanır. ** iconv ** \ (3) öğesini çağırmadan önce, ** iconv ** programı önce ** iconv_open ** \ (3) kullanarak bir dönüşüm tanımlayıcısı ayırmalıdır. İkinci işlevin çalışması ** GCONV_PATH ** ortam değişkeninin ayarından etkilenir:
