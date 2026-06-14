# Katkıda Bulunma

## Nasıl Katkıda Bulunulur?

1. Bu repoyu fork'la
2. Yeni bir branch oluştur: `git checkout -b yeni-ozellik`
3. Değişikliklerini yap
4. Commit at: `git commit -m 'Yeni özellik: ...'`
5. Push at: `git push origin yeni-ozellik`
6. Pull Request aç

## Repolar Arası Karşılaştırma Tablosu

| Özellik | Hangi Repodan Alınmış |
|---------|----------------------|
| Meta Ads kampanya CRUD | meta-ads-mcp |
| Google Ads entegrasyonu | google-meta-ads-ga4-mcp |
| Learning Phase analizi | meta-ads-analyzer |
| Claude Code skill | NotFair |
| Audit framework | claude-ads |
| n8n workflow'ları | google-meta-ads-ga4-mcp |
| GA4 entegrasyonu | claude-ads |
| Human-in-the-loop | markifact-mcp |

## Yeni Özellik Eklerken

1. Hangi repodan ilham alındığını belirt
2. Mevcut yapıya uygun yerleştir
3. README.md'deki karşılaştırma tablosunu güncelle
4. Docs/KURULUM.md'yi güncelle

## Yeni Platform Ekleme Deseni

Repo'da her platform **aynı 4 parçayla** gelir (Meta/Google/TikTok/LinkedIn böyle eklendi).
Örnek: "Snapchat Ads" eklemek için:

1. **MCP config** → `mcp/snapchat-ads-mcp.json` (gerçek bir MCP server'a işaret etmeli —
   hosted URL veya self-host command. UYDURMA paket adı kullanma; upstream'i doğrula.)
2. **Skill** → `skills/snapchat-ads-skill.md` (`skills/meta-ads-skill.md` formatını izle)
3. **Prompt** → `prompts/snapchat-ads-prompt.md` (`prompts/meta-ads-prompt.md` formatını izle)
4. **Workflow** → `workflows/N-snapchat-rapor.json` (geçerli n8n formatı —
   `workflows/4-tiktok-rapor.json`'u şablon al; node tipleri `n8n-nodes-base.*` olmalı)
5. **README** → "Desteklenen Platformlar" tablosuna satır ekle; varsa kaynak repoyu kredile
6. **.env.example** → gereken yeni env değişkenlerini ekle
7. **Doğrula** → `python3 -c "import json; json.load(open('mcp/...'))"` ve workflow JSON kontrolü

> İlke: araçları biz yazmıyoruz, gerçek MCP server'ları **birleştiriyoruz**. Eklediğin
> her şey upstream'de gerçekten var olmalı (link ver). Geri alınamaz işlemler (kampanya
> yayına alma) prompt'larda **PAUSED/taslak** varsayılanıyla, insan-döngüde kalmalı.
