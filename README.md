🕹️ Kıvılcım: Arcade Zihin Oyunları

Lumosity'den ilham alan, tarayıcıda çalışan bir bilişsel oyun uygulaması. 37 kısa oyun, adaptif zorluk ve ilerleme takibi içerir. Kayıt, ücret ya da kurulum gerekmez.

Canlı sürüm: https://sayko89.github.io/kivilcim/
Youtube Link: https://youtu.be/r45NOQXBVIg

Öne çıkanlar
37 oyun, 6 kategori: Hafıza, Dikkat, Esneklik, Problem Çözme, Görsel Algı, Uzamsal Akıl Yürütme
Kullanıcı geri bildirimlerine dayalı tasarım: 49.703 Lumosity yorumu analiz edildi. Ödeme duvarı, zorunlu kayıt, talimat eksikliği ve erişilebilirlik gibi en sık şikâyetlere çözüm üretildi.
Adaptif zorluk: Oyun içinde kademeli artar; oyunlar arasında aynı seviyedeki son 3 oyunun doğruluğuna göre ayarlanır (>%90 artır, <%60 azalt).
Her oyunda: kısa tutorial, puansız deneme turu, skor, doğruluk, tepki süresi, seviye ve oyuna özel metrikler
İlerleme ekranı: oyun bazında skor, doğruluk, tepki ve seviye grafikleri
Erişilebilirlik: renk körü dostu mod, büyük dokunma alanları, klavye desteği, ses kapatma
Gizlilik: tüm veriler yalnızca kullanıcının tarayıcısında (localStorage) saklanır.
Teknik yapı
Tek dosyalık, bağımlılıksız HTML/CSS/JavaScript; oyun başladıktan sonra ağ isteği yapılmaz.
Ortak GameSession motoru: zamanlayıcı, skor, seviye, doğruluk ve oyun sonu mantığını tüm oyunlar paylaşır.
Her oyun register() ile eklenen bağımsız bir modüldür; yeni oyun eklemek mevcut kodu değiştirmeyi gerektirmez.
Skor ve adaptif zorluk hesapları DOM'dan bağımsız, saf ve test edilebilir fonksiyonlardır (Core).

Veri modeli (her oyun sonucu):

userId, gameId, score, accuracy, reactionTime, level, startLevel, mistakes, timestamp, input, extra
Not

Bu uygulama tıbbi ya da psikolojik bir değerlendirme yapmaz; skorlar yalnızca oyun içi performansı gösterir.
