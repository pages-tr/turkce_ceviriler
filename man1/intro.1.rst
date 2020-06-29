İSİM
====

intro - kullanıcı komutlarına giriş

AÇIKLAMA
========

Kılavuzun 1. Bölümünde kullanıcı komutları ve araçları, örneğin dosya işleme araçları, kabuklar, derleyiciler, web tarayıcıları, dosya ve görüntü izleyiciler ve düzenleyiciler vb. araçlar açıklanmaktadır.

NOTLAR
======

Linux bir UNIX lezzetidir ve ilk yaklaşım olarak UNIX altındaki tüm kullanıcı komutları Linux (ve FreeBSD ve diğer birçok UNIX benzeri sistem) altında tam olarak aynı şekilde çalışır.

Linux altında, ilk önce birçok belgeyi okumadan işlerinizi yapabileceğiniz işaret ve tıklayıp sürükleyebileceğiniz GUI'ler (grafik kullanıcı arabirimleri) vardır. Geleneksel UNIX ortamı, bilgisayara ne yapacağını söylemek için komutlar yazdığınız bir CLI (komut satırı arabirimi) 'dir. Bu daha hızlı ve daha güçlüdür, ancak komutların ne olduğunu bulmayı gerektirir. Başlamak için minimum bir değerin altında.

Oturum Açma
-----------

Çalışmaya başlamak için, öncelikle kullanıcı adınızı ve şifrenizi vererek bir oturum açmanız gerekir. **login**\ (1) şimdi sizin için bir *kabuk* (komut yorumlayıcısı) başlatır. Grafiksel bir giriş durumunda, menüler veya simgeler içeren bir ekran alırsınız ve bir fare tıklaması pencerede bir kabuk başlatır. Ayrıca bkz. **xterm**\ (1).

Kabuk
-----

Kabuk komutları, komut yorumlayıcısı. Yerleşik değildirler, sadece bir programdır ve bunları kullanarak kabuğunuzu değiştirebilirsiniz. Herkesin kendi favorisi var. Öntanımlı ve en basit olana *sh* denir. *sh* linux çekirdeği ile gelir. Ayrıca bakınız
**ash**\ (1), **bash**\ (1), **chsh**\ (1), **csh**\ (1), **dash**\ (1),
**ksh**\ (1), **zsh**\ (1).

Bir oturum şöyle olabilir:

::

   knuth login: aeb
   Password: ********
   $ date
   Tue Aug  6 23:50:44 CEST 2002
   $ cal
        August 2002
   Su Mo Tu We Th Fr Sa
                1  2  3
    4  5  6  7  8  9 10
   11 12 13 14 15 16 17
   18 19 20 21 22 23 24
   25 26 27 28 29 30 31

   $ ls
   bin  tel
   $ ls -l
   total 2
   drwxrwxr-x   2 aeb       1024 Aug  6 23:51 bin
   -rw-rw-r--   1 aeb         37 Aug  6 23:52 tel
   $ cat tel
   maja    0501-1136285
   peter   0136-7399214
   $ cp tel tel2
   $ ls -l
   total 3
   drwxr-xr-x   2 aeb       1024 Aug  6 23:51 bin
   -rw-r--r--   1 aeb         37 Aug  6 23:52 tel
   -rw-r--r--   1 aeb         37 Aug  6 23:53 tel2
   $ mv tel tel1
   $ ls -l
   total 3
   drwxr-xr-x   2 aeb       1024 Aug  6 23:51 bin
   -rw-r--r--   1 aeb         37 Aug  6 23:52 tel1
   -rw-r--r--   1 aeb         37 Aug  6 23:53 tel2
   $ diff tel1 tel2
   $ rm tel1
   $ grep maja tel2
   maja    0501-1136285
   $

Burada Control-D yazmak oturumu sonlandırdı.

Buradaki $ komut istemiydi; kabuğun bir sonraki komut için hazır olduğunu göstermenin yolu budur. Bilgi istemi birçok şekilde özelleştirilebilir ve kullanıcı adı, makine adı, geçerli dizin, saat vb.eklenebilir. Bunu yapmak için PS1 ödevi istemi (PS1 = "Sırada ne var efendim?")  belirtildiği gibi değiştirir.

*date* (tarih ve saat veren) ve *cal* (takvim veren) komutları olduğunu görüyoruz.

*ls* komutu geçerli dizinin içeriğini listeler; hangi dosyalara sahip olduğunuzu gösterir. *-l* seçeneğiyle dosyanın sahibi, boyutu ve tarihini ve kişilerin dosyayı okuma ve/veya değiştirme izinlerini içeren uzun bir liste verir. Örneğin, burada "tel" dosyası 37 bayt uzunluğundadır, aeb'ye aittir ve sahibi onu okuyabilir ve yazabilir, diğerleri sadece okuyabilir. Sahip ve izinler *chown* ve *chmod* komutları ile değiştirilebilir.

*cat* komutu bir dosyanın içeriğini gösterir. (Ad "birleştirme ve yazdırma" klasöründen gelir: parametre olarak verilen tüm dosyalar birleştirilir ve "standart çıktıya" gönderilir (bkz. **stdout**\ (3)) ( Bu örnek için öntanımlı olanı terminal penceresidir.)

*cp* komutu ("copy" kelimesinden gelir) bir dosyayı kopyalar.

Diğer yandan, *mv* komutu ("move" kelimesinden gelir), sadece onu yeniden adlandırır.

*diff* komutu iki dosya arasındaki farkları listeler. Burada çıktı yoktu, çünkü fark yoktu.

*rm* komutu ("remove" kelimesinden gelir) dosyayı siler ve unutmayın. Bu komutu kullanırken dikkatli olun! Silinen dosya gider. Çöp sepeti veya başka bir yere değil. Silinen dosya silindi anlamına gelir, artık o dosya kayıplara karışmıştır ve yok olmuştur.

*grep* komutu ("g/re/p" olayından gelir) bir veya daha fazla dosyada bir dizenin oluşumlarını bulur. Burada Maja'nın telefon numarasını buldu.


Yol adları ve geçerli dizin
---------------------------

Dosyalar büyük bir ağaçta, dosya hiyerarşisinde yaşar. Her birinin ağacın kökünden ( kök dizin / olarak adlandırılır) dosyaya giden yolu açıklayan bir yol adı vardır. Örneğin, böyle bir tam yol adı */home/aeb/tel* olabilir. Her zaman tam yol adları kullanmak sakıncalıdır ve geçerli dizindeki bir dosyanın adı yalnızca son bileşen verilerek kısaltılabilir. Bu nedenle */home/aeb/tel*, geçerli dizin */home/aeb* olduğunda tel olarak kısaltılabilir.

*pwd* komutu geçerli dizini yazdırır.

*cd* komutu geçerli dizini değiştirir.

Ek olarak olarak *cd* ve *pwd* komutlarını beraber kullanmayı deneyin ve *cd* kullanımını keşfedin: "cd",
"cd.", "cd ..", "cd /" ve "cd ~" komutlarını deneyin ve her seferinde nerede olduğunuzu *pwd* sayesinde öğrenin.

Dizinler
--------

*mkdir* komutu yeni bir dizin açar.

*rmdir* komutu eğer bir dizin boş ise onu siler ancak değilse silmez ve sizi uyarır.

*find* komutu (oldukça barok bir sözdizimiyle), verilen ada veya diğer özelliklere sahip dosyaları bulur. Örneğin, "find . -name tel", bu dizinden ( *.* olarak adlandırılan dizin geçerli dizindir) başlayarak *tel* isimli dosyayı bulur. "find / -name tel" de aynısını yapar, ancak ağacın kökünden başlar. Çoklu GB diskteki büyük aramalar zaman alıcı olacaktır ve böyle bir arama için **locate**\ (1) kullanmak daha yararlı olabilir.


Diskler and Dosya Sistemleri
----------------------------

*mount* komutu bağlı bir diski ( ya da floppy, CDROM veya başka bir cihazı) büyük dosya sistemi ağacına bağlar
Ve *umount* komutu bağlı diski geri söker. *df* komutu da diskinizde ne kadar alanın boş olduğunu size veren komuttur.

İşlemler
--------

UNIX sisteminde, birçok kullanıcı ve sistem işlemi aynı anda çalışır. Kullandığınız hesap ön planda, diğerleri *arka planda* çalışır. *ps* komutu size hangi işlemlerin etkin olduğunu ve bu işlemlerin hangi işlem değerine sahip olduğunu gösterecektir. *kill* komutu, onlardan kurtulmanızı sağlar. Seçenek olmadan kullanmak işleme naif yaklaşır ve sadece şunu der: lütfen git. Ancak "kill -9" ve ardından işlem değerini girmeniz bu kadar nazik olmayacaktır ve süreci anında bir öldürecektir. Ön plan süreçleri genellikle Control-C yazılarak öldürülebilir.


Bilgi Almak
-----------

Her biri birçok seçeneğe sahip binlerce komut vardır. Geleneksel olarak komutlar *kılavuz sayfalarında* (bu gibi) belgelenir, böylece "man kill" komutunu vererek "kill" komutunun kullanımını görüntüleyebilirsiniz (ve "man man" komutu "man" komutunun ne işe yaradığını belgeleyecektir). *man* metni genellikle *sayfalayıcı* olarak kullanılan bir çağrı cihazı aracılığıyla gönderir, *less* gibi. Sonraki sayfayı almak için *boşluk* çubuğuna basın, çıkmak için *q* tuşuna basın.

Dokümantasyonda, **man**\ (1)'de olduğu gibi isim ve bölüm numarası vererek *man* sayfalarına atıf yapmak gelenekseldir. Man sayfaları kesiktir ve unutulmuş bazı ayrıntıları hızlı bir şekilde bulmanızı sağlar. Yeni gelenler için daha fazla örnek ve açıklama içeren bir giriş metni yararlıdır.

Bilgi dosyaları ile birlikte bir çok GNU/FSF yazılımı sağlanır. Program bilgilerinin kullanımı hakkında bir tanıtım için "info info" yazın.

Özel konular genellikle NASIL (HOWTO) belgesinde ele alınmaktadır. /usr/share/doc/howto/tr* adresine bakın ve orada HTML dosyaları bulursanız bir tarayıcı kullanarak onalrı açıp okuyun.


AYRICA BAKINIZ
==============

**ash**\ (1), **bash**\ (1), **chsh**\ (1), **csh**\ (1), **dash**\ (1),
**ksh**\ (1), **locate**\ (1), **login**\ (1), **man**\ (1),
**xterm**\ (1), **zsh**\ (1), **wait**\ (2), **stdout**\ (3),
**man-pages**\ (7), **standards**\ (7)
