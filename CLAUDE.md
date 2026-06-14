# AI Ads Manager Kit — AI Ajanlar İçin Kurulum Rehberi

Bu proje Claude Code, Cursor, Windsurf ve diğer AI ajanları ile çalışır.

## Hızlı Kurulum

```bash
# 1. Bu repoyu klonla
git clone https://github.com/Harungokc/ai-ads-manager-kit.git
cd ai-ads-manager-kit

# 2. Bağımlılıkları yükle
pip install -r requirements.txt

# 3. .env dosyasını oluştur
cp .env.example .env
# .env dosyasını kendi API anahtarlarınla doldur

# 4. Claude Code MCP ayarları
# `claude mcp add` komutuyla ekle (aşağıdaki örnekler) veya proje kökünde .mcp.json kullan.
# Ayrıntı: docs/MCP-KURULUM.md
```

## MCP Server Config'leri

> Bu MCP server'lar **hosted servislerdir** (npx paketi değil). URL formunda eklenir.
> Ayrıntı: [`docs/MCP-KURULUM.md`](docs/MCP-KURULUM.md).

### Meta Ads MCP (pipeboard, hosted)
```bash
claude mcp add --transport http meta-ads https://meta-ads.mcp.pipeboard.co/
```

### TikTok + LinkedIn (+Google+Meta) — adspirer (hosted, OAuth)
```bash
claude mcp add --transport http adspirer https://mcp.adspirer.com/mcp
```

### Google + Meta + GA4 MCP (Ryze AI, hosted SSE)
```bash
# Endpoint'i https://www.get-ryze.ai/ üzerinden al → GA_MCP_ENDPOINT_URL
claude mcp add --transport sse google-meta-ads-ga4 "$GA_MCP_ENDPOINT_URL"
```

## Platform API Anahtarları

### Meta Business API
1. [Meta Developers](https://developers.facebook.com/) → Uygulama oluştur
2. `ads_read`, `ads_management` permissions ekle
3. Business Token al → `.env`'e `META_ACCESS_TOKEN` olarak kaydet

### Google Ads API
1. Google Cloud Console → Google Ads API enable et
2. Developer Token al (approval 2-5 iş günü)
3. OAuth2 credentials oluştur
4. `.env`'e `GOOGLE_ADS_DEVELOPER_TOKEN`, `GOOGLE_ADS_CLIENT_ID`, `GOOGLE_ADS_CLIENT_SECRET` olarak kaydet

## AI Ajan Komut Örnekleri

```
# Kampanya oluştur
> "Meta Ads'te yeni retargeting kampanyası başlat"

# Performans analizi
> "Google Ads son 30 gün analiz et, öneriler ver"

# Learning Phase teşhisi
> "Kampanya 'Summer Sale' learning phase'ta ne durumda?"

# Cross-platform rapor
> "Tüm platformların haftalık performansını karşılaştır"
```
