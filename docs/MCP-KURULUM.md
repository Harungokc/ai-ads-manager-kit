# 🔌 MCP Kurulum Rehberi

Bu kit, reklam araçlarını **kendisi içermez** — bunun yerine alandaki en güçlü açık
kaynak/hosted MCP server'larını Claude Code'a bağlar (orkestrasyon katmanı). Araçlar
(600+) bu upstream MCP server'lardan gelir. Bu dosya, onları doğru şekilde nasıl
bağlayacağını anlatır.

> ⚠️ **Önemli:** Bu MCP server'lar **hosted servislerdir** (npm paketi olarak `npx` ile
> kurulmazlar). Aşağıdaki yöntemler her server'ın resmî dokümanına dayanır. Endpoint
> URL'leri ve token'lar zamanla değişebilir — kaynak repoları kontrol et.

---

## 1. Meta Ads MCP (pipeboard)

**Kaynak:** [pipeboard-co/meta-ads-mcp](https://github.com/pipeboard-co/meta-ads-mcp) · 135 araç

Hosted remote MCP olarak çalışır. İki yol var:

### Yöntem A — Hosted (önerilen)
1. [pipeboard.co](https://pipeboard.co) üzerinden hesap aç, Meta hesabını bağla.
2. Claude Code'a remote MCP olarak ekle:
   ```bash
   claude mcp add --transport http meta-ads https://meta-ads.mcp.pipeboard.co/
   ```
3. İlk kullanımda tarayıcıdan Pipeboard ile giriş yaparsın. Token ile geçmek istersen:
   ```bash
   claude mcp add --transport http meta-ads "https://meta-ads.mcp.pipeboard.co/?token=$PIPEBOARD_API_TOKEN"
   ```
   (`PIPEBOARD_API_TOKEN`'ı `.env`'e koy.)

Hazır config: [`mcp/meta-ads-mcp.json`](../mcp/meta-ads-mcp.json)

### Yöntem B — Self-host (ileri seviye)
Kendi Meta Developer App'inle kaynaktan kurmak istersen, [kaynak repo](https://github.com/pipeboard-co/meta-ads-mcp)'daki
talimatları izle ve `.env`'deki `META_ACCESS_TOKEN`, `META_AD_ACCOUNT_ID` değerlerini doldur.

---

## 2. Google + Meta + GA4 MCP (Ryze AI)

**Kaynak:** [irinabuht12-oss/google-meta-ads-ga4-mcp](https://github.com/irinabuht12-oss/google-meta-ads-ga4-mcp) · 250+ araç

Hosted SSE endpoint olarak çalışır. Endpoint URL'i **public değildir** — hosted servis
**[Ryze AI](https://www.get-ryze.ai/)** üzerinden sağlanır.

1. [Ryze AI](https://www.get-ryze.ai/)'dan (veya kaynak repodaki `docs/SETUP_CLAUDE.md` /
   `docs/SETUP_N8N.md` rehberinden) kendi MCP endpoint URL'ini al.
2. URL'i `.env`'e `GA_MCP_ENDPOINT_URL` olarak kaydet.
3. Claude Code'a ekle:
   ```bash
   claude mcp add --transport sse google-meta-ads-ga4 "$GA_MCP_ENDPOINT_URL"
   ```

Hazır config: [`mcp/google-ads-mcp.json`](../mcp/google-ads-mcp.json) (URL'i env'den okur)

---

## 3. Eklediğini Doğrula

```bash
claude mcp list          # bağlı MCP server'ları listeler
```
Claude Code oturumunda `/mcp` yazarak da bağlı server'ları ve araçlarını görebilirsin.

Çalıştığını test et:
```bash
claude "Meta Ads hesabımdaki aktif kampanyaları listele"
```

---

## 4. Sık Sorunlar

| Sorun | Çözüm |
|-------|-------|
| `command not found: claude` | Claude Code kurulu mu? Bkz. [`docs/KURULUM.md`](KURULUM.md) |
| MCP bağlanmıyor / 401 | Token süresi dolmuş olabilir; ilgili servisten yenile |
| `GA_MCP_ENDPOINT_URL` boş | Kaynak repodan endpoint URL'ini alıp `.env`'e ekle |
| Araçlar görünmüyor | `claude mcp list` ile bağlantıyı, sonra `/mcp` ile araçları kontrol et |

---

## Neden npx Değil?

Önceki sürümde bu config'ler `npx -y @scope/paket` kullanıyordu; ancak bu MCP server'lar
npm paketi olarak yayınlanmıyor — **hosted servisler**. Bu rehber, her server'ın resmî
kurulum yöntemini (remote MCP / SSE endpoint) yansıtır. Şüphede kalırsan yukarıdaki
kaynak repo linklerine bak; gerçeğin tek kaynağı onlardır.
