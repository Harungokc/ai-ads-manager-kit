# Kurulum Rehberi — Sıfırdan AI Ads Manager Kit

Bu rehber, hiçbir şey kurulu olmadan başlayıp tam çalışır hale getirmeniz içindir.

---

## 🗺️ Genel Bakış — Neler Kurulacak?

```
Adım 1: Python + Node.js kurulumu
Adım 2: Claude Code kurulumu
Adım 3: Meta Business API kurulumu
Adım 4: Google Ads API kurulumu
Adım 5: n8n kurulumu
Adım 6: MCP Server kurulumu
Adım 7: AI Ads Manager Kit kurulumu
Adım 8: İlk kampanyanı oluştur
```

---

## Adım 1: Python ve Node.js Kurulumu

### Python (3.10+)
```bash
# Windows: python.org'dan indir
# Mac: brew install python3
# Linux: sudo apt install python3 python3-pip

python --version
# → Python 3.10+ görüyorsan tamam
```

### Node.js (18+)
```bash
# Windows: nodejs.org'dan LTS indir
# Mac: brew install node
# Linux: curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -

node --version
# → v18.x.x görüyorsan tamam
```

### pip ve virtualenv
```bash
pip install --upgrade pip
pip install virtualenv

# Proje için sanal ortam oluştur
python -m venv venv

# Windows:
venv\Scripts\activate

# Mac/Linux:
source venv/bin/activate

# Artık (venv) ön eki görünmeli
```

---

## Adım 2: Claude Code Kurulumu

### Kurulum
```bash
# Mac/Linux:
brew install anthropic/formulae/claude-code

# Windows:
# https://docs.anthropic.com/en/docs/claude-code/setup adresinden indir

claude --version
```

### Claude Code İlk Ayarlar
```bash
# İlk çalıştırmada oturum açma isteyecek
claude

# MCP server'ları aktif et
# Claude Code'da Ctrl/Cmd + , → MCP sekmesi
```

### Alternatif: Cursor veya Windsurf
Bu kit Claude Code, Cursor ve Windsurf ile çalışır:
- **Cursor**: cursor.com → Download
- **Windsurf**: codeium.com/windsurf → Download

---

## Adım 3: Meta Business API Kurulumu

### 3.1: Meta for Developers'a Kaydol
1. [developers.facebook.com](https://developers.facebook.com/) adresine git
2. "Get Started" → Facebook hesabınla giriş yap
3. Hesabı onayla (telefon numarası + kredi kartı gerekebilir)

### 3.2: Uygulama Oluştur
1. [developers.facebook.com/apps](https://developers.facebook.com/apps) → "Create App"
2. App Type: **Business** seç
3. App name: `AI Ads Manager` (veya istediğin isim)
4. App ID ve App Secret'ı kopyala (ileride lazım olacak)

### 3.3: Ürün Ekle
App Dashboard'da:

1. **Meta Business API** ekle
   - sol menü → Products → add product
   - "Marketing API" → Configure

2. **WhatsApp Business API** (opsiyonel — WhatsApp bot için)
   - WhatsApp → Configure
   - Phone Number ekle

### 3.4: Access Token Al
1. [Meta Business Suite](https://business.facebook.com/) → Business Settings
2. System User oluştur → "Marketing API" permission'ları ver
3. Assets → Ad Accounts → erişim ver
4. System User Token → Generate Token
5. **Token'ı kopyala** (çok uzun string)

### 3.5: Ad Account ID Bul
1. [business.facebook.com](https://business.facebook.com/) → Business Settings
2. Accounts → Ad Accounts
3. Ad Account ID: `act_XXXXXXXXX` formatında (act_ sonra rakamlar)

### Token Test Et
```bash
curl -X GET "https://graph.facebook.com/v19.0/me?access_token=TOKENIN_BURAYA" \
  | python -m json.tool
# {"id": "XXXXXXXX", "name": "..."} görüyorsan başarılı
```

---

## Adım 4: Google Ads API Kurulumu

### 4.1: Google Cloud Console'da Proje Oluştur
1. [console.cloud.google.com](https://console.cloud.google.com/) → New Project
2. Project name: `ai-ads-manager`
3. Project ID: `ai-ads-manager-xxxxx` (benzersiz olmalı)

### 4.2: Google Ads API Enable Et
1. APIs & Services → Library
2. "Google Ads API" ara → Enable

### 4.3: OAuth2 Credential Oluştur
1. APIs & Services → Credentials
2. Create Credentials → OAuth client ID
3. Application type: Desktop app
4. Client ID ve Client Secret'ı indir/kopyala

### 4.4: Developer Token Al
1. [ads.google.com](https://ads.google.com/) → Sign in
2. Tools → Settings → API Center
3. Developer Token başvurusu yap
4. **Basic Access**: 2-15 gün içinde onaylanır (test için yeterli)
5. **Standard Access**: 2-5 iş günü + mülakat (production için)

### 4.5: MCC (My Client Center) Hesabı
Üst düzey erişim için MCC hesabı aç:
- ads.google.com → Tools → Manager Accounts → Create
- MCC ID: `xxx-xxx-xxxx` formatında

---

## Adım 5: n8n Kurulumu

### Seçenek A: Docker ile (Önerilen)
```bash
# Docker kurulu değilse indir: docker.com

docker volume create n8n_data

docker run -d \
  --name n8n \
  -p 5678:5678 \
  -v n8n_data:/home/node/.n8n \
  -e N8N_SECURE_COOKIE=false \
  n8nio/n8n

# Tarayıcıda aç: http://localhost:5678
```

### Seçenek B: npm ile
```bash
npm install -g n8n
n8n start

# Tarayıcıda aç: http://localhost:5678
```

### Seçenek C: Cloud (Kolay)
1. [n8n.io](https://n8n.io) → Start free
2. Cloud plan seç (ücretsiz plan mevcut)
3. Web arayüzünde çalış

### n8n İlk Ayarlar
1. Açılışta hesap oluştur
2. Credentials → Yeni ekle
3. Meta Ads ve Google Ads credential'larını kaydet

---

## Adım 6: MCP Server Kurulumu

> ⚠️ **Önemli:** Bu kitin kullandığı MCP server'lar **hosted servislerdir** (npm `npx`
> paketi DEĞİL). Aşağıdaki komutlar bu gerçeğe göre yazılmıştır. Ayrıntılı sürüm ve
> alternatifler (self-host) için: [`MCP-KURULUM.md`](MCP-KURULUM.md).

### 6.1: Claude Code'da MCP Ekle
```bash
# Meta Ads (pipeboard, hosted remote MCP):
claude mcp add --transport http meta-ads https://meta-ads.mcp.pipeboard.co/

# TikTok + LinkedIn (+Google+Meta) — adspirer (hosted, OAuth, token gerekmez):
claude mcp add --transport http adspirer https://mcp.adspirer.com/mcp

# Google + Meta + GA4 (Ryze AI, hosted SSE) — endpoint'i kaynaktan al:
#   https://www.get-ryze.ai/  →  $GA_MCP_ENDPOINT_URL
claude mcp add --transport sse google-meta-ads-ga4 "$GA_MCP_ENDPOINT_URL"
```

### 6.2: Bağlandı mı Kontrol Et
```bash
claude mcp list          # bağlı server'ları gösterir
claude                    # oturum içinde /mcp ile araçları gör
> "Meta Ads'te kampanya listemi göster"
```

### 6.3: Hazır Config Dosyaları
Repodaki [`mcp/`](../mcp/) klasöründe hazır config'ler var (URL formunda):
`meta-ads-mcp.json`, `adspirer-mcp.json`, `google-ads-mcp.json`. İstersen bunları
`~/.claude/settings/mcp.json`'a kopyalayabilirsin.

### 6.4: Self-host (İleri Seviye)
Hosted yerine kendi sunucunda çalıştırmak istersen (TikTok için AdsMCP, LinkedIn için
danielpopamd, Meta için kaynaktan), adım adım: [`MCP-KURULUM.md`](MCP-KURULUM.md).

---

## Adım 7: AI Ads Manager Kit Kurulumu

### 7.1: Repoyu İndir
```bash
git clone https://github.com/Harungokc/ai-ads-manager-kit.git
cd ai-ads-manager-kit
```

### 7.2: Sanal Ortam ve Bağımlılıklar
```bash
# Sanal ortam oluştur
python -m venv venv

# Aktifleştir
# Windows:
venv\Scripts\activate
# Mac/Linux:
source venv/bin/activate

# Bağımlılıkları yükle
pip install -r requirements.txt
```

### 7.3: .env Dosyasını Oluştur
```bash
cp .env.example .env
```

`.env` dosyasını düzenle — her platform için token'ları yapıştır:

```bash
# Meta Ads
META_ACCESS_TOKEN=EAAAFxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
META_AD_ACCOUNT_ID=act_123456789
META_APP_ID=1234567890
META_APP_SECRET=xxxxxxxxxxxxxxxxxxxxxxxx

# Google Ads
GOOGLE_ADS_DEVELOPER_TOKEN=xxxxxxxxxxxxxxxxxxx
GOOGLE_ADS_CLIENT_ID=xxx.apps.googleusercontent.com
GOOGLE_ADS_CLIENT_SECRET=xxxxxxxxxxxxxxx
GOOGLE_ADS_REFRESH_TOKEN=1//xxxxxxxxxxxxxxx
GOOGLE_ADS_CUSTOMER_ID=1234567890

# GA4
GA4_PROPERTY_ID=123456789
```

### 7.4: Google Ads OAuth2 Refresh Token Al
Google Ads API için refresh token gerekir. Şu adımlarla al:

```python
# Python ile:
from google.oauth2.credentials import Credentials
from google_auth_oauthlib.flow import InstalledAppFlow

SCOPES = ['https://www.googleapis.com/auth/adwords.read']

flow = InstalledAppFlow.from_client_secrets_file(
    'path/to/client_secret.json', SCOPES)
credentials = flow.run_local_server(port=0)
print(credentials.token)  # Refresh token'ı kopyala
```

### 7.5: GA4 Service Account Kurulumu
GA4 için service account gerekir:

1. Google Cloud Console → IAM → Service Accounts
2. "+ Create Service Account"
3. Name: `ga4-reader`
4. Role: **Viewer**
5. Keys → JSON oluştur → indir
6. JSON dosyasını projeye koy: `keys/ga4-service-account.json`

---

## Adım 8: İlk Kampanyayı Oluştur

### Claude Code ile Meta Ads
```bash
claude
```

Claude Code açılınca şunu yaz:
```
Meta Ads'te yeni bir kampanya oluştur:
- Kampanya adı: "Test Kampanyası"
- Hedef: conversions
- Bütçe: günlük 50 TL
- Hedef kitle: Türkiye, kadın, 25-40 yaş
- Reklam formatı: single image
```

### Claude Code ile Google Ads
```
Google Ads'te yeni search kampanyası oluştur:
- Kampanya adı: "Test Search"
- Keyword: "online eğitim"
- Bütçe: günlük 100 TL
- Hedef: conversions
```

### n8n ile Otomatik Kampanya
1. n8n'i aç: [http://localhost:5678](http://localhost:5678)
2. `workflows/1-meta-kampanya-olustur.json` import et
3. Credential'ları bağla (Meta token, account ID)
4. "Test" butonuna tıkla
5. Çalışıyorsa "Activate" et

---

## ✅ Kurulum Testi — Her Şey Çalışıyor mu?

Bu komutlarla test et:

```bash
# Python import test
python -c "
import meta_ads
import google_ads
print('✅ Python packages: OK')
"

# Meta API test
python -c "
import requests
token = 'TOKENIN'
acc_id = 'act_XXXXXXXX'
url = f'https://graph.facebook.com/v19.0/{acc_id}/campaigns?limit=1'
r = requests.get(url, params={'access_token': token})
print('✅ Meta API:', 'data' in r.json())
"

# Claude Code MCP test
# Claude Code'da şunu sor:
# > "MCP server'larıma bağlı mısın? Meta Ads kampanyalarımı listele"
```

---

## 🆘 Sorun Oldu mu?

### "Token geçersiz" hatası
- Meta: [business.facebook.com](https://business.facebook.com/) → System User Token yenile
- Google: OAuth2 refresh token süresi dolmuş → yeniden al

### "MCP server bulunamadı" hatası
```bash
# Yeniden ekle (hosted MCP — npx değil)
claude mcp add --transport http meta-ads https://meta-ads.mcp.pipeboard.co/
claude mcp list   # bağlı mı kontrol et
```

### "Rate limit" hatası
- Meta: 5 dakika bekle, tekrar dene
- Google: Günlük limit aşılmış → ertesi gün tekrar dene

### "Permission denied" hatası
- Meta: Uygulamaya `ads_read`, `ads_management` permission'ları ekle
- Google: Service account'a GA4 Viewer rolü ver

**Tüm sorunlar için:** [TROUBLESHOOTING.md](TROUBLESHOOTING.md) dosyasına bak.

---

## 📞 Destek

- GitHub Issues: [github.com/Harungokc/ai-ads-manager-kit/issues](https://github.com/Harungokc/ai-ads-manager-kit/issues)
- Meta Marketing API Docs: [developers.facebook.com/docs/marketing-apis](https://developers.facebook.com/docs/marketing-apis)
- Google Ads API Docs: [developers.google.com/google-ads/api/docs](https://developers.google.com/google-ads/api/docs)
- n8n Docs: [docs.n8n.io](https://docs.n8n.io)
