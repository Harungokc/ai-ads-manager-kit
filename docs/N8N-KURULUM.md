# n8n Kurulum Rehberi

## n8n Nedir?

n8n — "n8n" telaffuz edilir — açık kaynak workflow otomasyon platformu. Benzer: Zapier, Make.com ama self-hosted ve ücretsız.

## Kurulum

### Docker ile (Önerilen)
```bash
docker run -d \
  --name n8n \
  -p 5678:5678 \
  -v n8n_data:/home/node/.n8n \
  n8nio/n8n
```

### npm ile
```bash
npm install -g n8n
n8n start
```

## MCP Server'ı n8n'de Kullanma

### 1. n8n-MCP Server Kurulumu
```bash
npm install -g n8n-mcp-server
```

### 2. n8n'de MCP Tool Ekleme
1. n8n → Settings → MCP Servers
2. "Add Server" tıkla
3. Server name: `meta-ads-mcp`
4. Server command: `npx -y @pipeboard-co/meta-ads-mcp`
5. Environment variables ekle
6. Save

### 3. Workflow'da Kullanma
1. yeni workflow oluştur
2. "MCP" node ekle
3. Tool seç: `create_campaign`, `get_insights`, vb.
4. Credential'ı bağla
5. Test et

## Workflow Import

`workflows/` klasöründeki JSON dosyalarını import et:

1. n8n → Workflows → Import from JSON
2. Dosyayı seç veya yapıştır
3. Credential'ları ayarla
4. Activate

## Örnek Workflow: Otomatik Rapor

```
[Schedule: Her Pazartesi 09:00]
    ↓
[Meta Ads: Son 7 gün verisi çek]
    ↓
[Google Ads: Son 7 gün verisi çek]
    ↓
[Claude: Verileri yorumla]
    ↓
[Email: Raporu gönder]
```

## Kaynaklar

- n8n Docs: https://docs.n8n.io/
- n8n Community Nodes: https://www.n8n.io/integrations/
- Meta Marketing API: https://developers.facebook.com/docs/marketing-apis
