# LIDAR Doğru Tespiti ve Kesişim Analizi

Bu projede, TOML formatında verilen 2 boyutlu LIDAR verileri okunarak geometrik analizler gerçekleştirilmiştir. LIDAR ölçümlerinden elde edilen nokta bulutu üzerinden doğrular tespit edilmiş, bu doğruların kesişim noktaları hesaplanmış ve belirli açısal koşullara göre analizler yapılmıştır. Ayrıca, kesişim noktaları ile robotun konumu arasındaki mesafe hesaplanarak sonuçlar grafiksel olarak gösterilmiştir.

---

Projenin Amacı

- TOML formatındaki LIDAR verilerini **harici kütüphane kullanmadan** okumak
- Geçersiz LIDAR ölçümlerini filtrelemek
- Kutupsal koordinatları Kartezyen (x, y) koordinatlara dönüştürmek
- Nokta bulutu üzerinden doğruları tespit etmek
- Tespit edilen doğruların kesişim noktalarını hesaplamak
- Belirli bir açıdan büyük doğru çiftlerini seçmek
- Kesişim noktası ile robot konumu arasındaki mesafeyi hesaplamak
- Tüm sonuçları grafiksel olarak görselleştirmek

---

**Kullanılan Teknolojiler**

- Programlama Dili: C / C++
- Veri Formatı: TOML
- Kullanılan Konular:
  - Dosya okuma ve ayrıştırma
  - Veri filtreleme
  - Geometrik hesaplamalar
  - Kutupsal → Kartezyen dönüşüm
  - Doğru tespiti (RANSAC / PCA tabanlı yaklaşımlar)
  - Doğru kesişim ve açı hesaplamaları
  - Grafiksel gösterim

---

**Girdi Verileri**

- LIDAR verileri TOML dosyaları üzerinden alınmaktadır
- Dosyada yer alan temel bilgiler:
  - `angle_min`, `angle_max`, `angle_increment`
  - `range_min`, `range_max`
  - `ranges` (mesafe ölçümleri)

Aşağıdaki değerler filtrelenmektedir:
- NaN veya geçersiz ölçümler
- `range_min` değerinden küçük ölçümler
- `range_max` değerinden büyük ölçümler

Robotun konumu **(0, 0)** olarak kabul edilmiştir.

---

**İşlem Adımları**

1. TOML Dosyasının Okunması  
   LIDAR tarama parametreleri ve mesafe ölçümleri dosyadan okunur.

2. Filtreleme  
   Geçersiz ve sınır dışı ölçümler veri setinden çıkarılır.

3. Koordinat Dönüşümü  
   Kutupsal koordinatlar Kartezyen koordinatlara dönüştürülür.

4. Doğru Tespiti  
   Nokta bulutu içerisinden doğrular belirlenir.  
   En az 8 nokta bir doğru olarak kabul edilir.

5. Kesişim Analizi  
   Tespit edilen doğruların kesişip kesişmediği kontrol edilir ve kesişim noktaları hesaplanır.

6. Açıya Göre Doğru Seçimi
   Doğrular arasındaki açı hesaplanır ve belirlenen eşik açının üzerindeki doğru çiftleri seçilir.

7. Mesafe Hesabı  
   Seçilen doğru çiftlerinin kesişim noktası ile robot konumu arasındaki mesafe hesaplanır.

8. Grafiksel Gösterim  
   Noktalar, doğrular, kesişim noktaları ve robotun konumu grafik üzerinde gösterilir.

---

**Çıktılar**

- LIDAR nokta bulutu
- Tespit edilen doğrular
- Doğru kesişim noktaları
- Kesişen doğrular arasındaki açılar
- Robot ile kesişim noktası arasındaki mesafe
- Grafiksel çıktı

---

**Çalıştırma**

```bash
./program lidar1.toml
