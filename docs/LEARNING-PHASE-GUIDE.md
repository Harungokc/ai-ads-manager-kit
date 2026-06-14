# Learning Phase Rehberi

## Learning Phase Nedir?

Meta Ads, her yeni kampanya veya önemli değişiklikten sonra algoritmayı öğrenmeye başlar. Bu süreç **Learning Phase** olarak adlandırılır.

## Ne Kadar Sürer?

- Minimum: 7 gün
- Optimum: 50 conversion
- Bazı kampanyalar: 28 güne kadar sürebilir

## Learning Phase Sürecinde Ne Olur?

```
Gün 1-3: Algoritma ilk verileri toplar, maliyet yüksek
Gün 4-7: Algoritma öğrenmeye başlar, maliyet düşer
Gün 8-14: Performans stabilizasyonu
Gün 15+: Learning Phase tamamlanır (ideal)
```

## Learning Phase'te Nelere Dikkat Etmeli?

### ❌ YAPMA
- Bütçe değişikliği (especially artış)
- Audience değişikliği
- Bid strategy değişikliği
- Creative değişikliği
- Yeni conversion event ekleme
- Campaign/Ad Set pause etme

### ✅ YAP
- Performansı izle
- Kritik sorunları düzelt (website downtime, etc.)
- Audience'u genişletmek yerine bekle

## Learning Phase Tamamlandıktan Sonra

Artık güvenli değişiklikler:
- ✅ Bütçe artırımı/azaltımı
- ✅ Audience genişletme
- ✅ Bid artırımı
- ✅ Creative refresh

## Learning Phase Reset

Aşağıdaki değişiklikler Learning Phase'i sıfırlar:
- Audience değişikliği (>%50 overlap dışında)
- Bid strategy değişikliği
- Conversion event değişikliği
- Bütçe değişikliği (>%20)
- 7+ gün pause

## How to Check Learning Phase Status

```python
# Meta Marketing API ile
GET /act_{ad_account_id}/campaigns?fields=name,learning_stage_info
```

## Learning Phase Status Değerleri

| Status | Anlamı |
|--------|--------|
| NONE | Learning phase yok (yeterli veri var) |
| LEARNING | Learning phase aktif |
| LEARNED | Learning phase tamamlandı |

## Best Practices

1. **Sabır** — En az 7 gün bekle, ideal 14-28 gün
2. **Küçük bütçe** — Learning phase'teyken günlük 100-200₺ ile başla
3. **Birden fazla değişiklik yapma** — Her değişiklik reset
4. **Düşük performans kabul et** — Bu normal, sabah 7:00
