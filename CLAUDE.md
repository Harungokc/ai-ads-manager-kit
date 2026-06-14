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
# ~/.claude/settings/mcp.json dosyasına ekle:
```

## MCP Server Config'leri

### Meta Ads MCP
```json
{
  "mcpServers": {
    "meta-ads-mcp": {
      "command": "npx",
      "args": ["-y", "@pipeboard-co/meta-ads-mcp"]
    }
  }
}
```

### Google + Meta + GA4 MCP
```json
{
  "mcpServers": {
    "google-meta-ads-ga4-mcp": {
      "command": "npx",
      "args": ["-y", "@irinabuht12-oss/google-meta-ads-ga4-mcp"]
    }
  }
}
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
