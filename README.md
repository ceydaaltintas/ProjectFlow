# ProjectFlow

Ekip tabanlı proje takip sistemi — Gantt (Timeline) + Kanban (Tracker).

## Nasıl Çalıştırılır

### Yöntem 1: Doğrudan Tarayıcıda Aç
`index.html` dosyasını tarayıcıya sürükle-bırak. Hazır.

### Yöntem 2: VSCode Live Server
1. VSCode'da "Live Server" extension'ını kur
2. `index.html` dosyasını aç
3. Sağ alt köşede "Go Live" butonuna tıkla

### Yöntem 3: Local HTTP Server
```bash
# Python
python3 -m http.server 8080

# Node
npx serve .
```
Tarayıcıda: http://localhost:8080

## Supabase Bağlantısı

Dosya içindeki Supabase bilgileri zaten tanımlı:
- `SB_URL`: https://hailzmuaqyejjmrbxfik.supabase.co
- `SB_KEY`: sb_publishable_J-mn4WbxafSG4yoHdQu2kA_SvwOQy2o

Gerçek zamanlı senkronizasyon ve paylaşım özelliği çalışır durumda.

## Dosya Yapısı

```
projectflow-vscode/
├── index.html                    ← Tüm uygulama (tek dosya)
├── ProjectFlow_Analiz_Dokumani.docx  ← Kullanım kılavuzu
└── README.md                     ← Bu dosya
```

## Teknolojiler

- React 18 (CDN, Babel transpile)
- Supabase JS v2 (gerçek zamanlı senkronizasyon)
- SheetJS / xlsx (Excel import/export)
- html2canvas (PNG export)
- Pure CSS (framework yok)

## Önemli Notlar

- Veri tarayıcı localStorage + Supabase'de saklanır
- Proje paylaşımı: "🔗 Paylaş" → ?key=xxx formatında link
- Supabase'de `projects` tablosu ve `share_key` kolonu gereklidir
- Detaylar için `ProjectFlow_Analiz_Dokumani.docx` dosyasına bakın
