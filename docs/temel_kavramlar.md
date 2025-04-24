# IDS/IPS Temel Kavramlar

## IDS ve IPS nedir?

IDS | Instrusion Detection System | İzinsiz Giriş **Tespit** Sistemi
- Pasif izleme yapar, saldırıları **loglar** ve uyarı verir.
- Olayları kaydeden bir güvenlik kamerası olarak düşünüşebilir. İzler, kaydeder fakat müdahale etmez.
- **Dedektif**

IPS | Intrusion Prevention System | İzinsiz Giriş Önleme Sistemi
- **Aktif** müdahale eder. Saldırıları **engeller**.
- Kapıdaki güvenlik görevlisi gibi düşünülebilir. Şüpheliyi içeri almaz.
- **Polis**
 
## IDS vs. IPS
| Özellik      | IDS                    | IPS                     |
| ------------ | ---------------------- | ----------------------- |
| **Tepki verme**    | Pasif (Loglama/Uyarı)  | Aktif (Engelleme)       |
| **Kullanım** | *`snort -l`             | *`suricata -q`           |
| **Örnek**    | Port taramasını tespit | Brute force'u engelleme |
| **Gecikme**  | Düşük              | Yüksek (Analiz süresi) |
| **Risk**     | False Positive     | False Negative     |

- `snort -l /log/dizin`: Komut, snort'un **loglama modunda** yani IDS gibi çalıştırıldığını ifade eder. -l komutu ile logların nereye kaydedileceği belirtilir. 
- `suricata -q 0`: Suricata'yı bir IPS gibi çalıştırmak için kullanılır. `-q` parametresi ile hangi NFQUEUE kuyruğunu dinleyeceğini belirtirsin. Bu modda suricata gelen paketleri analiz eder ve şüpheli olanları **aktif olarak** engeller. Yani gerçek zamanlı müdahale de bulunur.

- Gecikme burada, **ağ paketlerinin analiz edilip işlenmesi sırasında oluşan zaman farkını** ifade ediyor. 
    - IDS (Snort): Paketi alır, kopyasını inceler ama aktarıma müdahale etmez. Bu yüzden **gecikme çok düşüktür**.
    - IPS (Suricata): Paketi analiz eder. Analiz ettikten sonra karar verir: paket geçsin mi, engellensin mi ? Bu analiz süresi bir kaç milisaniyelikte olsa gecikme yaratır. Kritik ağlarda bu bile fark edilebilir.

- False Positive: Kısaca aslında tehdit olmayan bir şeyi tehdit olarak algılamaktır. **Mesela normal bir port taramasını saldırı olarak algılayıp alarm vermesi**. Bu durum IDS'lerde daha sık olur çünkü **saldırı benzeri davranışlar, saldırılardan daha yüksek bir olasılık getirir.** Bu nedenle de IDS yanlış pozitif olarak değerlendirilir.
- False Negative: **Gerçek bir saldırıyı görememesi, gözden kaçırması.** Mesela gerçek bir brute force saldırısını fark edememesi durumu. IPS sistemleri bazen performans kaygısıyla bazı paketleri atlayabilir. Bu da false negative, yanlış negatif riskini arttırır.



# Snort

## Modüler Yapı

![Snort-Moduler-Yapı](https://github.com/user-attachments/assets/cf57a4c7-0b98-4931-b8bf-c224a10f4346)
*Yukarıdaki görsel lastguardsecurity.com internet sitesinden alınmıştır.*

Snort temelde 4 modülden oluşur. Bunlar kod çözücü, ön işlemci, tespit motoru, alarm üretimi. İşlemler aşağıdaki gibi gerçekleşir.
- Libpcap tarafından yakalanan paketler hem .pcap dosyaları aracılığıyla hem de canlı trafik üzerinden çözümlenir. Kod çözücü, paketleri katmanlarına ayırır. (Ethernet, IP, TCP/UDP gibi..)
- Ön işlemci, paketleri tespit motorunun anlayabileceği şekle sokar.
- Tespit motoru, Snort'un beynidir diyebiliriz. Tespit motorunda kural setleri yazılır. Bu kısımda kural setleri ile saldırı tespitleri yapılır.
- Uyarı oluşturma kısmı ise tespit edilen saldırıların ne tür uyarı oluşturacağını belirler. 

![Snort-Moduler-Yapı2](https://github.com/user-attachments/assets/71bbd172-a08e-4867-8912-4ba956a042be)
*DÜMF Mühendislik Dergisi syf. 66*

- Yukarıdaki görselden de gördüğümüz gibi oluşturulan uyarılardan bir uyarı veritabanı oluşturulabilir. Daha sonra uyarılar oluşturulur.

* libpcap, ağ arayüzü üzerinden geçen trafiği yakalamak ve işlemek için kullanılan bir düşük seviye C kütüphanesidir. Ağdaki ham paketleri yakalar. Snort, Wireshark gibi uygulamalar ise bu verileri analiz eder.

# Suricata 





NOT:

Aslında Snort'ta, Suricata'da hem IDS hem IPS olarak çalışabilir. Fakat ilk niyet ve varsayılan kullanım şekli Snort -> IDS, Suricata -> IPS olarak bir **etiketlenmeye** yol açtı. Bunu iki neden de inceleyecek olursak;
- Snort, ilk çıktığında sadece bir IDS'ti. Daha sonraki sürümlerinde IPS olarakta kullanılabiliyor olmasına rağmen, IDS olarak kullanılmaya devam etti.
- Suricata IPS destekli olarak tasarlandı ve IPS olarak Snort'tan daha performanslı çalışmakta. 

Yani kısacası, topluluk alışkanlıkları ve yaygın kullanım şekillerinden dolayı snort IDS, suricata IPS olarak kullanılıyor. Fakat her ikiside hem IDS, hem IPS olarak çalışabiliyor.


