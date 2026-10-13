# CS 1.6 WebAssembly (Xash3D FWGS) Projesi

Bu proje, **Aimflare** ve benzeri sitelerin tarayıcı üzerinde Counter-Strike 1.6 çalıştırmak için kullandığı **WebAssembly (WASM)** mimarisini içerir.

## Nasıl Çalışıyor?
1. **API Değil, Oyun Motoru:** Arka planda bir API çalışmaz. C/C++ ile yazılmış açık kaynaklı **Xash3D FWGS** motoru, **Emscripten** ile WebAssembly'ye (`xash.wasm`) derlenmiştir.
2. **WebGL Render:** Oyun grafikleri HTML5 `<canvas>` elementi üzerine WebGL 2 ile doğrudan ekran kartı kullanılarak çizilir.
3. **Oyun Dosyaları:** Haritalar (`.bsp`), modeller (`.mdl`) ve sesler CDN üzerinden parçalı zip (`valve.zip.part1..17`) olarak çekilip tarayıcının sanal belleğine (Emscripten MEMFS) yüklenir.
4. **Valorant Arayüzü / HUD:** Standart CS 1.6 HUD'ı gizlenip, HTML/CSS katmanları (`div#custom-hud`) oyun canvas'ının üzerine bindirilir.

## Nasıl Çalıştırılır?
WebAssembly ve CDN fetch işlemleri güvenlik (`CORS` ve `file://` kısıtlamaları) nedeniyle bir HTTP sunucusu gerektirir.

### 1. Python ile Yerel Sunucu Başlatma
Terminal veya PowerShell üzerinden proje dizininde şu komutu çalıştırın:
```bash
cd "C:\Users\eserh\.gemini\antigravity\scratch\cs16-web"
python -m http.server 8080
```

### 2. Tarayıcıda Açma
Tarayıcınızdan (Chrome, Edge vb.) şu adrese gidin:
```
http://localhost:8080/
```
"OYUNU BAŞLAT" butonuna bastığınızda dosyalar CDN'den belleğe indirilip oyun başlayacaktır.
