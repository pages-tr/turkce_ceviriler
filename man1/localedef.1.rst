İSİM
====

localedef - yerel ayar dosyalarını derler

ÖZET
====

| **localedef** [*seçenekler*] *çıktı_konumu*
| **localedef --add-to-archive** [*seçenekler*] *derlenmiş_çıktı_konumu*
| **localedef --delete-from-archive** [*seçenekler*] *yereladı* ...
| **localedef --list-archive** [*seçenekler*]
| **localedef --help**
| **localedef --usage**
| **localedef --version**

AÇIKLAMA
========

**localedef** programı belirtilen *charmap* ve *input* dosyalarını okur,
C kütüphanesindeki yerel ayar işlevleri (**setlocale** \ (3), ** localeconv**\ (3) vb.)
tarafından hızlı bir şekilde kullanılabilen bir ikili forma derler.
Çıktıyı *çıktı_konumu*'na yerleştirir.

*çıktı_konumu* bağımsız değişkeni şu şekilde yorumlanır:

-  *çıktı_konumu*, bir eğik çizgi karakteri ('/') içeriyorsa, çıktı
   tanımlarının saklanacağı dizinin adı olarak yorumlanır. Bu durumda,
   her yerel ayar kategorisi için ayrı bir çıktı dosyası vardır
   (*LC_TIME*, *LC_NUMERIC*, vb.).

-  **--no-archive** seçeneği kullanılırsa, *çıktı_konumu* kategori
   başına derlenen dosyaların yerleştirildiği */usr/lib/locale*
   içindeki bir alt dizinin adıdır.

-  Aksi takdirde, *çıktı_konumu* bir yerel ayarın adıdır ve
   derlenen yerel ayar verileri */usr/lib/locale/locale-archive*
   arşiv dosyasına eklenir. Yerel ayar arşivi, sistem tarafından
   sağlanan tüm yerel ayarları içeren bellek eşlemeli bir dosyadır;
   **LOCPATH** ortam değişkeni ayarlanmadığında tüm yerelleştirilmiş
   programlar tarafından kullanılır.

Her durumda, yerel ayar dosyaları yazmaya çalıştığı dizin önceden oluşturulmamışsa
**localedef** iptal olur.

Hiçbir *charmapfile* verilmezse, varsayılan olarak *ANSI_X3.4-1968* (ASCII için)
değeri kullanılır. *inputfile* verilmezse veya tire (-) olarak verilirse,
**localedef** veriyi standart girişten okur.

SEÇENEKLER
==========

İşlem seçim seçenekleri
-----------------------
Birkaç seçenek **localedef** 'i yerel ayar tanımlarını derlemekten başka bir şey
yapmaya yönlendirir. Bu seçeneklerden yalnızca biri aynı anda kullanılmalıdır.

**--add-to-archive**
   Yerel derleme arşiv dosyasına *compiledpath* dizinlerini ekleyin. Dizinler
   **--no-archive** kullanılarak **localedef**'in önceki çalıştırmaları
   tarafından oluşturulmuş olmalıdır.

**--delete-from-archive**
   Yerel ayar arşiv dosyasından adlandırılmış yerel ayarları silin.

**--list-archive**
   Yerel ayar arşiv dosyasında bulunan yerel ayarları listeleyin.

Diğer Seçenekler
----------------
Aşağıdaki seçeneklerden bazıları yalnızca belirli işlemler için uygundur;
genellikle hangileri olduğu açık bir şekilde anlaşılmalıdır.
**-f** ve **- c**'nin beklediğinizden geri döndüğüne dikkat edin;
yani, **-f ** **--force** ile aynı değildir.

**-f**\ *charmapfile*\ **, --charmap=**\ *charmapfile*
  Girdi dosyası tarafından kullanılan karakter kümesini tanımlayan dosyayı belirtin.
  *charmapfile*, eğik çizgi karakteri ('/') içeriyorsa, karakter haritasının adı
  olarak yorumlanır. Aksi takdirde, dosya geçerli dizinde ve karakter eşlemeleri
  için varsayılan dizinde aranır. Ortam değişkeni **I18NPATH** ayarlanırsa,
  *$I18NPATH/charmaps/* ve *$I18NPATH/* da geçerli dizinden sonra
  aranır. Karakter eşlemeleri için varsayılan dizin **localedef --help**
  tarafından yazdırılır.

**-i**\ *inputfile*\ **, --inputfile=**\ *inputfile*
   Derlenecek yerel tanım dosyasını belirtin. Dosya geçerli dizinde ve yerel ayar
   tanımları için varsayılan dizinde aranır. Ortam değişkeni **I18NPATH**
   ayarlanmışsa, geçerli dizinden sonra *$I18NPATH/locales/* ve *$I18NPATH*
   içinde aranır. Yerel ayar tanımı dosyaları için varsayılan dizin
   **localedef --help** tarafından yazdırılır.

**-u**\ *repertoirefile*\ **, --repertoire-map=**\ *repertoirefile*
   *repertoirefile*'dan sembolik adlardan Unicode kod noktalarına eşlemeleri okuyun.
   *repertoirefile*, eğik çizgi karakteri ('/') içeriyorsa, repertuar haritasının
    yol adı olarak yorumlanır. Aksi takdirde, dosya geçerli dizinde ve repertuar
    haritaları için varsayılan dizinde aranır. Ortam değişkeni **I18NPATH**
    ayarlanırsa, geçerli dizinden sonra *$I18NPATH/repertoiremaps/* ve *$I18NPATH*'da
    aranır. Repertuar haritaları için varsayılan dizin **localedef --help**
    tarafından yazdırılır.

**-A**\ *aliasfile*\ **, --alias-file=**\ *aliasfile*
   Yerel adların diğer adlarını aramak için *aliasfile*  takma ad dosyasını kullanın.
   Varsayılan takma ad dosyası yoktur.

**-c**, **--force**
   Girdi dosyası hakkında uyarılar oluşturulmuş olsa bile çıktı dosyalarını yazın.

**-v**, **--verbose**
   Normalde yok sayılan hatalar hakkında ek uyarılar oluşturun.

**--big-endian**
   big-endian çıktı oluştur.

**--little-endian**
   little-endian çıktı oluşturur.

**--no-archive**
   Yerel ayar arşiv dosyasını kullanmayın, bunun yerine yerel ayar arşiv
   dosyasıyla aynı dizinde alt dizin olarak *outputpath* oluşturun ve içindeki
   yerel ayar kategorileri için ayrı çıktı dosyaları oluşturun. Bu, sistem yerel
   ayarı arşiv güncelleştirmelerinin **localedef** ile oluşturulan özel yerel
   ayarların üzerine yazmasını önlemeye yardımcı olur.

**--no-hard-links**
   Yüklü yerel ayarlar arasında sabit bağlantılar oluşturmayın.

**--no-warnings=**\ *warnings*
   Devre dışı bırakılacak uyarıların virgülle ayrılmış listesi. Desteklenen
   uyarılar *ascii* ve *intcurrsym*'dir.

**--posix**
   POSIX'e kesinlikle uyun. **--verbose** anlamına gelir. Bu seçeneğin şu anda
   başka bir etkisi yoktur. **POSIXLY_CORRECT** ortam değişkeni ayarlanmışsa,
   POSIX uyumluluğu varsayılır.

**--prefix=**\ *pathname*
   Tam arşiv yol adına eklenecek öneki ayarlayın. Varsayılan olarak önek
   boştur. Önek *foo* olarak ayarlandığında, arşiv *foo/usr/lib/locale/locale-archive*
   içine yerleştirilir.

**--quiet**
   Tüm bildirimleri ve uyarıları bastırın ve yalnızca önemli hataları bildirin.

**--replace**
   Yerel ayar arşiv dosyasındaki bir yerel ayarı değiştirin. Bu seçenek
   olmadan, yerel ayar zaten arşiv dosyasındaysa bir hata oluşur.

**--warnings=**\ *warnings*
   Etkinleştirmek için virgülle ayrılmış uyarıların listesi.
   Desteklenen uyarılar *ascii* ve *intcurrsym* dir.

**-?**, **--help**
   Bir kullanım özeti yazdırın ve çıkın. Ayrıca **localedef** tarafından
   kullanılan varsayılan yolları da yazdırır.

**--usage**
   Kısa bir kullanım özeti yazdırın ve çıkın.

**-V**, **--version**
   **localedef** için sürüm numarasını, lisansı ve garanti reddini yazdırın.

ÇIKIŞ DURUMU
============

Aşağıdaki çıkış değerlerinden biri **localedef** tarafından döndürülebilir:

   **0**
      Komut başarıyla tamamlandı.

   **1**
      Uyarılar veya hatalar oluştu, çıktı dosyaları yazıldı.

   **4**
      Hatalarla karşılaşıldı, çıktı oluşturulmadı.

ÇALIŞMA ORTAMI
==============

**POSIXLY_CORRECT**
  **--posix** bayrağı, bu ortam değişkeni ayarlanmışsa varsayılır.

**I18NPATH**
   Dosyalar için iki nokta üst üste işaretli arama dizinleri listesi.

DOSYALAR
========

*/usr/share/i18n/charmaps*
   Her zamanki varsayılan karakter eşleme yolu.

*/usr/share/i18n/locales*
   Yerel ayar tanımı dosyaları için olağan varsayılan yol.

*/usr/share/i18n/repertoiremaps*
   Repertuar harita yolu için olağan varsayılan yol.

*/usr/lib/locale/locale-archive*
   Olağan varsayılan yerel ayar arşiv konumu.

*/usr/lib/locale*
   Derlenmiş tek tek yerel ayar veri dosyaları için her zamanki varsayılan yol.

*outputpath/LC_ADDRESS*
   Adreslerin ve coğrafya ile ilgili öğelerin biçimlendirilmesi hakkında bilgi içeren bir çıktı dosyası.

*outputpath/LC_COLLATE*
   Dizeleri karşılaştırma kuralları hakkında bilgi içeren bir çıktı dosyası.

*outputpath/LC_CTYPE*
   Karakter sınıfları hakkında bilgi içeren bir çıktı dosyası.

*outputpath/LC_IDENTIFICATION*
   Yerel ayarla ilgili meta veriler içeren bir çıktı dosyası.

*outputpath/LC_MEASUREMENT*
   Yerel ölçümler hakkında bilgi içeren bir çıktı dosyası (metrik ve ABD geleneksel).

*outputpath/LC_MESSAGES/SYS_LC_MESSAGES*
   Dil mesajları ve olumlu ya da olumsuz yanıtın nasıl göründüğü hakkında bilgi içeren bir çıktı dosyası yazdırılmalıdır.

*outputpath/LC_MONETARY*
   Parasal değerlerin biçimlendirilmesi hakkında bilgi içeren bir çıktı dosyası.

*outputpath/LC_NAME*
   Kişiler için selamlar hakkında bilgi içeren bir çıktı dosyası.

*outputpath/LC_NUMERIC*
   Parasal olmayan sayısal değerlerin biçimlendirilmesi hakkında bilgi içeren bir çıktı dosyası.

*outputpath/LC_PAPER*
   Standart kağıt boyutu ile ilgili ayarlar hakkında bilgi içeren bir çıktı dosyası.

*outputpath/LC_TELEPHONE*
   Telefon hizmetleri ile kullanılacak biçimler hakkında bilgi içeren bir çıktı dosyası.

*outputpath/LC_TIME*
   Veri ve zaman değerleri biçimlendirme hakkında bilgi içeren bir çıktı dosyası.

UYUMLULUK
=========

POSIX.1-2008.

ÖRNEKLER
========

UTF-8 karakter kümesinde Fince için yerel ayar dosyalarını derleyin ve
**fi_FI.UTF-8** adıyla varsayılan yerel ayar arşivine ekleyin:

::

   localedef -f UTF-8 -i fi_FI fi_FI.UTF-8

Bir sonraki örnek aynı şeyi yapar, ancak *fi_FI.UTF-8* dosyasına dosya oluşturur.
**LOCPATH** ortam değişkeni geçerli dizine ayarlandığında programlar tarafından
kullanılabilir (son argümanın eğik çizgi içermesi gerektiğini unutmayın):

::

   localedef -f UTF-8 -i fi_FI ./fi_FI.UTF-8

AYRICA BAKINIZ
==============

**locale**\ (1), **charmap**\ (5), **locale**\ (5),
**repertoiremap**\ (5), **locale**\ (7)
