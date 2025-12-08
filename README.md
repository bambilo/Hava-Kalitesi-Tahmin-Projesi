# Hava Kalitesi (NO2) Tahmin Projesi

Bu projede, Avrupa'daki hava kalitesi verilerini kullanarak, hava durumunun (nem, sıcaklık vb.) kirlilik üzerindeki etkisini inceledim ve bir **Makine Öğrenmesi (Lineer Regresyon)** modeli geliştirdim.

Veri Kaynağı: Kaggle - Air Quality Europe Dataset.

Proje adımlarım ve kod bloklarında yaptıklarım sırasıyla aşağıdadır:

---

### 1. Veri Yükleme ve Hazırlık
İlk olarak **Pandas, Numpy, Matplotlib** gibi gerekli kütüphaneleri projeme dahil ettim.
- `data.csv` dosyasını okuyup tablo haline getirdim.
- Sütun isimlerini temizledim.
- Hedefim `NO2` (Azot Dioksit) miktarını tahmin etmekti. Ancak veri setinde cevabın kendisini barındıran (kopya veren) `AQI` sütunlarını analizinden çıkardım.

![KOD BLOĞU1](ss1.png)

### 2. En Önemli Özelliği Bulma ve Görselleştirme
Burada, NO2 kirliliğini en çok etkileyen özelliğin ne olduğunu bulmak için **korelasyon** (ilişki) analizi yaptım.
- Bilgisayar analiz sonucunda en etkili faktörün **(Nem)** olduğunu buldu.
- Ben de Nem ile NO2 arasındaki ilişkiyi gösteren renkli bir grafik çizdirdim.
![KOD BLOĞU](ss2.png)

**Grafik Yorumu:**
Aşağıdaki grafikte, nem oranının artışına göre kirliliğin nasıl dağıldığını görüyoruz. Renkler hava kalitesinin iyi veya kötü olduğunu gösteriyor. Verilerin çok dağınık olması, net bir çizgi olmadığını gösteriyor.

![Scatter Plot](grafik1.png)

### 3. Modeli Kurma ve Eğitme
Makine öğrenmesi modelimi burada kurdum.
- Veriyi **%80 Eğitim (Train)** ve **%20 Test** olarak ikiye böldüm. Bunu yapmamın sebebi, modelin ezber yapmasını önlemek ve görmediği verilerle test etmekti.

## 📊 Model Karşılaştırması ve Seçimi

Bu projede hava kalitesi tahmini için farklı makine öğrenmesi algoritmaları denenmiş ve performansları karşılaştırılmıştır. Aşağıdaki tabloda görüldüğü üzere, veri setimizdeki özellikler ile hedef değişken arasındaki ilişkiyi en iyi açıklayan model **Linear Regression** olmuştur.

![KOD BLOĞU](ss5.png)

**Sonuç:** En yüksek $R^2$ skorunu (0.82) ve en düşük hata oranlarını (MSE: 24.79) verdiği için projenin modeli olarak **Lineer Regresyon** seçtim.
- **Linear Regression (Doğrusal Regresyon)** modelini seçip eğitim verisiyle eğittim.Tahmin edeceğim değer bir sınıf değil, sayısal bir değer olduğu için model olarak Linear Regression algoritmasını seçtim.

![KOD BLOĞU](ss3.png)

### 4. Test Etme ve Sonuç Grafiği
Eğittiğim modeli, ayırdığım **Test** verileri üzerinde denedim.
- **Sonuç:** Modelin R2 skoru (Başarı oranı) 0'a yakın çıktı.
- **Grafik Yorumu:** Aşağıdaki grafikte Mavi noktalar gerçek değerler, Kırmızı çizgi ise benim modelimin tahminidir. Kırmızı çizginin düz olması, modelin "Nem oranına bakarak net bir artış veya azalış bulamadım, o yüzden ortalama bir değer tahmin ediyorum" dediğini gösterir.
![Regression Plot](grafik2.png)

### 5. Detaylı İlişki Analizi
Tüm değişkenlerin birbiriyle olan ilişkisini görmek için bir **Isı Haritası** çizdirdim.
- Tablodaki mavi renkler ilişkinin düşük olduğunu, kırmızı renkler yüksek olduğunu gösterir.
- Bizim tablomuzda çoğu yerin mavi olması, veri setindeki özelliklerSin birbirini çok keskin etkilemediğini kanıtlamış oldu.
![grafik3](grafik3.png)

### 6. Tahmin Denemesi
Son olarak modelin çalışıp çalışmadığını görmek için sisteme rastgele bir **Nem** değeri girdim ve modelin bana o nem oranında havadaki NO2 miktarının ne olacağını tahmin etmesini sağladım.

![KOD BLOĞU](ss4.png)

---

## Genel Sonuç
Bu proje sayesinde, elimizdeki veri setinde **Nem oranının tek başına hava kirliliğini belirlemediğini**, verilerin çok dağınık olduğunu bilimsel ve görsel olarak kanıtlamış oldum.

---
