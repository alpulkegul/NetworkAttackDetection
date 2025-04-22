---
Oluşturma Tarihi: 2025-04-22T20:44
Güncelleme Tarihi: 2025-04-22T20:47
---
# IDS/IPS Temel Kavramlar

## IDS vs. IPS
| Özellik      | IDS                    | IPS                     |
| ------------ | ---------------------- | ----------------------- |
| **Tepki**    | Pasif (Loglama/Uyarı)  | Aktif (Engelleme)       |
| **Kullanım** | `snort -l`             | `suricata -q`           |
| **Örnek**    | Port taramasını tespit | Brute force'u engelleme |

## Snort vs. Suricata

**Snort**  

```bash
snort -V  # Kali'de varsayılan: 2.9.xx
```

- Basit kural yazımı (`/etc/snort/rules/local.rules`).
- **Suricata**:

```bash
suricata -V  # Kali'de varsayılan: 6.0.x
```

- Çok iş parçacıklı (multi-threaded) performans.


## Kali'ye Özel Notlar

Snort kuralları: `/etc/snort/rules/`
Suricata logları: `/var/log/suricata/fast.log`
