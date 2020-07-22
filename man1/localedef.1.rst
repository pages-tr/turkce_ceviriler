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
   Comma-separated list of warnings to disable. Supported warnings are
   *ascii* and *intcurrsym*.

**--posix**
   Conform strictly to POSIX. Implies **--verbose**. This option
   currently has no other effect. POSIX conformance is assumed if the
   environment variable **POSIXLY_CORRECT** is set.

**--prefix=**\ *pathname*
   Set the prefix to be prepended to the full archive pathname. By
   default, the prefix is empty. Setting the prefix to *foo*, the
   archive would be placed in *foo/usr/lib/locale/locale-archive*.

**--quiet**
   Suppress all notifications and warnings, and report only fatal
   errors.

**--replace**
   Replace a locale in the locale archive file. Without this option, if
   the locale is in the archive file already, an error occurs.

**--warnings=**\ *warnings*
   Comma-separated list of warnings to enable. Supported warnings are
   *ascii* and *intcurrsym*.

**-?**, **--help**
   Print a usage summary and exit. Also prints the default paths used by
   **localedef**.

**--usage**
   Print a short usage summary and exit.

**-V**, **--version**
   Print the version number, license, and disclaimer of warranty for
   **localedef**.

ÇIKIŞ DURUMU
============

One of the following exit values can be returned by **localedef**:

   **0**
      Command completed successfully.

   **1**
      Warnings or errors occurred, output files were written.

   **4**
      Errors encountered, no output created.

ÇALIŞMA ORTAMI
==============

**POSIXLY_CORRECT**
   The **--posix** flag is assumed if this environment variable is set.

**I18NPATH**
   A colon-separated list of search directories for files.

DOSYALAR
========

*/usr/share/i18n/charmaps*
   Usual default character map path.

*/usr/share/i18n/locales*
   Usual default path for locale definition files.

*/usr/share/i18n/repertoiremaps*
   Usual default repertoire map path.

*/usr/lib/locale/locale-archive*
   Usual default locale archive location.

*/usr/lib/locale*
   Usual default path for compiled individual locale data files.

*outputpath/LC_ADDRESS*
   An output file that contains information about formatting of
   addresses and geography-related items.

*outputpath/LC_COLLATE*
   An output file that contains information about the rules for
   comparing strings.

*outputpath/LC_CTYPE*
   An output file that contains information about character classes.

*outputpath/LC_IDENTIFICATION*
   An output file that contains metadata about the locale.

*outputpath/LC_MEASUREMENT*
   An output file that contains information about locale measurements
   (metric versus US customary).

*outputpath/LC_MESSAGES/SYS_LC_MESSAGES*
   An output file that contains information about the language messages
   should be printed in, and what an affirmative or negative answer
   looks like.

*outputpath/LC_MONETARY*
   An output file that contains information about formatting of monetary
   values.

*outputpath/LC_NAME*
   An output file that contains information about salutations for
   persons.

*outputpath/LC_NUMERIC*
   An output file that contains information about formatting of
   nonmonetary numeric values.

*outputpath/LC_PAPER*
   An output file that contains information about settings related to
   standard paper size.

*outputpath/LC_TELEPHONE*
   An output file that contains information about formats to be used
   with telephone services.

*outputpath/LC_TIME*
   An output file that contains information about formatting of data and
   time values.

UYUMLULUK
=========

POSIX.1-2008.

ÖRNEKLER
========

Compile the locale files for Finnish in the UTF-8 character set and add
it to the default locale archive with the name **fi_FI.UTF-8**:

::

   localedef -f UTF-8 -i fi_FI fi_FI.UTF-8

The next example does the same thing, but generates files into the
*fi_FI.UTF-8* directory which can then be used by programs when the
environment variable **LOCPATH** is set to the current directory (note
that the last argument must contain a slash):

::

   localedef -f UTF-8 -i fi_FI ./fi_FI.UTF-8

AYRICA BAKINIZ
==============

**locale**\ (1), **charmap**\ (5), **locale**\ (5),
**repertoiremap**\ (5), **locale**\ (7)
