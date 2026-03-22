# Play Store Review Skill - Kullanım Kılavuzu 🚀

Bu eklenti (skill), Android uygulamanızın (Kotlin, Java, React Native, Expo, Flutter) **Google Play Geliştirici Politikaları** ve **Teknik Kalite Beklentilerine** uygun olup olmadığını yapay zeka ajanları (Claude, Cursor, vs.) aracılığıyla otomatik olarak analiz etmenizi sağlar.

## 🎯 Bu Eklenti Ne İşe Yarar?

Uygulamanızı Google Play Store'a göndermeden önce veya yeni bir özellik geliştirirken:
- Uygulamanızın **reddedilme (rejection)** veya **askıya alınma (suspension)** risklerini tespit eder.
- Android'e özgü teknik kısıtlamaları (API seviyeleri, SDK gereksinimleri) inceler.
- Yanlış kod mimarilerini (örneğin ödeme sistemini atlama, tehlikeli izin istekleri) doğrudan kod üzerinden bulup uyarır.

## ⚙️ Kurulum ve Entegrasyon

### 1. Claude Code ile Kullanım
Proje dizininize bir terminal açın ve şu komutları çalıştırın:
```bash
/plugin marketplace add enes-1/play-store-review-skill
/plugin install play-store-review@play-store-review
```

### 2. Cursor veya Diğer Ajanlar
Eğer Cursor veya Windsurf kullanıyorsanız terminalinizden:
```bash
npx skills add enes-1/play-store-review-skill
```

## 🗣️ Yapay Zeka ile Nasıl Konuşmalısınız? (Örnek İstekler)

Eklenti projenize kurulduğunda yapay zeka projenizdeki bu kurallardan haberdar olur. Aşağıdaki gibi Türkçe istemler (prompt) kullanarak otomatik kod incelemesi tetikleyebilirsiniz:

1. **Genel İnceleme (Store Gönderimi Öncesi):**
   > *"Projemi Google Play politikalarına göre genel bir incelemeden geçirir misin? Olası ret sebeplerini listele."*

2. **Gizlilik ve İzin Analizi:**
   > *"AndroidManifest.xml ve konum izni isteyen fonksiyonlarımı Gizlilik politikası kurallarına göre analiz et."*

3. **Satın Alma (In-App Purchase) Kontrolü:**
   > *"Uygulamamda dijital bir abonelik satıyorum. Play Store faturalandırma (Billing) kurallarını ihlal edip etmediğimi kontrol eder misin?"*

4. **Reklam ve Çocuk Politikası:**
   > *"Projeme AdMob entegre ettim, ancak uygulamam 'Çocuk' kategorisine girebilir. Families Policy kurallarına uygun mu test et."*

## 📁 Kurallar ve Kapsam

Bu AI Skill, **7 Ana Başlıktan** oluşur:

1. **Kısıtlı İçerik (`1-restricted-content.md`):** Kumar, yasa dışı servisler, nefret söylemi ve çocukları koruma (Families Policy).
2. **Taklit ve Fikri Mülkiyet (`2-impersonation-and-ip.md`):** Telif hakları ve tasarımsal taklit sorunları.
3. **Gizlilik ve Güvenlik (`3-privacy-and-security.md`):** Aşırı izin talepleri (SMS/Arama geçmişi vb.), belirgin veri izni açıklamaları (Prominent Disclosure).
4. **Para Kazanma ve Reklamlar (`4-monetization-and-ads.md`):** Google Play Billing zorunlulukları ve rahatsız edici tam ekran reklamlar.
5. **Mağaza Girişi (`5-store-listing-and-promotion.md`):** Yanıltıcı başlıklar (örn: "Bedava", "En iyi" kelimeleri) ve sahte 5 yıldız teşvikleri.
6. **Spam ve Minimum İşlevsellik (`6-spam-and-minimum-functionality.md`):** Sadece Webview olan veya sürekli çöken uygulamalar.
7. **Uygulama Kalitesi & Teknik Şartlar (`7-app-quality-and-vitals.md`):** Güncel Target API seviyesi, 64-bit desteği, ANR ve Çökme (Crash) sınırları.

---

> **💡 İpucu:** Yanıt sürelerini kısaltmak ve isabet oranını artırmak için AI'a doğrudan sorunun olduğu bölümü işaret edebilirsiniz. *(Örn: "Gizlilik ve Güvenlik (3. Kural) açısından mevcut kodumu değerlendir.")*
