# NovaBang — Yapım Sürecinde Kullanılan Promptlar

Bu dosya EDS'e yüklenecek teslim dosyası değildir. Oyunun hangi adımlarla, hangi promptlarla ve neden öyle yazılarak yapıldığını anlatan ayrı bir kayıttır.

**Genel yöntem:** Oyun tek bir HTML dosyası olarak (harici kütüphane ve görsel yok, ses yok) adım adım geliştirildi. Her adımda önce mevcut oyunu bozmamak, sonra yalnızca istenen değişikliği yapmak hedeflendi. Sayılar her promptta açıkça yazıldı, böylece sonuç ölçülebildi.

**Önemli not — sonradan değişen özellikler:** Bu dosya sürecin gerçek kaydıdır, bu yüzden bazı promptlarda sonradan kaldırılan ya da değiştirilen özellikler geçer. Oyunun son hâli ve teslim dosyası şöyledir:
- **Kombo sistemi:** Prompt 1'de vardı, Prompt 3'te tamamen kaldırıldı. Son oyunda kombo yoktur.
- **Kuyruklu yıldız yağmuru:** Prompt 2'de vardı, Prompt 3'te meteor yağmuruna dönüştürüldü.
- **Evreler ve adları:** Prompt 1 ve 2'deki evre sırası (Yıldız, Kırmızı Dev, Mavi Dev) Prompt 4'te küçükten büyüğe yeniden tasarlandı.
- **Büyüme değerleri:** Prompt 1 ve 2'deki büyüme miktarları Prompt 5'te %40 çarpanla azaltıldı.
- **Oyunun adı:** Yıldız Kayması → Kozmik Kıvılcım (Prompt 6) → NovaBang (Prompt 7).

---

## Prompt 0 — Fikir (kendi cümlelerimle)
```
Galaksi temasında uzayda geçen yıldız kayması oyunu. Kayan yıldızları biz kontrol ediyoruz ve galaksilere çarparak daha da büyüyen yıldızlar elde ediyoruz.
```
**Neden:** Fikir bana ait, yapay zekâdan yalnızca çeşitlendirme ve netleştirme desteği aldım. Bu adımdan sonra mekanikleri (evrim, boyut kuralı, kara delik, süpernova vb.) birlikte konuşup seçtim.

---

## Prompt 1 — Temel oyun
```
Tarayıcıda çalışan, tek bir HTML dosyasından oluşan (harici kütüphane ve görsel dosyası olmadan) casual bir oyun yap. Oyunun geçici adı "Yıldız Kayması".

Konu: Uzayda geçiyor. Oyuncu, parmağını (mobil) ya da fareyi (bilgisayar) sürükleyerek bir kayan yıldızı yönlendiriyor. Yıldız galaksilere çarparak büyüyor ve evrim geçiriyor.

Bu ilk aşamada yalnızca şu 5 özelliği yap:
1. Yıldız, parmak/fare nereye giderse yumuşakça oraya kayar ve arkasında boyutuyla uzayan bir kuyruk bırakır.
2. Galaksiler ekranın üstünden aşağı akar. Üç çeşit vardır: sarmal (+3 büyüklük, +10 skor), eliptik (+6, +25), kuasar (+12, +50). Yıldızın büyüklüğü 0-99 arasındadır ve evreleri belirler: Yıldız Tozu (0-9), Meteor (10-29), Kuyruklu Yıldız (30-59), Yıldız (60-99). Her evrede yıldızın rengi ve parlaklığı değişir.
3. Boyut kuralı: sarmalı her evre yutar, eliptiği Meteor ve üstü, kuasarı Kuyruklu Yıldız ve üstü yutar. Yutabildiğin galaksinin etrafında turkuaz düz halka, yutamadığının etrafında kırmızı kesikli halka olsun. Yutamadığın galaksiye çarparsan 1 can gider ve büyüklüğün %20 azalır. Oyuncunun 3 canı var. 12. saniyeden sonra kara delikler gelir: 150 birim çekim alanı vardır, merkezine (60 birim) girersen 1 can gider.
4. Skor: galaksi puanı x kombo çarpanı. 3 saniye içinde art arda galaksi yutarsan çarpan x2, x3, x4 olur. Süre dolarsa ya da can kaybedersen sıfırlanır.
5. 3 can bitince oyun sonu ekranı çıksın (skor, en yüksek skor, ulaşılan evre) ve "Tekrar oyna" düğmesi oyunu yeniden başlatsın.

Zorluk: her 30 saniyede akış hızı %10 artsın.
Ekranlar: başlangıç (oyun adı, kısa nasıl oynanır, Başla düğmesi), oyun (canlar, skor, evre çubuğu), oyun sonu.
Görsel tarz: koyu lacivert ve mor uzay, turkuaz vurgular, neon parıltılı flat cartoon. Sevimli ama gizemli bir his.
Cihaz: önce mobil dikey, masaüstünde de çalışsın.
Şunları henüz ekleme: yerçekimi sapanı, asteroit, güçlendirmeler, süpernova.
```
**Neden böyle yazdım:**
- Tek HTML dosyası ve harici dosya yok: teslimi ve açmayı kolaylaştırır.
- "Yalnızca şu 5 özelliği yap" ve "henüz ekleme": kapsamı sınırlar, hata riskini azaltır ve ödevdeki "ilk sürümde tam 5 özellik" kuralıyla örtüşür.
- Sayılar (+3, %20, 150 birim, 3 saniye): yapay zekâ tahmin yürütmez, sonuç ölçülebilir olur.
- Halka renkleri: kuralı yazıyla değil görselle öğretir.

---

## Prompt 2 — Daha zor oyun, geniş evrim, süpernova, çekim
```
Oyunu şu değişikliklerle güncelle. Mevcut çalışan kısımları bozma, dosya yine tek HTML olsun.

1. Daha büyük evreler: Yıldız evresinden sonra Kırmızı Dev (100-149) ve Mavi Dev (150-199) evrelerini ekle. Yıldızın rengi büyüklüğüne göre yumuşakça değişsin (gri-mavi, turuncu, turkuaz, sarı, kırmızı, mavi). Evre çubuğu 0-200 arası olsun. İki yeni galaksi türü ekle: Dev (60 ve üstü yutar, +18 büyüklük, +100 skor) ve Süper (100 ve üstü yutar, +28 büyüklük, +200 skor).
2. Süpernova: büyüklük 200 olunca yıldız 2,2 saniye boyunca şişip beyazlaşsın, sonra patlasın. Şok dalgası ekrandaki tüm engelleri yok edip puana çevirsin, +1000 bonus versin. Patlamadan sonra arka plan yeni bir renk dünyasına geçsin (Mavi Uzay → Kızıl Nebula → Zümrüt Bulutsu, sonra döngü). Yıldız 10 büyüklükte yeniden doğsun, canı 3'ten azsa +1 can kazansın. Her bölgede puan çarpanı +0,5 artsın.
3. Çekim kuvveti: yutamadığım galaksiler, kara delikler, asteroitler ve pulsarlar yıldızı kendilerine çeksin. Çekim alanları ekranda soluk halka olarak görünsün. Çekim, yıldızın maksimum hızından zayıf olsun ki kaçmak mümkün olsun.
4. Daha zor engeller: asteroit kuşakları (çarpınca -8 büyüklük ve 1 saniye yavaşlama). 2. bölgeden itibaren dönen ışınlı pulsarlar (ışına değince -1 can). 3. bölgeden itibaren hızlı kuyruklu yıldız yağmuru (çarpınca -12 büyüklük). Bölge başına akış hızı %20 artsın.
5. Genel zorluk: akış hızı 125 olsun, can kaybında büyüklük %25 azalsın, kara delikler 8. saniyede başlasın.
Sayıları kodun en üstünde ayarlanabilir sabitler olarak tut.
```
**Neden böyle yazdım:**
- "Mevcut kısımları bozma": yapay zekâ bazen istenmeyen yerleri de yeniden yazar, bu cümle onu korumaya çeker.
- Numaralı 5 madde: her isteğin yapılıp yapılmadığını tek tek kontrol edebilmek için.
- "Kaçmak mümkün olsun": çekim kuvveti zor olsun ama haksız olmasın diye koşul koydum.
- "Sayıları en üste koy": sonraki küçük ayarlar (hızı azalt gibi) tek satır değiştirmekle bitsin diye.

---

## Prompt 3 — Kombo kaldırma ve meteor yağmuru
```
Oyunu güncelle. Mevcut çalışan kısımları bozma, dosya tek HTML kalsın.

1. Kombo sistemini tamamen kaldır: kombo sayacı, çarpan, süre çubuğu ve ekrandaki göstergesi olmasın. Galaksi yutunca sadece galaksinin puanı x bölge çarpanı kadar skor gelsin.
2. Kuyruklu yıldız yağmurunu kaldır ve yerine zamanla gelen "meteor yağmuru" raidleri ekle:
   - İlk yağmur oyunun 16. saniyesinde başlasın. Yağmurdan önce 2,2 saniye uyarı olsun: sol ve üst kenar turuncu parlasın, sağa akan oklar görünsün, ekranın üstünde "Meteor yağmuru" yazsın.
   - Meteorlar soldan ve üst kenardan girip sağa ve aşağı doğru, yaklaşık 28-52 derece açıyla gelsin. Ateşli kuyruğu olsun, oyuncu yönünü okuyabilsin.
   - Yağmur bitince 10-24 saniyelik ara olsun.
   - Çarpınca -12 büyüklük ve 1 saniye yavaşlama; büyüklük 12'den azsa 1 can gitsin. Büyük kayalar -18 götürsün.
3. Zorluk her yağmurda artsın: yağmur süresi, meteor sıklığı ve hızı artsın, aralar kısalsın. 3. yağmurdan sonra yavaş ama iri kayalar, 6. yağmurdan sonra ikili gruplar, 11. yağmurdan sonra üçlü gruplar gelsin. Bölge numarası da yağmur gücünü artırsın. Yağmur ekranı kaçılamayacak kadar doldurmasın.
4. Süpernova patlayınca yağmur dursun, yeni bölgede kısa bir sakin süre olsun.
Sayıları kodun en üstünde ayarlanabilir sabitler olarak tut.
```
**Neden böyle yazdım:**
- Kaldırılan sistemin parçalarını tek tek saydım (sayaç, çarpan, çubuk, gösterge), yoksa yapay zekâ yalnızca ekrandaki yazıyı silip arkadaki kodu bırakabilir.
- "Oyuncu yönünü okuyabilsin" ve "kaçılamayacak kadar doldurmasın": zor oyun ile haksız oyun arasındaki farkı anlatır.
- Kademeli artış listesi (3., 6., 11. yağmur): "zorluk artsın" tek başına belirsizdir, hangi yağmurda ne değiştiği yazılınca ölçülebilir olur.

---

## Prompt 4 — 6 yıldız evresini küçükten büyüğe yeniden tasarlama
```
Yıldız evrelerini baştan tasarla. Mevcut çalışan kısımları bozma, dosya tek HTML kalsın.

1. Tam 6 evre olsun ve küçükten büyüğe, gerçek boyut sırasına göre dizilsin:
   Yıldız Tozu (0-9), Meteor (10-29), Kuyruklu Yıldız (30-59), Sarı Cüce (60-99), Mavi Dev (100-149), Kırmızı Süper Dev (150-199). 200 büyüklükte süpernova patlasın.
2. Her evrenin kendine has bir görünümü olsun: toz için dönen zerreler; meteor için dönen kızgın kaya ve kıvılcım; kuyruklu yıldız için buzlu bir koma ve iki ayrı kuyruk (mavi iyon, altın toz); sarı cüce için dalgalanan korona ışınları; mavi dev için keskin ışınlar ve dış halka; kırmızı süper dev için nabız gibi atan parlaklık, yüzey püskürtmeleri ve koyu lekeler.
3. Renk büyüklüğe göre değişsin: gri-mavi, turuncu, turkuaz, sarı, mavi, kırmızı. Renk evrenin sonuna doğru bir sonrakine yumuşakça geçsin.
4. Yıldızın yarıçapı evre başlarında sırasıyla 5, 7,5, 10,5, 14,5, 19,5, 25 birim olsun ve evreler arasında yumuşakça büyüsün. Süpernovadan hemen önce 30 olsun.
5. Kuyruk uzunluğu evreye göre değişsin: kuyruklu yıldızda en uzun, toz evresinde en kısa.
6. Hangi galaksiyi yutabileceğim evre numarasına bağlı olsun (evre 1: sarmal, evre 2: eliptik, evre 3: kuasar, evre 4: dev, evre 5: süper, evre 6: hepsi).
Bütün sayıları kodun en üstünde ayarlanabilir sabitler olarak tut.
```
**Neden böyle yazdım:**
- "Tam 6 evre" ve "gerçek boyut sırasına göre": ilk sürümde sıralama yanlıştı (Mavi Dev, Kırmızı Dev'den sonra geliyordu). Bu ifade o hatayı önler.
- Her evre için ayrı görünüm tarifi: "farklı görünsün" demek yerine her birine özgü bir özellik verdim, yoksa hepsi aynı yıldızın rengi değişmiş hâli olarak kalır.
- Galaksi kuralını evre numarasına bağlamak: eşikler kodda birden fazla yerde kopyalanıp çelişmesin diye.

---

## Prompt 5 — Büyümeyi zorlaştırma
```
Yıldızın büyümesini zorlaştır. Mevcut çalışan kısımları bozma, dosya tek HTML kalsın. Şu an oyun çok kolay ve çok çabuk bir sonraki bölgeye geçiyor.

1. Genel büyüme çarpanı ekle: bir galaksiyi yutunca gelen büyüklük artışı, mevcut değerin %40'ı kadar olsun. Skor değişmesin.
2. Büyüdükçe küçük av az beslesin: yıldız bir evre büyüdükçe, o evrenin altındaki galaksi türünden alınan büyüme %30 azalsın, en az %15'i kalsın. (Örnek: Yıldız Tozu evresinde sarmal galaksi tam büyüme verir; Mavi Dev evresinde çok az verir.) Bunu ilk fark ettiğimde ekranda kısa bir ipucu göster.
3. Büyük evrelerde küçük galaksiler daha seyrek çıksın.
4. Her yeni bölgede büyüme %10 daha zor olsun, en fazla %40.
5. Hedef: iyi bir oyuncunun bir bölgeyi bitirmesi yaklaşık 2-4 dakika sürsün.
Sayıları kodun en üstünde ayarlanabilir sabitler olarak tut.
```
**Neden böyle yazdım:**
- Sorunu açıkça söyledim ("çok kolay ve çok çabuk"), böylece yapay zekâ çözümü doğru yönde tutar.
- "Skor değişmesin": büyümeyi yavaşlatırken puanın da düşmesini engeller.
- "En az %15'i kalsın": alt sınır olmazsa küçük galaksilerden büyüme sıfıra iner ve oyun tıkanabilir.
- Hedef süre (2-4 dakika) ölçülebilir olduğu için, otomatik bir botla süreyi ölçüp doğrulayabildim (22 saniyeden yaklaşık 107 saniyeye çıktı).

---

## Prompt 6 — Yeni ad ve klavye kontrolü
```
Oyunun adını "Kozmik Kıvılcım" olarak değiştir (sayfa başlığı, başlangıç ekranındaki büyük başlık ve erişilebilirlik etiketi). Başlangıç ekranına "Bir kıvılcımdan süpernovaya: galaksileri yut, büyü, patla." sloganını koy. Bilgisayarda ok tuşları ve W, A, S, D ile de yıldızı yönlendirebileyim; fare ve dokunmatik kontroller aynen çalışsın. Tuşa basılıyken yıldız o yöne fareyle aynı azami hızda gitsin, tuş bırakılınca dursun. Başlangıç ekranındaki ipucunu klavyeyi de içerecek şekilde güncelle. Mevcut çalışan kısımları bozma.
```
**Neden böyle yazdım:**
- Adın hangi yerlerde değişeceğini tek tek yazdım (başlık, ekran, etiket), yoksa biri unutulabilir.
- "Fare ve dokunmatik aynen çalışsın": yeni bir kontrol eklerken eskisinin bozulmasını önler.
- "Fareyle aynı azami hız": klavye kullananın avantajlı ya da dezavantajlı olmaması için.
- Ödevdeki "Bilgisayar (tuşlar)" başlığı ve kural listesiyle uyumlu olması için eklendi.

---

## Prompt 7 — Oyunun son adı
```
Oyunun adını "NovaBang" olarak değiştir (sayfa başlığı, başlangıç ekranındaki büyük başlık ve erişilebilirlik etiketi). Slogan aynı kalsın. Başka hiçbir şeyi değiştirme.
```
**Neden böyle yazdım:**
- Ad, "nova" (süpernova) ve "bang" (patlama) sözcüklerinden oluşur ve oyunun ana anına, yıldızın patlamasına gönderme yapar.
- Adın başka bir oyunla çakışıp çakışmadığı önce web aramasıyla kontrol edildi, aynı adlı bir oyun bulunamadı.
- "Başka hiçbir şeyi değiştirme" ile yalnızca ismin değişmesi, çalışan oyunun bozulmaması hedeflendi.
