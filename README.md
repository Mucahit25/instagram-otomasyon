# Instagram otomatik paylaşım

> **Render eklemek:** `instagram-otomasyon/renderlar/` klasörüne at. Birden fazla görsel tek gönderide kaydırmalı olsun istiyorsan bir alt klasöre koy. İstersen klasöre `bilgi.txt` ekle (firma, fuar, şehir, m², ahşap/modüler).
>
> **Gerisi otomatik:** Sistem her gün kontrol eder. Yeni render varsa düzenler, logonu ekler, açıklamasını ve etiketlerini yazar, en uygun saate (Pazartesi akşam, Çarşamba akşam, Cuma sabah) koyar. Haftada 3 paylaşım.
>
> **Render bitince:** Sistem durur ve sana bir kez haber verir. Yeni render eklediğinde kaldığı yerden devam eder. Hiçbir render iki kez paylaşılmaz.

## Render nasıl eklenir (GitHub sitesinden)

1. Bu deponun sayfasında `instagram-otomasyon` → `renderlar` klasörüne gir.
2. Sağ üstte **Add file → Upload files**.
3. Renderları sürükle bırak. Kaydırmalı gönderi için: renderları bilgisayarında bir klasöre koy, klasörü komple sürükle.
4. Altta **Commit changes**'e bas. Sistem birkaç dakika içinde çalışır.

Ayrıntılı kurallar: `instagram-otomasyon/renderlar/NASIL-KULLANILIR.txt`.

## Onay modu

İlk haftalarda sistem gönderiyi Buffer'da **taslak** olarak açar ve sana önizleme maili atar. Sen Buffer'da taslağa bakıp önerilen saate planlarsın.

Kapatmak için: `instagram-otomasyon/config.yaml` içinde `onay_modu: true` satırını `onay_modu: false` yap. Bundan sonra gönderiler doğrudan planlanır, sen yine mail alırsın.

## Saatleri değiştirmek

`config.yaml` içinde `zaman_dilimleri` bölümü. Günler: pazartesi, sali, carsamba, persembe, cuma, cumartesi, pazar. Haftalık adet: `haftalik_adet`.

## Sistemi durdurmak

`config.yaml` içinde `aktif: true` satırını `aktif: false` yap. Hiçbir şey paylaşılmaz, kayıt korunur. Tekrar `true` yapınca kaldığı yerden devam eder.

## Elle çalıştırmak

Depo sayfasında **Actions → Instagram paylaşım → Run workflow**. "Deneme" kutusunu işaretlersen Buffer'a hiçbir şey gitmez, sadece önizleme maili gelir.

## Teknik not

- Akış: `instagram-otomasyon/src/main.py`. Görsel: `gorsel.py`, açıklama: `aciklama.py`, zamanlama: `zamanlama.py`, kayıt: `kayit.py`, Buffer: `yayinci/buffer.py`, bildirim: `bildirim.py`, git: `depo.py`.
- Kalıcı kayıt: `instagram-otomasyon/kayit/paylasimlar.json`. Elle düzenlenmez.
- Hazır görseller `instagram-otomasyon/hazir/<proje_id>/` içinde, Buffer onları commit SHA'lı `raw.githubusercontent.com` adresinden çeker. Bu yüzden depo herkese açık olmalı.
- Gizli değerler: Settings → Secrets and variables → Actions. `BUFFER_API_KEY`, `CLAUDE_CODE_OAUTH_TOKEN`, `GMAIL_ADRES`, `GMAIL_UYGULAMA_SIFRESI`, `BILDIRIM_EPOSTA`.
- Testler: `cd instagram-otomasyon && python -m pytest`.
- GitHub, 60 gün hiç hareket olmayan depolarda günlük çalışmayı durdurur. Yeni render yüklemek sistemi yine çalıştırır.
