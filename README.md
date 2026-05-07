# ProjectFlow

Ekip tabanlı proje takip sistemi — Gantt (Timeline) + Kanban (Tracker).

## Dosya Yapısı

```
projectflow-vscode/
├── index.html                        ← Tüm uygulama (tek dosya, sıfır build)
├── ProjectFlow_Analiz_Dokumani.docx  ← Kullanım kılavuzu & analiz dokümanı
└── README.md                         ← Bu dosya
```

## Teknolojiler

| Kütüphane | Kullanım |
|---|---|
| React 18 (CDN) | UI, state yönetimi |
| Babel (CDN) | JSX transpile (build adımı yok) |
| Supabase JS v2 | Gerçek zamanlı senkronizasyon, bulut depolama |
| SheetJS / xlsx | Excel import/export |
| html2canvas | Gantt → PNG export |
| Pure CSS | Stil (framework yok) |

## Özellikler

**Dashboard**
- Aktif / gecikmiş / başlamadı / tamamlanan proje grupları
- Hero istatistik kartları ve proje kartları

**Timeline (Gantt)**
- Ekip bazlı görev planlama, ekip gruplamalı Gantt görünümü
- Destek ekipler: Görevlere birden fazla destek ekip atanabilir; Gantt filtresi destek ekipleri de kapsar
- Baseline takibi: gecikme / uzama / baseline sonrası görev renklendirmesi
- Bağımlı görev analizi (Impact Analysis) ve otomatik öteleme
- Gantt üzerinde yeni görev ekleme: ekip başlığındaki "+" butonu veya boş alana drag
- Bar resize: çubuğun sağ kenarını sürükleyerek süre değiştirme
- Ekip bazlı / tarihe göre sıralama toggle
- Görev kopyalama

**Tracker (Kanban)**
- To Do / In Progress / In Review / Completed sütunları
- Sürükle-bırak, ekip/tür/kişi filtreleri, ilerleme özeti

**Paylaşım**
- `?key=<shareKey>` formatında proje bazlı güvenli link
- İlk ziyarette Timeline sekmesi; daha önce Tracker seçilmişse Tracker
- Paylaşılan kullanıcı yalnızca o projeyi görür ve düzenleyebilir

**Excel import/export**
- Timeline: Görev / Ekip / Destek Ekipler / Süre / Başlangıç / Bitiş / Baseline Bitiş / Gecikme / Uzama
- Tracker: Ekip / Başlık / Tür / Statü / İlgili Görev / Sorumlu
- Import sırasında yeni ekipler (birincil ve destek) otomatik oluşturulur

## Veritabanı Kurulumu

Supabase üzerinde aşağıdaki tabloyu oluşturun:

```sql
create table projects (
  id         text primary key,
  name       text,
  share_key  text unique,
  data       jsonb,
  updated_at timestamptz default now()
);

-- Gerçek zamanlı senkronizasyon için
alter publication supabase_realtime add table projects;
```

`index.html` içindeki Supabase bağlantı bilgilerini (URL ve anon key) kendi projenize göre güncelleyin. Bu bilgileri kaynak kontrol sistemine eklemeyin.

## Veri Saklama

| Katman | Anahtar | Açıklama |
|---|---|---|
| localStorage | `pf_v15` | Çevrimdışı yedek |
| localStorage | `pf_owned_v1` | Kullanıcıya ait proje ID listesi |
| Supabase | `projects` tablosu | Birincil bulut depolama |

Uygulama açılışında localStorage ve Supabase verileri birleştirilir; Supabase önceliklidir.

## Geliştirme Notları

- Tüm uygulama tek `index.html` dosyasında; build adımı, paket yöneticisi veya bundler gerekmez.
- Dosyayı doğrudan tarayıcıda açabilir ya da GitHub Pages / Netlify gibi statik hosting üzerinde yayınlayabilirsiniz.
- Detaylı iş kuralları ve kullanım kılavuzu için `ProjectFlow_Analiz_Dokumani.docx` dosyasına bakın.
