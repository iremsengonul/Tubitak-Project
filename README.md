# Sürdürülebilir İnsani Yardım Lojistiği için Enerji Kısıtlı ve Ürün Bozulmasına Duyarlı Minimax Tesis Yerleşim Modeli

**TÜBİTAK 2209-A Üniversite Öğrencileri Araştırma Projeleri Destekleme Programı**

- **Proje Yürütücüsü:** İrem Şengönül

---

## Proje Hakkında

Bu proje, afet koşullarında (deprem, yangın) ilaç tedarik zincirinin sürdürülebilirliğini artırmayı amaçlamaktadır. Tetanos aşısı, insülin ve enzim bazlı merhemler gibi 2–8 °C aralığında saklanması gereken ilaçlar için **soğuk hava depolarının en uygun konumlarını** belirleyen bir karar destek modeli geliştirilmektedir.

Model, **Minimax** yaklaşımıyla afet sonrası en uzak talep noktasına olan maksimum erişim süresini en aza indirir. Bunu yaparken depo kapasitesi, toplam enerji tüketimi ve ilaçların bozulma süresi kısıtlarını da dikkate alır.

**Pilot bölge:** İzmir (deprem kuşağında yer alması ve orman yangını riskinin yüksek olması nedeniyle seçilmiştir).

## Araştırma Sorusu

> Afet riski yüksek olan pilot bölgede, afet sonrası ilaç erişim süresini minimize eden, enerji ve kapasite kısıtlarını sağlayan soğuk zincir ilaç depolarının konumlandırması nasıl optimize edilir?

## Hipotezler

- **H1:** Minimax algoritmasıyla geliştirilen tesis yerleşim modeli, mevcut sistemlere kıyasla afet sonrası maksimum erişim süresini azaltır.
- **H2:** Enerji tüketimi ve ilaç bozulma süresi kısıtlarının modele entegre edilmesi, sistemin sürdürülebilirliğini ve operasyonel verimliliğini artırır.
- **H3:** Önerilen model, afet senaryoları altında lojistik ağın erişilebilirliğini koruyarak ilaç tedarik zincirinin sürekliliğini güçlendirir.

## Matematiksel Model

### Parametreler

| Sembol | Açıklama |
|---|---|
| $I$ | Talep noktaları kümesi |
| $J$ | Depo / hastane adayları kümesi |
| $w_i$ | Talep miktarı (örn. kişi sayısı) |
| $c_j$ | Depo $j$'nin kapasitesi |
| $e_j$ | Depo $j$'nin enerji tüketim oranı (kWh/saat) |
| $E_{max}$ | Sistemde izin verilen maksimum toplam enerji tüketimi |
| $d_{ij}$ | Talep noktası $i$ ile depo $j$ arası mesafe |
| $v$ | Taşıma hızı |
| $T_{max}$ | Ürünün bozulmadan ulaşabileceği maksimum süre |
| $t_{ij} = d_{ij}/v$ | Ulaşım süresi |

### Karar Değişkenleri

| Değişken | Açıklama |
|---|---|
| $x_j \in \{0,1\}$ | Depo $j$ açılırsa 1 |
| $y_{ij} \in \{0,1\}$ | Talep noktası $i$, depo $j$'den hizmet alırsa 1 |
| $z \geq 0$ | En kötü durumdaki ağırlıklı mesafe (maksimum değer) |

### Amaç Fonksiyonu

$$\min_{x,y} \; \max_{i \in I, j \in J} \left( w_i \cdot d_{ij} \cdot y_{ij} \right)$$

Doğrusal hâli: $\min z$ öyle ki $w_i \, d_{ij} \, y_{ij} \leq z, \;\; \forall i \in I, j \in J$

### Kısıtlar

1. Her talep noktası bir depodan hizmet almalı: $\sum_{j \in J} y_{ij} = 1, \;\; \forall i \in I$
2. Depo açılmadan hizmet veremez: $y_{ij} \leq x_j, \;\; \forall i \in I, j \in J$
3. Depo kapasitesi aşılmamalı: $\sum_{i \in I} w_i \, y_{ij} \leq c_j \, x_j, \;\; \forall j \in J$
4. Ürün bozulmadan ulaşmalı: $t_{ij} \, y_{ij} \leq T_{max}, \;\; \forall i \in I, j \in J$
5. Toplam enerji tüketimi sınırı: $\sum_{j \in J} e_j \, x_j \leq E_{max}$
6. İkili değişkenler: $x_j, y_{ij} \in \{0,1\}$

## Kullanılan Teknolojiler

- **Python**
- **PuLP** ve **Pyomo** (açık kaynak optimizasyon kütüphaneleri)
- **Gurobi** (akademik lisans ile çözücü)

## Kurulum ve Çalıştırma

```bash
pip install pulp pyomo gurobipy
python main.py
```

> Gurobi'yi tam kapasiteyle kullanmak için akademik lisans gereklidir: https://www.gurobi.com/academia/

## Proje Takvimi

| Tarih | Faaliyet |
|---|---|
| 07/2026 – 10/2026 | Veri toplama, afet senaryolarının belirlenmesi, veri temizliği |
| 09/2026 – 12/2026 | Model tasarımı ve matematiksel formülasyon |
| 11/2026 – 02/2027 | Python ile model kodlama ve Gurobi entegrasyonu |
| 12/2026 – 04/2027 | Simülasyon, sonuç analizi ve duyarlılık testleri |

## Beklenen Çıktılar

- Ulusal veya uluslararası hakemli bir konferansta tam metin bildiri
- Afet öncesi planlamada kullanılabilecek karar destek aracı prototipi
- İnsani yardım kuruluşları için enerji verimli dağıtım stratejileri
- Modelin başka illere ölçeklenebilmesi

## Anahtar Kelimeler

Afet Lojistiği · İlaç Tedarik Zinciri · İnsani Yardım Lojistiği · Minimax · Soğuk Hava Deposu · Sürdürülebilirlik · Tesis Yerleşimi
