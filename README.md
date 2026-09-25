# AI Prayer Reminder

Frontend statis untuk pengingat sholat berbasis lokasi menggunakan AlAdhan Prayer Times API. Kamera dan AI hanya digunakan sebagai bantuan visual; aplikasi tidak menilai sah/tidaknya ibadah dan tidak mengunci perangkat.

## Jalankan web secara aman

Geolocation dan kamera membutuhkan secure context. Gunakan localhost, bukan `file://`:

```bash
npm install
npx serve www
```

Buka URL localhost yang ditampilkan. Alternatif deployment HTTPS: GitHub Pages, Cloudflare Pages, Netlify, atau Vercel.

## Model Teachable Machine

Edit `www/script.js` dan ganti:

```js
const MODEL_URL = "GANTI_DENGAN_URL_MODEL_TEACHABLE_MACHINE/";
```

dengan URL model Anda yang memiliki `model.json` dan `metadata.json`.

## Capacitor Android

```bash
npm install
npm install @capacitor/core @capacitor/cli @capacitor/android
npx cap init
npx cap add android
npx cap sync android
npx cap open android
```

Setelah perubahan web, jalankan kembali `npx cap sync android`. Di Android Studio pilih **Build → Build Bundle(s) / APK(s) → Build APK(s)**. APK debug biasanya berada di `android/app/build/outputs/apk/debug/app-debug.apk`. Untuk distribusi gunakan **Generate Signed Bundle / APK** dan simpan keystore secara aman.

Android memerlukan permission lokasi dan kamera. Jangan meminta permission yang tidak digunakan. Background alarm saat aplikasi benar-benar ditutup memerlukan implementasi native Android; JavaScript timer tidak menjamin alarm berjalan setelah WebView ditutup.

## Privacy

Lokasi digunakan untuk request jadwal AlAdhan. Video tidak direkam, disimpan, atau diupload oleh aplikasi. Model inference dilakukan di browser/WebView jika tersedia. API pihak ketiga tetap memiliki kebijakan pemrosesan datanya sendiri.
