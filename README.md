# 👻 Retro Pac-Man

HTML5 Canvas, JavaScript ve Firebase kullanılarak geliştirilmiş; liderlik tablosu, çoklu seviyeler ve mobil uyumluluk içeren modern bir Pac-Man klonu.

> 🕹️ [OYUNU CANLI OYNA](https://pacman-game-rose.vercel.app/) 🕹️

Tıklayın ve hemen tarayıcınızda oynayın!

---

# 🎮 Özellikler

- **3 Farklı Seviye:** Giderek zorlaşan harita tasarımları.

- **Akıllı Hayalet Yapay Zekası:**

    * 🔴 **Kırmızı:** Doğrudan oyuncuyu kovalar.

    * 🩷 **Pembe:** Pusu kurmaya çalışır.

    * 🟠 **Turuncu:** Rastgele hareket eder.

    * 💠 **Mavi:** Oyuncuyu sıkıştırmaya çalışır.

- 🏆 **Canlı Liderlik Tablosu:** Firebase Firestore tabanlı, anlık güncellenen en iyi 10 skor.

- 📱 **Tam Mobil Uyumluluk:** Dokunmatik ekranlar için kaydırma (swipe) kontrolleri.

- **Güçlendirmeler:** Büyük yemleri yiyerek hayaletleri avlayın!

- **Şık Bildirimler:** Toastify kütüphanesi ile modern kullanıcı deneyimi.

---

# 🛠️ Kullanılan Teknolojiler

- **Frontend:** HTML5, CSS3, Vanilla JavaScript (ES6+)

- **Oyun Motoru:** HTML5 Canvas API

- **Backend & Veritabanı:** Firebase (Authentication & Firestore)

- **Bildirimler:** Toastify.js

---

# 🚀 Kurulum ve Çalıştırma

Projeyi kendi bilgisayarınızda veya sunucunuzda çalıştırmak için aşağıdaki adımları izleyin.

**1. Projeyi Klonlayın**
``` bash
git clone [https://github.com/KULLANICI_ADINIZ/pacman-game.git](https://github.com/KULLANICI_ADINIZ/pacman-game.git)
cd pacman-game
```

**2. Firebase Yapılandırması (Önemli!)**

Projenin çalışması için bir `firebase-config.js` dosyasına ihtiyacınız var. Ana dizinde bu dosyayı oluşturun ve içine kendi Firebase bilgilerinizi ekleyin:

`firebase-config.js` içeriği:

``` javascript
export const firebaseConfig = {
    apiKey: "SENIN_API_ANAHTARIN",
    authDomain: "proje-id.firebaseapp.com",
    projectId: "proje-id",
    storageBucket: "proje-id.firebasestorage.app",
    messagingSenderId: "123456789",
    appId: "1:123456789:web:abcdef"
};
```

**3. Çalıştırın**

`index.html` dosyasını modern bir tarayıcıda açın veya bir yerel sunucu (Live Server vb.) başlatın.

---

# 🔥 Firebase Kurulum Rehberi

Oyunun Liderlik Tablosu özelliğinin çalışması için Firebase Konsolu'nda yapmanız gereken ayarlar:

**1. Proje Oluşturun:** [Firebase Console](https://console.firebase.google.com/)'a gidin ve yeni bir proje oluşturun.

**2. Web App Ekleyin:** Proje ayarlarına gidip bir Web Uygulaması ekleyin ve config bilgilerini alın.

**3. Authentication (Kimlik Doğrulama):**

- `Build` -> `Authentication` -> `Sign-in` method sekmesine gidin.

- **Anonymous** (Anonim) giriş seçeneğini etkinleştirin.

- `Settings` -> `Authorized domains` kısmına sitenizin yayınlanacağı domaini (örn: `kullaniciadi.github.io`) ekleyin.

4. **Firestore Database:**

- `Build` -> `Firestore Database` sekmesine gidin ve veritabanı oluşturun.

- **Rules (Kurallar)** sekmesine gidip aşağıdaki güvenli kuralları yapıştırın:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /leaderboard/{document=**} {
      // Herkes okuyabilir
      allow read: if true;
      
      // Sadece geçerli formatta ve oturum açmış kullanıcılar yazabilir
      allow create: if request.auth != null
                    && request.resource.data.name is string
                    && request.resource.data.name.size() > 0
                    && request.resource.data.name.size() <= 10
                    && request.resource.data.score is number;
      
      // Düzenleme ve silme yasak
      allow update, delete: if false;
    }
  }
}
```

---

# 📜 Lisans

Bu proje MIT Lisansı ile lisanslanmıştır.

Geliştirici: [Bora Kol](https://www.linkedin.com/in/borakol/)