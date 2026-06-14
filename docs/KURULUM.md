# Kurulum Rehberi

## Gereksinimler

- Python 3.10+
- Node.js 18+ (MCP server için)
- Claude Code / Cursor / Windsurf (opsiyonel)
- n8n (workflow otomasyonu için)

## Adım 1: Repoyu İndir

```bash
git clone https://github.com/Harungokc/ai-ads-manager-kit.git
cd ai-ads-manager-kit
```

## Adım 2: Python Bağımlılıkları

```bash
pip install -r requirements.txt
```

## Adım 3: API Anahtarları

`.env.example` dosyasını `.env` olarak kopyala ve doldur:

```bash
cp .env.example .env
```

Gerekli değişkenler:
- `META_ACCESS_TOKEN` — Meta Business API token
- `META_AD_ACCOUNT_ID` — Meta Ads Account ID (act_xxxxxx)
- `GOOGLE_ADS_DEVELOPER_TOKEN` — Google Ads Developer Token
- `GOOGLE_ADS_CLIENT_ID` — Google OAuth2 Client ID
- `GOOGLE_ADS_CLIENT_SECRET` — Google OAuth2 Client Secret
- `GA4_PROPERTY_ID` — GA4 Property ID (123456789)
- `TIKTOK_ACCESS_TOKEN` — TikTok Access Token
- `LINKEDIN_ACCESS_TOKEN` — LinkedIn Access Token

## Adım 4: MCP Server Kurulumu

### Meta Ads MCP
```bash
npx -y @pipeboard-co/meta-ads-mcp
```

### Google + Meta + GA4 MCP
```bash
npx -y @irinabuht12-oss/google-meta-ads-ga4-mcp
```

## Adım 5: n8n Workflow Import

1. n8n'i aç (https://n8n.io veya local)
2. `workflows/` klasöründeki JSON dosyalarını import et
3. Credential'ları ayarla
4. Aktive et

## Platform Bazlı Detaylar

### Meta Business API Kurulumu
1. [Meta for Developers](https://developers.facebook.com/)
2. Yeni uygulama oluştur → "Business" tipi
3. WhatsApp, Instagram Graph API veya Marketing API ekle
4. Access Token al

### Google Ads API Kurulumu
1. [Google Cloud Console](https://console.cloud.google.com/)
2. Google Ads API enable et
3. Developer Token başvurusu yap
4. MCC hesabı önerilir

## Test

```bash
python -c "from meta_ads import MetaAdsClient; print('Meta Ads: OK')"
python -c "from google_ads import GoogleAdsClient; print('Google Ads: OK')"
```
