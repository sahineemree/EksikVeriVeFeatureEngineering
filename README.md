# Feature Engineering: Eksik Verileri Anlama ve İşleme Rehberi

Gerçek dünya verileriyle çalışırken "kayıp veriler" (missing values) en sık karşılaşılan problemlerden biridir. Bu eksiklikleri doğru yönetmek, modelinizin başarısını doğrudan etkiler. Bu rehberde eksik veri türlerini ve bunlarla başa çıkma yöntemlerini inceleyeceğiz.

---

## 1. Eksik Veri Türleri (Neden Eksikler?)

Eksik veriyi nasıl dolduracağımıza karar vermeden önce, verinin neden eksik olduğunu anlamamız gerekir. Bunu üç ana gruba ayırıyoruz:

### A. Tamamen Rastgele Eksiklik (MCAR - Missing Completely at Random)
Verinin eksik olmasının, veri setindeki başka hiçbir değişkenle veya eksik olan değerin kendisiyle bir ilgisi yoktur.

* **Örnek:** Bir anket formunun bir sayfası rüzgarda uçtuğu için bazı cevapların kaybolması.
* **Etki:** Veride bir yanlılık (bias) yaratmaz. Bu satırları silmek veya basit yöntemlerle doldurmak genellikle sorun çıkarmaz.

### B. Rastgele Eksiklik (MAR - Missing at Random)
Eksiklik, veri setindeki gözlemlenebilir başka bir değişkene bağlıdır.

* **Örnek:** Erkeklerin kilo bilgisini paylaşmaya kadınlardan daha az eğilimli olması. Burada "kilo" bilgisinin eksik olması "cinsiyet" değişkeniyle ilişkilidir.
* **Etki:** Sadece ortalamayı almak yerine, cinsiyet gibi ilişkili diğer özellikleri kullanarak tahmin yapmak (regresyon vb.) daha mantıklıdır.

### C. Rastgele Olmayan Eksiklik (MNAR - Missing Not at Random)
Eksiklik, eksik olan değerin kendisiyle ilgilidir.

* **Örnek:** Çok yüksek maaş alan kişilerin, mahremiyet nedeniyle anketlerde maaşlarını belirtmemesi.
* **Etki:** En tehlikeli türdür çünkü veride gizli bir desen/bias vardır. Bunu çözmek için alan uzmanlığı (domain knowledge) gerekir.

---

## 2. Eksik Verilerle Başa Çıkma Yöntemleri

### 1. Veriyi Silmek (Drop)
Eğer eksik veri miktarı çok azsa (örneğin tüm verinin %5'inden azı), bu satırları tamamen silebilirsiniz.

```python
# Tüm eksik değer içeren satırları siler
df.dropna(inplace=True)
