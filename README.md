# ProjectFlow

Ekip tabanlı proje takip sistemi — Gantt (Timeline) + Kanban (Tracker).

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
