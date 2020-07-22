İSİM
====

locale - bölgeye özgü bilgi al

ÖZET
====

::

   locale [seçenek]
   locale [seçenek] -a
   locale [seçenek] -m
   locale [seçenek] isim ...

AÇIKLAMA
========

**locale** komutu, standart çıktıda geçerli yerel ayar veya tüm yerel ayarlarla
ilgili bilgileri görüntüler.

Bağımsız değişkenler olmadan çağrıldığında, **locale**, yerel ayarı denetleyen
ortam değişkenlerinin ayarlarına bağlı olarak her yerel ayar kategorisi için
geçerli yerel ayar ayarlarını görüntüler (bkz. **locale** \ (5)) (bkz. **locale** \ (7)).
Ortamda ayarlanan değişkenler için değerler çift tırnak işareti olmadan, zımni
değerler çift tırnak işareti ile yazdırılır.

**-a** veya **-m** seçeneği (veya uzun biçimli eşdeğerlerinden biri) belirtilirse,
davranış aşağıdaki gibidir:

**-a**, **--all-locales**
   Mevcut tüm yerel ayarların bir listesini görüntüler. **-v** seçeneği, çıktıya
   her bir yerel ayar için **LC_IDENTIFICATION** meta verilerinin eklenmesine
   neden olur.

**-m**, **--charmaps**
   Kullanılabilir karakter eşlemlerini görüntüleyin (karakter kümesi açıklama
   dosyaları). Yerel ayar için geçerli karakter kümesini görüntülemek için
   **locale -c charmap** kullanın.

**locale** komutu, yerel anahtar kelimelerin adları olan bir veya daha fazla
bağımsız değişkenle de sağlanabilir (örneğin, *date_fmt*, *ctype-class-names*,
*yesexpr* veya *decimal_point*) veya yerel kategoriler (örneğin, **LC_CTYPE**
veya **LC_TIME**). Her bağımsız değişken için aşağıdakiler görüntülenir:

- Yerel ayar anahtar kelimesi için, görüntülenecek anahtar kelimenin değeri.

- Yerel ayar kategorisi için, o kategorideki tüm anahtar kelimelerin değerleri görüntülenir.

Bağımsız değişkenler sağlandığında, aşağıdaki seçenekler anlamlıdır:

**-c**, **--category-name**
   Kategori adı bağımsız değişkeni için, yerel kategori kategorisinin adını, o kategoriye ait anahtar kelime değerleri listesinden önce ayrı bir satıra yazın.

   Bir anahtar kelime adı bağımsız değişkeni için, anahtar kelime değerinden önceki ayrı bir satıra bu anahtar kelime için yerel ayar kategorisinin adını yazın.

   Bu seçenek, birden çok ad bağımsız değişkeni belirtildiğinde okunabilirliği artırır. ** - k ** seçeneği ile birleştirilebilir.

**-k**, **--keyword-name**
   Değeri görüntülenen her anahtar kelime için, çıktının şu biçime sahip olması için söz konusu anahtar kelimenin adını da ekleyin:

   *anahtar kelime*\ = "*değer*"

**locale** komutu aşağıdaki seçenekleri de bilir:

**-v**, **--verbose**
   Bazı komut satırı seçenekleri ve bağımsız değişken kombinasyonları için ek bilgileri görüntüler.

**-?**, **--help**
   Komut satırı seçenekleri ve bağımsız değişkenlerinin bir özetini görüntüleyin ve çıkın.

**--usage**
   Kısa kullanım mesajı görüntüleyin ve çıkın.

**-v**, **--version**
   Program sürümünü görüntüleyin ve çıkın.

DOSYALAR
========

*/usr/lib/locale/locale-archive*
   Her zamanki varsayılan yerel ayar arşiv konumu.

*/usr/share/i18n/locales*
   Yerel ayar tanımı dosyaları için olağan varsayılan yol.

UYGUNLUK
========

POSIX.1-2001, POSIX.1-2008.

ÖRNEKLER
========

::

   $ locale
   LANG=en_US.UTF-8
   LC_CTYPE="en_US.UTF-8"
   LC_NUMERIC="en_US.UTF-8"
   LC_TIME="en_US.UTF-8"
   LC_COLLATE="en_US.UTF-8"
   LC_MONETARY="en_US.UTF-8"
   LC_MESSAGES="en_US.UTF-8"
   LC_PAPER="en_US.UTF-8"
   LC_NAME="en_US.UTF-8"
   LC_ADDRESS="en_US.UTF-8"
   LC_TELEPHONE="en_US.UTF-8"
   LC_MEASUREMENT="en_US.UTF-8"
   LC_IDENTIFICATION="en_US.UTF-8"
   LC_ALL=

   $ locale date_fmt
   %a %b %e %H:%M:%S %Z %Y

   $ locale -k date_fmt
   date_fmt="%a %b %e %H:%M:%S %Z %Y"

   $ locale -ck date_fmt
   LC_TIME
   date_fmt="%a %b %e %H:%M:%S %Z %Y"

   $ locale LC_TELEPHONE
   +%c (%a) %l
   (%a) %l
   11
   1
   UTF-8

   $ locale -k LC_TELEPHONE
   tel_int_fmt="+%c (%a) %l"
   tel_dom_fmt="(%a) %l"
   int_select="11"
   int_prefix="1"
   telephone-codeset="UTF-8"



Aşağıdaki örnek, *./Wrk* dizininden *$HOME/.locale* dizini altındaki
**localedef**\ (1) yardımcı programıyla özel bir yerel ayarı derler
ve sonucu **date**\ (1) komutunu girip kabuk profil dosyasındaki **LOCPATH**
ve **LANG** ortam değişkenlerini ayarlar; böylece sonraki yerel
kullanıcı oturumlarında özel yerel ayar kullanılır:

::

    $ mkdir -p $HOME/.locale
    $ I18NPATH=./wrk/ localedef -f UTF-8 -i fi_SE $HOME/.locale/fi_SE.UTF-8
    $ LOCPATH=$HOME/.locale LC_ALL=fi_SE.UTF-8 date
    $ echo "export LOCPATH=\$HOME/.locale" >> $HOME/.bashrc
    $ echo "export LANG=fi_SE.UTF-8" >> $HOME/.bashrc


AYRICA BAKINIZ
==============

**localedef**\ (1), **charmap**\ (5), **locale**\ (5), **locale**\ (7)
