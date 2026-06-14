# Troubleshooting

## Meta Ads Hataları

### "Invalid access token"
- Token süresi dolmuş olabilir → Meta Business > Settings > Tokens
- Token'ın `ads_read` ve `ads_management` permission'ları var mı kontrol et

### "Ad account not found"
- `act_` prefix'ini ekle: `act_123456789`
- Business Account ID değil, Ad Account ID kullan

### "Rate limit exceeded"
- Meta: 200 req/s limit
- 1-2 saniye bekle, tekrar dene
- Batch API kullan (tek seferde 25 işlem)

## Google Ads Hataları

### "Developer token not approved"
- Basic access: 15 gün içinde onaylanır
- Standard access: 2-5 iş günü + mülakat

### "OAuth token expired"
- Refresh token kullan
- `google-ads.ini`'deki `refresh_token`ı yenile

## MCP Server Hataları

### "MCP server not found"
```bash
# Server'ı yeniden ekle
claude /mcp add meta-ads -- npx -y @pipeboard-co/meta-ads-mcp
```

### "Connection timeout"
- Internet bağlantısını kontrol et
- Firewall port'larını aç (MCP default: 3100)

## n8n Workflow Hataları

### "Credential not found"
- n8n → Settings → Credentials
- Yeni credential oluştur
- Workflow'da credential'ı yeniden seç

### "Node not found"
- n8n sürümünü kontrol et (1.0+ gerekli)
- MCP server'ın çalışıyor olduğundan emin ol
