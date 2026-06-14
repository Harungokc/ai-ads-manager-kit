# Platform API Detayları

## Meta Ads API

### Endpoint'ler
- Base: `https://graph.facebook.com/v19.0`
- Ads Manager: `/act_{account_id}/ads`
- Campaigns: `/act_{account_id}/campaigns`
- Insights: `/{ad_id}/insights`

### Temel İşlemler
```python
# Kampanya listesi
GET /act_{ad_account_id}/campaigns?fields=name,status,objective

# Kampanya oluşturma
POST /act_{ad_account_id}/campaigns

# Reklam seti oluşturma
POST /act_{ad_account_id}/adsets

# Reklam oluşturma
POST /act_{ad_account_id}/ads
```

### Rate Limits
- Normal: 200 request/saniye
- Creative: 50 request/saniye
- Insights: 200 request/saniye

## Google Ads API

### Endpoint
- OAuth2: `https://oauth2.googleapis.com/token`
- API: `https://googleads.googleapis.com/v18`

### Temel İşlemler
```python
# Kampanya listesi
GET /customers/{customer_id}/campaigns

# Kampanya oluşturma
MUTATE /customers/{customer_id}/campaigns
```

## Learning Phase Takibi

Meta Ads'te kampanyalar "Learning Phase" sürecinden geçer:

| Gün | Beklenti |
|-----|----------|
| 1-7 | İlk optimizasyonlar, yüksek maliyet |
| 8-14 | Performans stabilizasyonu |
| 15+ | Learning Phase tamamlanmış olmalı |

**Önemli:** Learning Phase'teyken büyük değişiklik yapma — her değişiklik learning phase'i sıfırlar.

## Breakdown Effect

Reklam performansında "breakdown" (kırılım) analizi:

```
Demographics: Yaş + Cinsiyet kırılımı
Placement: Instagram / Facebook / Audience Network
Device: Mobile / Desktop
Geography: Şehir bazlı
```

meta-ads-analyzer skill'ı breakdown effect'i otomatik hesaplar.

## Conversion Tracking

### Meta Pixel
```javascript
fbq('track', 'Purchase', {
  value: 99.90,
  currency: 'TRY'
});
```

### Google Ads Conversion Tag
```javascript
gtag('report', 'conversion', {
  send_to: 'AW-XXXXXXXXX/...'
});
```
