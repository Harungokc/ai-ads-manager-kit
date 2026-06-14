# TikTok Ads Skill — Claude Code

## Konsept

Bu skill Claude Code'a TikTok Ads yönetim yetenekleri kazandırır. `amekala/ads-mcp`
(adspirer, 31 TikTok aracı) ve `AdsMCP/tiktok-ads-mcp-server` yaklaşımlarından beslenir.
Doğal dille kampanya kurma, rapor çekme ve optimizasyon yapar.

## Kullanım

```bash
claude "TikTok'ta yeni ürünüm için Traffic kampanyası başlat, günlük 30$, hedef 18-24"
claude "TikTok kampanyalarımın son 7 gün video tamamlanma oranını analiz et"
claude "Düşük performanslı TikTok ad group'larını listele ve duraklatmayı öner"
```

## Araçlar

### Kampanya Yönetimi
- `create_campaign` — Yeni kampanya oluştur (objective + bütçe)
- `get_campaigns` — Kampanyaları listele
- `update_campaign` — Bütçe / durum güncelle
- `pause_campaign` / `resume_campaign` — Duraklat / başlat

### Ad Group (Reklam Grubu)
- `create_adgroup` — Hedef kitle, yerleşim, bütçe, teklif
- `get_adgroups` — Reklam gruplarını listele
- `update_adgroup_budget` — Bütçe güncelle

### Creative (Reklam)
- `upload_video` — Video creative yükle
- `create_ad` — In-Feed / Spark / Carousel reklam oluştur
- `get_ad_preview` — Önizleme

### Analitik
- `get_campaign_performance` — Kampanya metrikleri
- `get_adgroup_performance` — Ad group metrikleri
- `get_video_metrics` — İzlenme, tamamlanma oranı, 2s/6s görüntüleme

## Prompt Template

```
Platform: TikTok Ads
Hedef: [REACH | TRAFFIC | VIDEO_VIEWS | CONVERSIONS | APP_PROMOTION]
Hedef kitle: [yaş, ilgi, davranış, bölge]
Bütçe: [günlük/toplam]
Creative: [In-Feed | Spark Ads | Carousel]
Aksiyon: [create | analyze | optimize]
```

## TikTok Marketing API v1.3 Uç Noktaları

- `/open_api/v1.3/campaign/create/` — Kampanya oluştur
- `/open_api/v1.3/campaign/get/` — Kampanya listele
- `/open_api/v1.3/adgroup/create/` — Reklam grubu oluştur
- `/open_api/v1.3/ad/create/` — Reklam oluştur
- `/open_api/v1.3/report/integrated/get/` — Performans raporu
- Auth: `Access-Token` header + `advertiser_id`

## Kaynak

Araçlar `amekala/ads-mcp` (hosted, OAuth) veya `AdsMCP/tiktok-ads-mcp-server` (self-host)
üzerinden gelir. Kurulum: [`docs/MCP-KURULUM.md`](../docs/MCP-KURULUM.md).
