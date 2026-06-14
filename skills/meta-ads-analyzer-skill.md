# Meta Ads Analyzer Skill — Claude Code

## Konsept

Uzman seviyesinde Meta Ads kampanya teşhisi. Learning Phase, Breakdown Effect ve campaign diagnosis.

> Kaynak: [mathiaschu/meta-ads-analyzer](https://github.com/mathiaschu/meta-ads-analyzer) (364⭐)

## Kullanım

```bash
claude "Kampanya 'Summer Sale' learning phase'ta ne durumda?"
claude "Breakdown Effect analizi yap"
claude "Kampanya teşhisi: ROAS düşük, neden?"
```

## Learning Phase Analizi

### Ne Zaman Tamamlanır?
- Minimum 50 conversion (optimizasyon event)
- 7 gün geçmesi
- Haftalık spend'in stable olması

### Learning Phase'te YAPILMAZ
- ❌ Bütçe değişikliği (learning phase sıfırlanır)
- ❌ Audience değişikliği
- ❌ Bid strategy değişikliği
- ❌ Creative değişikliği

### Learning Phase Tamamlandıktan Sonra
- ✅ Büyük değişiklikler artık güvenli
- ✅ Audience genişletme
- ✅ Bid artırımı

## Breakdown Effect Analizi

### Yaygın Breakdown Türleri

1. **Age/Gender Breakdown**
   - Hangi demografik grubun performansı düşük?
   - Düşük performanslı grupları exclude et

2. **Placement Breakdown**
   - Instagram Feed vs Stories vs Reels
   - Facebook News Feed vs Right Column
   - Audience Network performansı

3. **Device Breakdown**
   - Mobile vs Desktop CTR ve Conversion farkı
   - Düşük performanslı cihazı exclude et

4. **Geography Breakdown**
   - Hangi şehirler/ülkeler düşük performanslı?
   - Placement exclusion

### Diagnosis Framework

```
Step 1: ROAS hesapla (Revenue / Spend)
Step 2: Breakdown analizi yap (age, gender, placement, device, geo)
Step 3: Düşük performanslı segment'leri tespit et
Step 4: Exclusion öner (audience, placement)
Step 5: Creative refresh öner (eğer creative fatigue varsa)
Step 6: Bid adjustment öner
```

## Campaign Health Check

Her kampanya için kontrol et:

| Metrik | İyi | Kötü |
|--------|-----|------|
| ROAS | > 4x | < 2x |
| CTR | > 2% | < 0.5% |
| CPC | < 50% of target CPA | > CPA |
| Frequency | < 3 | > 7 |
| Learning Phase | ✅ Complete | ⚠️ Still learning |

## Örnek Diagnosis

```
Kampanya: "Summer Sale - Retargeting"
ROAS: 1.2x (hedef: 3x) ❌
Learning Phase: Complete ✅
CTR: 1.8% (orta)
CPC: ₺8.50

Breakdown Analysis:
- Kadın 25-34: ROAS 2.1x ✅
- Kadın 35-44: ROAS 0.8x ❌
- Erkek: ROAS 0.5x ❌

Öneriler:
1. Erkekleri audience'dan çıkar
2. Kadın 35-44 bid'ini %20 düşür
3. Kadın 25-34 bid'ini %30 artır
4. Creative refresh yap (5 varyasyon ekle)
```
