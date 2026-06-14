# LinkedIn Ads Skill — Claude Code

## Konsept

Bu skill Claude Code'a LinkedIn Ads (B2B reklam) yönetim yetenekleri kazandırır.
`amekala/ads-mcp` (adspirer, 45 LinkedIn aracı) ve `danielpopamd/linkedin-ads-mcp`
(25 araç) yaklaşımlarından beslenir. B2B hedefleme ve Lead Gen odaklıdır.

## Kullanım

```bash
claude "LinkedIn'de yazılım yöneticilerine yönelik Lead Gen kampanyası kur, günlük 40$"
claude "LinkedIn kampanyalarımın sektör ve unvan bazında performansını analiz et"
claude "En düşük CTR'ye sahip LinkedIn reklamlarını bul ve iyileştirme öner"
```

## Araçlar

### Hesap & Kampanya
- `list_accounts` — Reklam hesaplarını listele
- `create_campaign` — Kampanya grubu + kampanya oluştur
- `update_campaign` — Bütçe / durum / teklif güncelle
- `pause_campaign` / `resume_campaign`

### Creative & Lead Gen
- `create_creative` — Sponsored Content / Message / Text Ads
- `create_lead_gen_form` — Lead Generation form oluştur
- `get_lead_forms` — Form yanıtlarını çek

### Hedefleme (B2B)
- `target_by_job_title` — Unvan bazlı
- `target_by_company` — Şirket / sektör / büyüklük
- `target_by_seniority` — Kıdem (junior → C-level)
- `matched_audiences` — Web sitesi / liste retargeting

### Analitik
- `get_campaign_performance` — Spend, impressions, clicks, CTR, CPC, CPM
- `get_demographics` — Job function, industry, seniority kırılımı
- `get_conversions` — Dönüşüm ve lead form performansı

## Prompt Template

```
Platform: LinkedIn Ads
Hedef: [BRAND_AWARENESS | WEBSITE_VISITS | ENGAGEMENT | LEAD_GENERATION | CONVERSIONS]
Hedef kitle: [unvan, sektör, şirket büyüklüğü, kıdem, beceri]
Bütçe: [günlük/toplam]
Format: [Sponsored Content | Message Ad | Text Ad | Lead Gen]
Aksiyon: [create | analyze | optimize]
```

## LinkedIn Marketing API Uç Noktaları

- `/rest/adAccounts` — Hesaplar
- `/rest/adCampaignGroups` — Kampanya grubu CRUD
- `/rest/adCampaigns` — Kampanya CRUD
- `/rest/creatives` — Creative CRUD
- `/rest/adAnalytics` — Performans/demografik rapor
- Auth: `Authorization: Bearer` + `LinkedIn-Version` header

## Kaynak

Araçlar `amekala/ads-mcp` (hosted, OAuth) veya `danielpopamd/linkedin-ads-mcp` (self-host)
üzerinden gelir. Kurulum: [`docs/MCP-KURULUM.md`](../docs/MCP-KURULUM.md).
