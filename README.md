# 🧩 Feature Engineering: Eksik Verileri Anlama ve İşleme Rehberi

Eksik verilerle doğru şekilde başa çıkmak, makine öğrenmesi ve veri analizi projelerinde **model başarısını doğrudan etkileyen** kritik bir adımdır. Bu rehberde, eksik verilerin **neden oluştuğunu** ve **nasıl ele alınması gerektiğini** net ve pratik bir şekilde ele alıyoruz.

---

## 🔍 1. Eksik Veri Türleri (Neden Eksikler?)

Eksik veriyi **nasıl dolduracağımıza karar vermeden önce**, verinin **neden eksik olduğunu** anlamamız gerekir. Bu durum üç ana başlık altında incelenir:

---

### 🎲 A. Tamamen Rastgele Eksiklik (MCAR – Missing Completely at Random)

Verinin eksik olması, veri setindeki **başka hiçbir değişkenle** veya **eksik olan değerin kendisiyle** ilişkili değildir.

**Örnek:**

* Bir anket formunun bir sayfasının rüzgarda uçması sonucu bazı cevapların kaybolması.

**Etki:**

* Veride **yanlılık (bias)** oluşturmaz.
* Bu satırları silmek veya basit yöntemlerle doldurmak genellikle sorun yaratmaz.

---

### 🔗 B. Rastgele Eksiklik (MAR – Missing at Random)

Eksiklik, veri setindeki **gözlemlenebilir başka bir değişkene** bağlıdır.

**Örnek:**

* Erkeklerin kilo bilgisini paylaşmaya kadınlardan daha az eğilimli olması.
* Burada kilo bilgisinin eksikliği, **cinsiyet** değişkeniyle ilişkilidir.

**Etki:**

* Sadece ortalama almak yerine,
* Cinsiyet gibi **ilişkili değişkenleri** kullanarak tahmin yapmak (örneğin regresyon) daha mantıklıdır.

---

### ⚠️ C. Rastgele Olmayan Eksiklik (MNAR – Missing Not at Random)

Eksiklik, **eksik olan değerin kendisiyle** doğrudan ilişkilidir.

**Örnek:**

* Çok yüksek maaş alan kişilerin, mahremiyet nedeniyle anketlerde maaşlarını belirtmemesi.

**Etki:**

* En **tehlikeli** eksik veri türüdür.
* Veride gizli bir desen / **bias** bulunur.
* Çözüm için mutlaka **alan uzmanlığı (domain knowledge)** gerekir.

---

## 🛠️ 2. Eksik Verilerle Başa Çıkma Yöntemleri

Eksik verilerle çalışırken kullanabileceğimiz temel yöntemler aşağıda özetlenmiştir.

---

### 🗑️ 1. Veriyi Silmek (Drop)

* Eğer eksik veri miktarı çok azsa (genellikle **%5’ten az**),
* Bu satırlar tamamen silinebilir.

```python
df.dropna(inplace=True)
```

---

### ✏️ 2. İmputasyon (Doldurma Yöntemleri)

Eksik verileri çeşitli stratejilerle doldurabiliriz:

* **İstatistiksel Doldurma**

  * Sayısal veriler: **Ortalama (Mean)** veya **Medyan (Median)**
  * Kategorik veriler: **Mod** (en sık tekrar eden değer)

* **Zaman Serisi Doldurma**

  * Önceki değeri kopyalama (**Forward Fill**)
  * Sonraki değeri kopyalama (**Backward Fill**)

* **Tahmin Dayalı Doldurma**

  * **KNN (K-En Yakın Komşu)** gibi algoritmalarla,
  * Benzer satırlara bakarak eksik değer tahmin edilir.

---

### 🧠 3. Eksiklik Göstergesi Ekleme (Missing Indicator)

* Bazen bir verinin **eksik olması bile başlı başına bir bilgidir**.
* Eksik değer doldurulurken, yanına yeni bir sütun eklenir:

  * **0 → Veri vardı**
  * **1 → Veri eksikti**

Bu yöntem özellikle **ağaç tabanlı modellerde** oldukça etkilidir.

---

### 🧑‍🔬 4. Alan Uzmanlığını (Domain Knowledge) Kullanmak

* Eğer yüksek maaşlı bireylerin veri girmediği biliniyorsa (MNAR durumu),
* Bu boş değerler:

  * **"Yüksek Gelir Grubu"** gibi yeni bir kategoriye atanabilir.

Bu yaklaşım, istatistiksel yöntemlerin yetersiz kaldığı durumlarda **en sağlıklı çözümdür**.

---

📌 **Özetle:**

* Eksik veriyle mücadelede **tek bir doğru yöntem yoktur**.
* Doğru yaklaşım, eksikliğin türüne ve problemin bağlamına göre seçilmelidir.
