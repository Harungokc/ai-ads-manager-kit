# n8n Kurulum Rehberi

n8n — açık kaynak workflow otomasyon platformu (Zapier/Make alternatifi, self-hosted ve
ücretsiz). Bu kitteki `workflows/` JSON'larını import edip, reklam raporlama ve
optimizasyonunu **zamanlanmış** olarak otomatikleştirmek için kullanılır.

> Bu kitteki workflow'lar AI yorumlaması için **Claude API**'yi kullanır (HTTP Request +
> Header Auth). Aşağıda credential kurulumu adım adım anlatılır.

---

## 1. n8n'i Kur

### Docker ile (önerilen)
```bash
docker run -d --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n docker.n8n.io/n8nio/n8n
```
Tarayıcıda aç: **http://localhost:5678** → ilk girişte yerel hesap oluştur.

### npm ile
```bash
npm install -g n8n
n8n start
```

### n8n Cloud
[n8n.io](https://n8n.io) → Start free (kurulum istemiyorsan).

---

## 2. Claude API Credential'ı Ekle (workflow'lar için zorunlu)

Workflow'lardaki "Claude" node'ları bir **Header Auth** credential'ı bekler:

1. n8n → **Credentials** → **Add credential** → **Header Auth**
2. **Name:** `Anthropic API (x-api-key)`
3. **Header Name:** `x-api-key`
4. **Header Value:** `sk-ant-...` (Claude API anahtarın — [console.anthropic.com](https://console.anthropic.com/settings/keys))
5. Kaydet.

> `anthropic-version` ve `content-type` header'ları workflow içinde zaten tanımlı —
> sadece bu Header Auth credential'ını node'lara bağlaman yeterli.

---

## 3. Platform API Credential'ları

Workflow'lar reklam verisini doğrudan platform API'lerinden çeker. Gereken değerler `.env`
mantığıyla aynıdır; n8n'de ya **HTTP Request node'una expression** ile ya da n8n
credential olarak verilir:

| Workflow | Platform | Gereken |
|----------|----------|---------|
| 1, 3 | Meta Ads | `META_ACCESS_TOKEN`, `META_AD_ACCOUNT_ID` |
| 2, 3 | Google Ads | `GOOGLE_ADS_DEVELOPER_TOKEN`, OAuth `access_token`, `GOOGLE_ADS_CUSTOMER_ID` |
| 4 | TikTok Ads | `TIKTOK_ACCESS_TOKEN`, `TIKTOK_ADVERTISER_ID` |
| 5 | LinkedIn Ads | `LINKEDIN_ACCESS_TOKEN`, `LINKEDIN_AD_ACCOUNT_ID` |

> n8n'de ortam değişkeni kullanmak için `{{ $env.DEGISKEN }}` expression'ı çalışır
> (workflow'larda bu şekilde tanımlı). Docker'da `-e META_ACCESS_TOKEN=...` ile geçir.

---

## 4. Workflow'ları Import Et

1. n8n → **Workflows** → **Import from File**
2. `workflows/` klasöründen ilgili JSON'u seç
3. Node'lardaki `REPLACE` credential'larını kendi credential'larınla eşle
4. **Test workflow** ile dene → **Active** yap

### Mevcut Workflow'lar
| Dosya | Ne yapar |
|-------|----------|
| `1-meta-kampanya-olustur.json` | Meta'da kampanya oluşturur (PAUSED) + Claude optimizasyon önerisi |
| `2-google-ads-optimize.json` | Her gün Google Ads son 7 gün performansını çeker → Claude analiz |
| `3-cross-platform-report.json` | Haftalık Meta + Google verisini birleştirir → Claude karşılaştırmalı rapor |
| `4-tiktok-rapor.json` | Günlük TikTok performans raporu → Claude analiz |
| `5-linkedin-rapor.json` | Haftalık LinkedIn (B2B) performans raporu → Claude analiz |

> Rapor workflow'larının çıktısını bir **Gmail / Slack / Telegram** node'una bağlayarak
> raporu otomatik gönderebilirsin.

---

## 5. Örnek Akış (Workflow 3)

```
[Schedule: Her Pazartesi 09:00]
        ↓
[Meta — Son 7 Gün]   [Google — Son 7 Gün]   (paralel HTTP)
        ↓                     ↓
        └──────► [Verileri Birleştir] ◄──────┘
                        ↓
              [Claude — Karşılaştırmalı Rapor]
                        ↓
              (opsiyonel: Gmail/Slack/Telegram)
```

---

## Kaynaklar
- n8n Docs: https://docs.n8n.io/
- Claude API: https://docs.anthropic.com/
- MCP kurulumu (Claude Code tarafı): [`MCP-KURULUM.md`](MCP-KURULUM.md)
