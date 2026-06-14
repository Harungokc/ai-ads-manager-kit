# Meta Ads Skill — Claude Code

## Konsept

Bu skill Claude Code'a Meta Ads yönetim yetenekleri kazandırır. NotFair + meta-ads-mcp + claude-ads'in en iyi yanlarından birleştirilmiştir.

## Kullanım

```bash
claude "Instagram Ads'te yeni kampanya başlat"
claude "Meta Ads performans analizi yap"
claude "Learning Phase teşhisi"
```

## Araçlar

### Kampanya Yönetimi
- `create_campaign` — Yeni kampanya oluştur
- `pause_campaign` — Kampanya durdur
- `resume_campaign` — Kampanya başlat
- `update_campaign_budget` — Bütçe güncelle
- `duplicate_campaign` — Kampanya kopyala

### Reklam Yönetimi
- `create_adset` — Reklam seti oluştur
- `create_ad` — Reklam oluştur
- `get_ad_preview` — Reklam önizleme
- `upload_creative` — Görsel/video yükle

### Analitik
- `get_campaign_insights` — Kampanya metrikleri
- `get_adset_insights` — Reklam seti metrikleri
- `get_ad_insights` — Reklam metrikleri
- `get_breakdown` — Breakdown analizi
- `get_learning_phase` — Learning Phase durumu

### Optimizasyon
- `run_breakdown_analysis` — Breakdown Effect hesapla
- `suggest_budget_reallocation` — Bütçe önerisi
- `generate_creative_variants` — Creative varyasyonları

## Prompt Template

```
"Platform: Meta Ads
Hedef: [objective]
Hedef kitle: [audience]
Bütçe: [budget]
Reklam formatı: [format]
Aksiyon: [action]"
```

## Meta Marketing API v25.0 Uç Noktaları

- `/act_{ad_account_id}/campaigns` — Kampanya CRUD
- `/act_{ad_account_id}/adsets` — Reklam seti CRUD
- `/act_{ad_account_id}/ads` — Reklam CRUD
- `/{ad_id}/insights` — Performans verisi
- `/act_{ad_account_id}/advertiser_permissions` — Erişim kontrolü
