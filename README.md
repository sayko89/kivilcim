#  Kıvılcım: Arcade Zihin Oyunları

**Kıvılcım**, Lumosity'den ilham alan, tarayıcıda çalışan bir bilişsel oyun uygulamasıdır. 6 kategoride 37 kısa oyun, oyuncunun performansına uyum sağlayan zorluk sistemi ve ayrıntılı ilerleme takibi sunar. Kayıt, ücret ya da kurulum gerektirmez; telefonda da bilgisayarda da açılır açılmaz oynanır.

🎮 **Canlı sürüm:** https://sayko89.github.io/kivilcim/
📁 **Kaynak kod:** https://github.com/sayko89/kivilcim
🕹️ **Youtube link:** https://youtu.be/r45NOQXBVIg

> Bu uygulama tıbbi ya da psikolojik bir değerlendirme yapmaz. Skorlar yalnızca oyun içi performansı gösterir.

---

## İçindekiler

1. [Projenin amacı](#1-projenin-amacı)
2. [Kullanıcı geri bildirimi analizi](#2-kullanıcı-geri-bildirimi-analizi)
3. [Lumosity'den farkları](#3-lumositynin-eksikleri-ve-kıvılcımın-çözümleri)
4. [Oyunlar](#4-oyunlar)
5. [Oyun akışı](#5-oyun-akışı)
6. [Puanlama ve ölçülen metrikler](#6-puanlama-ve-ölçülen-metrikler)
7. [Adaptif zorluk sistemi](#7-adaptif-zorluk-sistemi)
8. [Veri modeli ve ilerleme takibi](#8-veri-modeli-ve-ilerleme-takibi)
9. [Teknik mimari](#9-teknik-mimari)
10. [Yeni oyun ekleme](#10-yeni-oyun-ekleme)
11. [Tasarım ve erişilebilirlik](#11-tasarım-ve-erişilebilirlik)
12. [Test](#12-test)
13. [Yerel olarak çalıştırma](#13-yerel-olarak-çalıştırma)
14. [Bilinen sınırlar ve yol haritası](#14-bilinen-sınırlar-ve-yol-haritası)

---

## 1. Projenin amacı

Projenin hedefi Lumosity'yi birebir kopyalamak değil, kullanıcıların Lumosity hakkında en çok şikâyet ettiği noktaları tespit edip bunları gideren özgün bir web uygulaması geliştirmektir. Oyun mekaniklerinden ilham alınmıştır; isim, logo, görsel tasarım ve oyun adları tamamen özgündür.

## 2. Kullanıcı geri bildirimi analizi

Tasarım kararları, [`seyyah/challenge1`](https://github.com/seyyah/challenge1) deposunda paylaşılan **49.703 Google Play yorumunun** (Haziran 2014 – Eylül 2026) analizine dayanır.

**Yıldız dağılımı**

| Puan | Yorum sayısı | Oran |
|---|---:|---:|
| ⭐⭐⭐⭐⭐ | 32.595 | %65,6 |
| ⭐⭐⭐⭐ | 8.381 | %16,9 |
| ⭐⭐⭐ | 2.938 | %5,9 |
| ⭐⭐ | 1.640 | %3,3 |
| ⭐ | 4.149 | %8,3 |

Uygulama genel olarak seviliyor; oyunların kendisi övülüyor. Sorunlar oyunları çevreleyen deneyimde yoğunlaşıyor. 1–3 yıldızlı yaklaşık 8.700 yorumda anahtar kelime taramasıyla öne çıkan temalar:

| Tema | Olumsuz yorumlardaki payı | Not |
|---|---|---|
| Fiyat / ödeme duvarı | ~%30 | 12 yıl boyunca sabit kalan en büyük şikâyet |
| Zorunlu hesap / giriş sorunları | ~%11–14 | E-posta zorunluluğu, yaş sınırı, giriş hataları |
| Az oyun / tekrar | ~%7–10 | Her gün aynı oyunlar, çabuk sıkıcı olma |
| Talimat eksikliği | 2017–2021'de ~%8 | "Nasıl oynanacağını söylemiyor" |
| Teknik hatalar | son yıllarda ~%7 | Açılmama, donma, kısa süre |

Daha az sayıda ama somut istekler: renk körlüğü modu, ses kapatma, büyük butonlar, yatay ekran desteği, günlük antrenmanda oyun değiştirebilme, dokunmatik ve klavye skorlarının ayrı tutulması, ilerleme grafikleri.

*Oranlar anahtar kelime eşleştirmesiyle hesaplanmış yaklaşık değerlerdir; bir yorum birden fazla temaya girebilir.*

## 3. Lumosity'nin eksikleri ve Kıvılcım'ın çözümleri

| Kullanıcı şikâyeti | Kıvılcım'daki çözüm |
|---|---|
| Ödeme duvarı, günlük oyun sınırı | Tamamen ücretsiz, tüm oyunlar açık |
| Zorunlu kayıt, yaş sorulması | Hesap yok; veriler yalnızca tarayıcıda |
| Aynı oyunların tekrarı | 37 oyun; günlük antrenmanda her oyun "Değiştir" ile değiştirilebilir |
| Kuralların anlatılmaması | Her oyun öncesi adım adım tutorial ve puansız deneme turu |
| Yanlıştan sonra süre kaybı | Geri bildirim gösterilirken süre durur |
| Renk körlüğü | Renk körü dostu mod; doğru/yanlış hem renk hem ✓/✗ ile gösterilir |
| Ses kapatılamaması | Oyun içinde tek dokunuşla ses kapatma |
| Dokunmatik skorların düşük çıkması | Skorlar giriş yöntemine (dokunmatik, fare, klavye) göre ayrı tutulur |
| Abartılı bilimsel iddialar | "Beyni geliştirir" yerine "oyun içi performansını takip et" dili |

## 4. Oyunlar

Her oyun yaklaşık 1–3 dakika sürer.

### 🧠 Hafıza (8)

| Oyun | Beceri | Süre | Açıklama |
|---|---|---|---|
| Hafıza ızgarası | Görsel hafıza | 8 tur | Kısa süre yanan kareleri hatırla ve aynılarını seç. |
| Kaybolan Rota | Görsel hafıza | ~2 dk, 5 tur | Birkaç saniye görünen rotayı hatırla ve başlangıçtan hedefe yeniden çiz. |
| Sahte Hatıra | Çalışma belleği | ~2 dk, 2 hikâye | Kısa bir hikâyeyi oku; neyin anlatıldığını, neyin anlatılmadığını ayırt et. |
| Değişeni Bul | Görsel hafıza | ~2 dk, 8 tur | Bir sahneyi ezberle; tekrar göründüğünde değişen nesneyi bul. |
| N-Geri | Çalışma belleği | 60 sn | Harf akışında her harfin N adım öncekiyle aynı olup olmadığını söyle. |
| Sıra Hafızası | Sıralı hafıza | ~2 dk, 8 tur | Yanan düğmelerin sırasını tekrarla; her doğru turda dizi uzar. |
| Rakam Dizisi | Kısa süreli bellek | ~2 dk, 6 tur | Gösterilen rakamları yaz; ileri seviyede tersten. |
| Kart Eşleştir | Görsel-uzamsal hafıza | ~1–2 dk | Kartları çevir, aynı resimleri eşleştir. |

### ⚡ Dikkat (6)

| Oyun | Beceri | Süre | Açıklama |
|---|---|---|---|
| Anlam mı, renk mi? | Dikkat ve odak | 45 sn | Kelimenin anlamı ile rengi eşleşiyor mu? (Stroop) |
| Çift Görev | Bölünmüş dikkat | 60 sn | Solda tek sayıları, sağda mavi daireleri aynı anda yakala. |
| Trafik Kontrol | Karar verme ve dikkat | 75 sn | Kavşağın ışıklarını yönet, kazaları önle, ambulanslara yol aç. |
| Ok Yönü | Seçici dikkat | 45 sn | Yalnızca ortadaki okun yönüne göre karar ver (Flanker). |
| Köstebek Avı | Tepki hızı ve ketleme | 45 sn | Köstebeklere dokun, kirpilere dokunma. |
| Sayı Avı | Görsel tarama | ~1–2 dk | Tablodaki sayıları sırayla bul (Schulte tablosu). |

### 🔄 Esneklik (3)

| Oyun | Beceri | Süre | Açıklama |
|---|---|---|---|
| Kural Değişti | Bilişsel esneklik | 60 sn | Şekilleri kurala göre ayır; kural sessizce değişir, fark et ve uyum sağla. |
| Sayı mı, Harf mi? | Görev değiştirme | 60 sn | Kartın yerine göre sayıya ya da harfe bak. |
| Ters Köşe | Ketleme ve esneklik | 45 sn | Komutu uygula; "TERS" kartında tersini yap. |

### 🧩 Problem Çözme (10)

| Oyun | Beceri | Süre | Açıklama |
|---|---|---|---|
| Hızlı hesap | Sayısal işlem | 45 sn | İşlemin sonucunu dört seçenek arasından bul. |
| Sayı Dedektifi | Örüntü tanıma | ~2 dk, 10 soru | Sayı ve sembol dizilerindeki kuralı çöz. |
| Sudoku | Mantıksal akıl yürütme | ~2–4 dk | 4×4'ten 9×9'a, tek çözümlü bulmacalar. |
| Kelime Bulmacası | Sözel akıl yürütme | ~2–3 dk | Her oyunda yeniden üretilen Türkçe çapraz bulmaca. |
| Para Üstü | Günlük matematik | ~1–2 dk | Alışveriş fişinden para üstünü hesapla. |
| Kesir Karşılaştır | Oran ve büyüklük | ~1–2 dk | Hangi kesir büyük, yoksa eşitler mi? |
| Harf Karıştır | Sözel akıcılık | 90 sn | Karışık harflerden kelime kur. |
| Hanoi Kulesi | Planlama | ~1–3 dk | Diskleri kurallara uyarak en az hamleyle taşı. |
| Terazi | Mantıksal çıkarım | ~2 dk, 8 soru | Dengedeki terazilerden eksik ağırlığı bul. |
| Eş mi, Zıt mı? | Sözel akıl yürütme | 60 sn | Kelimenin eş ya da zıt anlamlısını bul. |

### 👁️ Görsel Algı (4)

| Oyun | Beceri | Süre | Açıklama |
|---|---|---|---|
| Aynı mı? | İşleme hızı | 45 sn | Yeni şekil bir öncekiyle aynı mı? |
| Kalabalıkta Hedef | Görsel dikkat | ~1,5 dk, 10 tur | Onlarca benzer şeklin arasındaki tek farklıyı bul. |
| Farklı Ton | Görsel ayırt etme | 45 sn | Tonu biraz farklı olan kareyi bul; fark giderek incelir. |
| Nokta Tahmini | Sayısal sezgi | 45 sn | Saymadan, hangi kutuda daha çok nokta olduğuna karar ver. |

### 🗺️ Uzamsal Akıl Yürütme (6)

| Oyun | Beceri | Süre | Açıklama |
|---|---|---|---|
| Hafıza Haritası | Uzamsal hafıza | ~2 dk, 4 tur | Ada haritasında gösterilen rotayı tekrar oluştur. |
| Zihinsel Tetris | Zihinsel döndürme | ~2 dk, 10 soru | Şeklin döndürülmüş halini, ayna görüntüsünden ayırt et. |
| Labirent | Uzamsal planlama | ~1–3 dk | Her oyunda yeni üretilen labirentten en kısa yoldan çık. |
| Saat Okuma | Uzamsal yorumlama | ~1–2 dk | Analog saati oku; ileri seviyede zamanı ileri al. |
| Pusula | Yön takibi | ~2 dk, 10 soru | Dönüş komutlarını zihninde takip et. |
| Ayna mı? | Zihinsel döndürme | 45 sn | Döndürülmüş harf normal mi, ayna görüntüsü mü? |

## 5. Oyun akışı

```
Ana sayfa ─► Tutorial ─► (Deneme turu) ─► Oyun ─► Sonuç ekranı ─► Tekrar oyna / Sıradaki oyun
```

- **Ana sayfa:** Her gün rastgele seçilen 3 oyunluk günlük antrenman, seri sayacı ve kategorilere göre süzülebilen tüm oyunlar. Her kartta oyun adı, açıklama, hedeflenen beceri, en yüksek skor, son skor, mevcut seviye ve "Oyna" butonu yer alır.
- **Tutorial:** Kurallar adım adım anlatılır. İlk açılışta puansız bir deneme turu önerilir; deneme turunda yanlış cevapların nedeni açıklanır.
- **Oyun ekranı:** Skor, seviye göstergesi, süre ya da tur çubuğu, ses kapatma ve çıkış butonu. Oyundan istenildiği an çıkılabilir; tüm zamanlayıcılar güvenle temizlenir.
- **Sonuç ekranı:** "Tamamlandı!" başlığıyla skor, doğruluk, ortalama tepki süresi, ulaşılan seviye ve oyuna özel metrikler gösterilir. Geçmiş performansla karşılaştırmalı bir mesaj verilir; örneğin *"Önceki oyuna göre tepki süren %8 iyileşti."* ya da *"Bu oyunda önceki en yüksek skorunu geçtin!"*

## 6. Puanlama ve ölçülen metrikler

**Temel puan formülü** (deterministik, `Core.points`):

```
puan = 10 + 2 × (seviye − 1) + 5 × min(seri − 1, 6)
```

Doğru cevap serisi (combo) puanı artırır; seri bonusu 6'da tavan yapar. Bazı oyunlar tamamlama bonusu ya da oyuna özgü puan kullanır (örneğin Hanoi Kulesi'nde hamle verimliliği, Labirent'te rota verimliliği).

**Her oyunda tutulan ortak metrikler:** skor, doğruluk oranı, ortalama tepki süresi, ulaşılan seviye, hata sayısı.

**Oyuna özgü metriklerden örnekler:**

| Oyun | Ek metrik |
|---|---|
| Kural Değişti | Kural değişiminden sonraki ortalama uyum süresi ve deneme sayısı |
| Ok Yönü | Dikkat dağılma etkisi (uyumsuz − uyumlu tepki süresi) |
| Sayı mı, Harf mi? | Görev geçiş maliyeti |
| Sahte Hatıra | Yanlış hatırlama oranı (anlatılmayan olaya "Evet" deme) |
| Çift Görev | Sol ve sağ görev doğruluğu ayrı ayrı |
| Trafik Kontrol | Kazasız geçen araç, ortalama karar süresi, akış verimliliği |
| Labirent | Çıkmaz yola girme, gereksiz adım, rota verimliliği |
| Ayna mı? | Küçük ve büyük dönme açılarında tepki süresi |

## 7. Adaptif zorluk sistemi

Zorluk iki katmanda ayarlanır:

**Oyun içi:** Oyunlar performansa göre kademeli olarak zorlaşır ya da kolaylaşır. Örneğin Kaybolan Rota'da hatasız tamamlanan rota bir sonrakinde uzar, Sıra Hafızası'nda doğru tekrar edilen dizi bir adım büyür.

**Oyunlar arası:** Bir sonraki oyunun başlangıç seviyesi, o seviyede oynanan son 3 oyunun ortalama doğruluğuna göre belirlenir:

| Son oyunlardaki ortalama doğruluk | Karar |
|---|---|
| > %90 | Seviye 1 artar |
| %60 – %90 | Seviye korunur |
| < %60 | Seviye 1 azalır |

Deneyimi bozmamak için karar en az 2 oyun sonunda verilir ve yalnızca mevcut seviyede oynanan oyunlar hesaba katılır. Böylece tek bir iyi ya da kötü oyun seviyeyi oynatmaz.

```js
function nextStartLevel(cur, history, max) {
  const w = history.filter(h => h.startLevel === cur).slice(-3);
  if (w.length < 2) return cur;
  const a = mean(w.map(h => h.accuracy));
  if (a > 0.9) return Math.min(max, cur + 1);
  if (a < 0.6) return Math.max(1, cur - 1);
  return cur;
}
```

## 8. Veri modeli ve ilerleme takibi

Her oyun sonucu tarayıcının `localStorage` alanında şu yapıyla saklanır:

```json
{
  "id": "r1abc23",
  "userId": "u-k3j9x2a1",
  "gameId": "rota",
  "score": 850,
  "accuracy": 0.92,
  "reactionTime": 1240,
  "level": 7,
  "startLevel": 6,
  "mistakes": 3,
  "timestamp": 1791053723061,
  "input": "dokunmatik",
  "extra": { "maxRoute": 12, "bestCombo": 9 }
}
```

- `userId`: hesap gerektirmeyen, cihaza özgü anonim kimlik
- `reactionTime`: milisaniye cinsinden ortalama tepki süresi
- `input`: dokunmatik, fare ya da klavye; skorlar bu alana göre ayrı karşılaştırılır
- `extra`: oyuna özgü metrikler

**İlerleme ekranı:** günlük seri, toplam oyun, son 7 günün takvimi ve oyun bazında skor, doğruluk, tepki süresi ve seviye grafikleri ile oturum geçmişi tablosu.

## 9. Teknik mimari

Uygulama tek bir HTML dosyasından oluşur; framework ya da derleme adımı gerektirmez. Oyun başladıktan sonra hiçbir ağ isteği yapılmaz.

| Katman | Sorumluluk |
|---|---|
| **Core** | DOM'dan bağımsız, saf fonksiyonlar: puanlama, özet çıkarma, adaptif zorluk, karşılaştırma mesajları |
| **Kayıt defteri (Registry)** | Oyunların `register()` ile sisteme eklenmesi; ana sayfa ve kategoriler buradan otomatik oluşur |
| **GameSession** | Tüm oyunların ortak motoru: zamanlayıcı, skor, seri, seviye, doğruluk, tepki süresi, oyun sonu ve güvenli temizlik |
| **quiz() yardımcısı** | Seçenekli oyunlar için ortak soru–cevap döngüsü (klavye kısayolları, geri bildirim, deneme turu) |
| **Görünümler** | Ana sayfa, tutorial, oyun, sonuç, ilerleme, ayarlar |
| **Depolama** | `localStorage`; eski sürüm kayıtları yeni veri modeline otomatik taşınır |

GameSession'ın oyunlara sunduğu başlıca API:

```js
s.hit({ rt })          // doğru cevap: puan, seri, tepki süresi
s.miss()               // hata: seri sıfırlanır
s.setLevel(n)          // oyun içi seviye değişimi
s.timer(ms)            // duraklatılabilir geri sayım
s.later(fn, ms)        // oyundan çıkınca otomatik iptal edilen zamanlayıcı
s.loop(fn)             // animasyon döngüsü (requestAnimationFrame)
s.key(fn)              // klavye kısayolları
s.end()                // sonucu kaydet, adaptif zorluğu güncelle, sonuç ekranını göster
```

Rastgele üretilen içerikler: Sudoku (tek çözüm garantili), kelime bulmacası yerleşimi, labirentler, Kaybolan Rota yolları, ada haritaları, Sahte Hatıra hikâyeleri ve Zihinsel Tetris şekilleri her oyunda yeniden üretilir.

## 10. Yeni oyun ekleme

Yeni bir oyun eklemek için mevcut kodu değiştirmek gerekmez; yeni bir `register()` çağrısı yeterlidir:

```js
K.register({
  id: 'ornek',
  name: 'Örnek Oyun',
  cat: 'dikkat',                 // hafiza | dikkat | esneklik | problem | gorsel | uzamsal
  skill: 'Seçici dikkat',
  glyph: 'star',
  len: '45 saniye',
  desc: 'Kartta gösterilecek kısa açıklama.',
  tutorial: () => ['Adım 1', 'Adım 2'],
  stats: e => [['Ek metrik', e.deger]],
  run(s) {
    K.quiz(s, {
      duration: 45000,
      practiceN: 3,
      gen: () => ({
        html: '<div class="card">?</div>',
        options: K.YN,
        correct: 'y',
        explain: 'Deneme turunda gösterilecek açıklama.'
      })
    });
  }
});
```

Oyun otomatik olarak ana sayfada kendi kategorisinde görünür; tutorial, deneme turu, sonuç ekranı, ilerleme grafikleri ve adaptif zorluk ek kod yazmadan çalışır.

## 11. Tasarım ve erişilebilirlik

- **Arcade teması:** koyu zemin, neon renk paleti, piksel yazı tipi (Press Start 2P), retro terminal yazı tipi (VT323), CRT tarama çizgileri ve basılınca içeri çöken butonlar
- **Responsive:** telefon, tablet ve masaüstünde çalışır; telefon yatay çevrildiğinde oyun düzeni yan yana geçer
- **Renk körü dostu mod:** renge dayanan oyunlar konum, desen ya da şekil kullanır
- **Klavye desteği:** oyunların çoğu ok tuşları, rakamlar ve Boşluk ile oynanabilir; tüm butonlara Tab ile ulaşılabilir
- **Dokunma alanları:** etkileşimli öğeler en az 44 piksel
- **Hareket azaltma:** sistem ayarında hareket azaltma açıksa animasyonlar ve tarama çizgisi efekti kapanır
- **Gizlilik:** hesap, çerez ya da sunucu yok; "Ayarlar" ekranından tüm veriler tek tıkla silinebilir

## 12. Test

- Puanlama ve adaptif zorluk fonksiyonları Node.js üzerinde birim testleriyle doğrulandı.
- 37 oyunun tamamı headless Chromium (Playwright) üzerinde otomatik botlarla baştan sona oynatıldı; JavaScript hatası olmadan sonuç ekranına ulaşıldığı doğrulandı.
- Sudoku, Kelime Bulmacası, Labirent ve Hanoi Kulesi, çözüm algoritmalarıyla çalışan botlar tarafından eksiksiz çözüldü.

## 13. Yerel olarak çalıştırma

Kurulum gerekmez:

1. Depoyu indir ya da klonla: `git clone https://github.com/sayko89/kivilcim.git`
2. `index.html` dosyasını tarayıcıda aç.

Yazı tipleri Google Fonts'tan yüklenir; internet yoksa sistem yazı tipleri kullanılır ve oyunlar çalışmaya devam eder.

## 14. Bilinen sınırlar ve yol haritası

**Bilinen sınırlar**
- Veriler tarayıcıya bağlıdır; cihazlar arasında taşınmaz ve tarayıcı verisi silinirse kaybolur.
- Oyun içi zorluk eşikleri tahmini değerlerdir; gerçek kullanıcı verisiyle ayarlanmaları gerekir.
- Sahte Hatıra şablonla hikâye ürettiği için uzun kullanımda cümle yapıları tekrar edebilir.
- Kategori dağılımı dengesizdir (Problem Çözme 10, Esneklik 3 oyun).

**Yol haritası**
- Esneklik ve Görsel Algı kategorilerine yeni oyunlar
- Dairesel labirent ve perspektifli Zihinsel Tetris
- Arkadaşla ya da sınıfça yarışma modu
- Günlük hatırlatıcı bildirimi (PWA)
- İsteğe bağlı bulut senkronizasyonu
