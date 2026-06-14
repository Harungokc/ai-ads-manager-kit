# 🚀 AI Ads Manager Kit

> Claude Code, n8n ve MCP ile Google Ads, Meta Ads ve daha fazlasını doğal dille yönet —
> alandaki en iyi MCP server'larını **tek konfigürasyonla** bir araya getirir, **600+ araca erişim** sağlar.

[![Stars](https://img.shields.io/github/stars/Harungokc/ai-ads-manager-kit?style=flat)](https://github.com/Harungokc/ai-ads-manager-kit)
[![MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

## 🧩 Bu Repo Ne? (Nasıl Çalışır)

Bu bir **orkestrasyon / birleştirme katmanı** — reklam araçlarını kendisi içermez.
Bunun yerine alandaki en güçlü açık kaynak/hosted **MCP server'larını** Claude Code'a
bağlar; 600+ araç bu upstream server'lardan gelir (hepsi [aşağıda](#-kaynak-repolar)
kredilenmiştir). Repo'nun kattığı değer:

- ✅ **Hazır MCP config'leri** — server'ları tek dosyayla bağla ([`mcp/`](mcp/), [`docs/MCP-KURULUM.md`](docs/MCP-KURULUM.md))
- ✅ **Claude Code skill'leri & prompt'ları** — Meta/Google için hazır uzman davranışı ([`skills/`](skills/), [`prompts/`](prompts/))
- ✅ **n8n workflow'ları** — kampanya oluşturma, optimizasyon, çok-platform rapor (import-edilebilir, [`workflows/`](workflows/))
- ✅ **Türkçe, sıfırdan dokümantasyon** — kurulum, learning phase, troubleshooting ([`docs/`](docs/))

## ⚡ Hızlı Başlangıç

### 1. Kurulum (5 dakika)

```bash
# Claude Code'da Meta Ads MCP'yi (pipeboard, hosted) ekle:
claude mcp add --transport http meta-ads https://meta-ads.mcp.pipeboard.co/

# Bağlandı mı kontrol et:
claude mcp list

# Detaylı MCP kurulumu (Google/GA4 dahil) → docs/MCP-KURULUM.md
# n8n workflow'larını import et → workflows/ (bkz. docs/N8N-KURULUM.md)
```
> ⚠️ Bu MCP server'lar **hosted servislerdir** (npm `npx` paketi değil). Endpoint ve
> token'lar için: [`docs/MCP-KURULUM.md`](docs/MCP-KURULUM.md).

### 2. Platform Bağlantıları

| Platform | Token / API | Ortam Değişkeni |
|----------|------------|----------------|
| Meta Ads | Meta Business Token | `META_ACCESS_TOKEN` |
| Google Ads | Google OAuth2 / Developer Token | `GOOGLE_ADS_DEVELOPER_TOKEN` |
| TikTok Ads | TikTok Access Token | `TIKTOK_ACCESS_TOKEN` |
| LinkedIn Ads | LinkedIn OAuth2 | `LINKEDIN_ACCESS_TOKEN` |
| GA4 | Google Analytics | `GA4_PROPERTY_ID` |

**.env dosyası oluştur:**
```bash
cp .env.example .env
# .env dosyasını doldur
```

### 3. Claude Code'da Kullanım

```bash
# Meta kampanyası oluştur
claude "Instagram'da yeni ürünüm için kampanya başlat, bütçe günlük 50$, hedef kitle kadın 25-40"

# Google Ads optimize et
claude "Google Ads kampanyamın son 7 günlük performansını analiz et, öner"

# Learning Phase teşhisi
claude "Kampanya 'Summer Sale' learning phase'ta ne durumda?"
```

---

## 📊 Özellik Karşılaştırması — Best-of 11 Repo

> Aşağıdaki tablolar, bu kitin **hangi upstream projeleri birleştirdiğini** ve her
> birinin neyi iyi yaptığını gösterir. Tikler bu kitin değil, kaynak projelerin
> özellikleridir; kit bunları tek noktadan erişilebilir kılar.

| Özellik | NotFair | claude-ads | google-meta-ads-ga4-mcp | meta-ads-mcp | meta-ads-analyzer |
|---------|---------|------------|-------------------------|---------------|-------------------|
| **Yıldız** | 2849⭐ | 6021⭐ | 1009⭐ | 987⭐ | 364⭐ |
| **Google Ads** | ✅ | ✅ | ✅ | ❌ | ❌ |
| **Meta Ads** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **TikTok Ads** | ❌ | ✅ | ❌ | ❌ | ❌ |
| **LinkedIn Ads** | ❌ | ✅ | ❌ | ❌ | ❌ |
| **YouTube Ads** | ❌ | ✅ | ❌ | ❌ | ❌ |
| **Apple Ads** | ❌ | ✅ | ❌ | ❌ | ❌ |
| **GA4 Entegrasyonu** | ❌ | ✅ | ✅ | ❌ | ❌ |
| **Kampanya Oluşturma** | ✅ | ✅ | ✅ | ✅ | ❌ |
| **Performans Analizi** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Learning Phase** | ❌ | ❌ | ❌ | ❌ | ✅ |
| **Breakdown Effect** | ❌ | ❌ | ❌ | ❌ | ✅ |
| **MCP Server** | ✅ | ❌ | ✅ | ✅ | ✅ |
| **Claude Code Skill** | ✅ | ✅ | ❌ | ❌ | ✅ |
| **n8n Entegrasyonu** | ✅ | ❌ | ✅ | ❌ | ❌ |
| **A/B Test Otomasyonu** | ❌ | ✅ | ✅ | ❌ | ❌ |
| **Budget Optimizasyonu** | ✅ | ✅ | ✅ | ❌ | ❌ |
| **Creative Generation** | ❌ | ✅ | ❌ | ❌ | ❌ |
| **PDF Rapor** | ❌ | ✅ | ❌ | ❌ | ❌ |
| **Parallel Agents** | ❌ | ✅ | ❌ | ❌ | ❌ |

---

## 🧰 Araç Sayısı (Upstream MCP'lerden Erişilen)

> Bu sayılar bağlanan **upstream MCP server'larından** gelir — bu repo araç yazmaz,
> erişimi birleştirir. Aşağıdaki ✅'ler hangi platform için hangi kaynakta araç
> bulunduğunu gösterir.

| Platform | claude-ads | google-meta-ads-ga4-mcp | markifact-mcp | ads-mcp | meta-ads-mcp |
|----------|-----------|-------------------------|---------------|---------|--------------|
| **Meta Ads** | ✅ | ✅ | ✅ | ✅ | ✅ (135 araç) |
| **Google Ads** | ✅ | ✅ | ✅ | ✅ | ❌ |
| **TikTok Ads** | ✅ | ❌ | ✅ | ✅ | ❌ |
| **LinkedIn Ads** | ✅ | ❌ | ✅ | ✅ | ❌ |
| **YouTube Ads** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **Apple Ads** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **GA4** | ✅ | ✅ | ✅ | ❌ | ❌ |
| **Microsoft Ads** | ✅ | ❌ | ❌ | ❌ | ❌ |

**Toplam: 600+ araca erişim** (bağlanan upstream MCP server'ları üzerinden)

---

## 📁 Repoda Ne Var?

```
ai-ads-manager-kit/
├── workflows/          # n8n JSON workflow'ları (import et → çalıştır)
│   ├── 1-meta-kampanya-olustur.json
│   ├── 2-google-ads-optimize.json
│   └── 3-cross-platform-report.json
├── skills/             # Claude Code skill dosyaları
│   ├── meta-ads-skill.md
│   └── meta-ads-analyzer-skill.md
├── mcp/                # MCP server config'leri
│   ├── meta-ads-mcp.json
│   └── google-ads-mcp.json
├── prompts/            # Claude system prompt'ları
│   ├── meta-ads-prompt.md
│   └── google-ads-prompt.md
├── docs/               # Detaylı dokümantasyon
│   ├── KURULUM.md
│   ├── MCP-KURULUM.md
│   ├── N8N-KURULUM.md
│   ├── PLATFORM-API.md
│   ├── TROUBLESHOOTING.md
│   └── LEARNING-PHASE-GUIDE.md
├── .env.example
├── requirements.txt
├── CLAUDE.md           # AI ajanlar için kurulum rehberi
├── CONTRIBUTING.md     # Katkı & geliştirme rehberi
└── LICENSE
```

> **📍 Mevcut durum:** Hazır ve test edilebilir entegrasyonlar **Meta Ads** ve
> **Google Ads / GA4**'tür (MCP config + skill + prompt + workflow). TikTok, LinkedIn,
> YouTube ve Apple Ads **yol haritasındadır** — karşılaştırma tablolarında bu platformlar
> için araç barındıran upstream projeler işaretlidir; kit'e entegrasyonları sırada.
> Katkı için: [`CONTRIBUTING.md`](CONTRIBUTING.md).

---

## 🔥 Her Reponun En İyi Yanı

### 1. NotFair (2849⭐) — `nowork-studio/NotFair`
**En iyi yanı:** Claude Code'a direkt entegre, kampanya oluşturma/durdurma/optimize komutları, SEO + GEO bir arada
> **Alınan:** Claude Code skill yapısı, kampanya yönetim komutları

### 2. claude-ads (6021⭐) — `AgriciDaniel/claude-ads`
**En iyi yanı:** 250+ kontrollü audit, parallel agents, YouTube/LinkedIn/TikTok/Apple geniş platform desteği, PDF rapor
> **Alınan:** Audit framework, parallel agent mimarisi, cross-platform genişletme

### 3. google-meta-ads-ga4-mcp (1009⭐) — `irinabuht12-oss/google-meta-ads-ga4-mcp`
**En iyi yanı:** 250+ MCP tool, n8n/Cursor/Windsurf uyumu, GA4 entegrasyonu
> **Alınan:** n8n workflow'ları, GA4 entegrasyonu, MCP server config'leri

### 4. meta-ads-mcp (987⭐) — `pipeboard-co/meta-ads-mcp`
**En iyi yanı:** Meta Marketing API v25.0 ile 135 araç, Docker desteği
> **Alınan:** Meta Marketing API detayları, Docker setup, Python tabanlı MCP implementasyonu

### 5. meta-ads-analyzer (364⭐) — `mathiaschu/meta-ads-analyzer`
**En iyi yanı:** Learning Phase analizi, Breakdown Effect diagnosis
> **Alınan:** Learning Phase skill'ı, Breakdown Effect analizi

### 6. markifact-mcp (40⭐) — `markifact/markifact-mcp`
**En iyi yanı:** 300+ araç, 4 platform, human-in-the-loop güvenlik katmanı
> **Alınan:** Human-in-the-loop pattern

### 7. ads-mcp (56⭐) — `amekala/ads-mcp`
**En iyi yanı:** Gemini CLI desteği
> **Alınan:** Gemini CLI entegrasyonu

### 8. konquest-meta-ads-mcp (31⭐) — `brandu-mos/konquest-meta-ads-mcp`
**En iyi yanı:** 57-tool supervised MCP, safety gates
> **Alınan:** Safety gates pattern'ı

### 9. advertising-hub (19⭐) — `itallstartedwithaidea/advertising-hub`
**En iyi yanı:** 14 platform, 25+ AI agent
> **Alınan:** Platform genişletme listesi

---

## 💡 Örnek Kullanım Senaryoları

### Senaryo 1: Yeni Ürün Lansmanı
```
claude "Instagram ve Google'da yeni ürünüm için kampanya başlat"
→ Meta: Conversion kampanyası, otomatik DM
→ Google: Search + Display, keyword araştırması
→ Analitik: GA4 event tracking kur
```

### Senaryo 2: Kampanya Teşhisi
```
claude "Kampanyam 'Delivery' learning phase'ta takıldı, ne yapmalıyım?"
→ meta-ads-analyzer: Learning Phase diagnosis
→ Öneri: Budget artışı, audience genişletme, creative refresh
```

### Senaryo 3: Haftalık Rapor Otomasyonu (n8n)
```
Her Pazartesi 09:00
→ Tüm platformlardan son 7 gün verisi çek
→ Claude ile yorumla
→ Telegram'a rapor gönder
```

---

## 🔗 Kaynak Repolar

| Repo | ⭐ | En İyi Yanı |
|------|---|-------------|
| [AgriciDaniel/claude-ads](https://github.com/AgriciDaniel/claude-ads) | 6021 | 250+ audit, parallel agents, PDF rapor |
| [nowork-studio/NotFair](https://github.com/nowork-studio/NotFair) | 2849 | Claude Code direkt, SEO+SEM+GEO |
| [irinabuht12-oss/google-meta-ads-ga4-mcp](https://github.com/irinabuht12-oss/google-meta-ads-ga4-mcp) | 1009 | 250+ MCP tools, n8n entegrasyonu |
| [pipeboard-co/meta-ads-mcp](https://github.com/pipeboard-co/meta-ads-mcp) | 987 | 135 araç, Docker, Cursor uyumlu |
| [mathiaschu/meta-ads-analyzer](https://github.com/mathiaschu/meta-ads-analyzer) | 364 | Learning Phase, Breakdown Effect |
| [markifact/markifact-mcp](https://github.com/markifact/markifact-mcp) | 40 | 4 platform, human-in-the-loop |
| [amekala/ads-mcp](https://github.com/amekala/ads-mcp) | 56 | Gemini CLI, multi-platform |
| [brandu-mos/konquest-meta-ads-mcp](https://github.com/brandu-mos/konquest-meta-ads-mcp) | 31 | Safety gates, diagnostic araçlar |
| [itallstartedwithaidea/advertising-hub](https://github.com/itallstartedwithaidea/advertising-hub) | 19 | 14 platform hub |

---

## 🤝 Katkıda Bulunma

```bash
git clone https://github.com/Harungokc/ai-ads-manager-kit.git
cd ai-ads-manager-kit
# Değişiklik yap → PR aç
```

---

## 📜 Lisans

MIT — Ticari kullanım serbest.
