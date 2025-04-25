---
Oluşturma Tarihi: 2025-04-25T04:33
Güncelleme Tarihi: 2025-04-25T09:32
---


Ubuntu, kali... paket yöneticisi

```bash
apt install suricata
```

```bash
apt install snort
```

Arch...

```bash
yay -S suricata
```

```bash
yay -S snort
```

Version

```bash
snort -V
```

```bash
suricata -V
```

Snort dizini

```bash
cd /etc/snort
ls
```

- `snort.conf` -> Ana yapılandırma dosyası
- `rules dizini` -> **imza tabanlı tespit kurallarını** içeren dosyalar bulunur
	- Örneğin: Web saldırılarına, exploit tespitlerine yönelik kurallar
- `clasification.config` -> Hangi alarmın hangi kuralı vereceğini ve kategorilerini belirliyoruz
- `file_magic.conf` -> Snort'un tespit için kullandığı dosya tiplerini tanımlayan imza kuralları bulunuyor
- `gen-msg.map` -> Kural IDleri ve açıklayıcı mesajları eşleştiren bir dosya
- `reference.config` -> Alarmlar için harici referans linkleri
- `threshold.conf` -> Alarmlar için eşik değerleri ve bastırma kuralları
	- suppression gen_id 1, sig_id 1852, track by_src, ip 192.168.1.100
	
	  Eğer `sig_id 1852`  (signature (imzalı)) numaralı alarm, **192.168.1.100** IP adresinden geliyorsa, bu alarmı **görmezden gel** (loglama, uyarı verme vb. yapma).
- `unicode.map` -> Unicode karakter dönüşüm dosyasıdır
	- Bu dosya da genelde UNICODE saldırılarını tespit etmek için kullanılır.

Suricata Dizini

```bash
cd /etc/suricata
ls
```

`suricata.yaml` -> Ana yapılandırma dosyası

`clasification.config` -> Alarmların öncelik seviyeleri ve kategorileri bulunuyor

`reference.config` -> Alarmlar için harici referans linkleri

```bash
nano /etc/snort/snort.conf
```

```bash
-w -l /etc/snort/snort.conf # Satır sayısı
```

```bash
nano /etc/suricata/suricata.yaml
```

```bash
-w -l /etc/suricata/suricata.yaml
```