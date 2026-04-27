# 🏠 House Price Prediction | Ev Fiyat Tahmin Modeli

Bu proje, Ames Iowa'daki konutlara ait 79 özellik kullanılarak ev satış fiyatlarını  
tahmin eden uçtan uca bir makine öğrenmesi pipeline'ı içermektedir.

[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://www.python.org/)
[![Scikit-learn](https://img.shields.io/badge/Scikit--learn-1.0+-orange.svg)](https://scikit-learn.org/)
[![XGBoost](https://img.shields.io/badge/XGBoost-1.7+-green.svg)](https://xgboost.readthedocs.io/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 📋 İçindekiler
- [İş Problemi](#iş-problemi)
- [Veri Seti](#veri-seti)
- [Proje Yapısı](#proje-yapısı)
- [Yöntem](#yöntem)
- [Sonuçlar](#sonuçlar)
- [Kurulum](#kurulum)
- [Kullanım](#kullanım)

---

## 💼 İş Problemi

Her bir eve ait özelliklerin ve ev fiyatlarının bulunduğu veri seti kullanılarak,  
farklı tipteki evlerin fiyatlarına ilişkin bir makine öğrenmesi modeli geliştirilmesi hedeflenmiştir.

---

## 📦 Veri Seti

| Özellik | Değer |
|:---|:---|
| Kaynak | [Kaggle - House Prices: Advanced Regression Techniques](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques) |
| Toplam Gözlem | 1,460 (train) + 1,459 (test) |
| Sayısal Değişken | 38 |
| Kategorik Değişken | 43 |
| Hedef Değişken | SalePrice |

---

## 📁 Proje Yapısı
```
house-price-prediction/
│
├── 📓 house_price_prediction.ipynb   # Ana notebook
├── 📄 train.csv                      # Eğitim verisi
├── 📄 test.csv                       # Test verisi
├── 📄 data_description.txt           # Değişken açıklamaları
├── 📄 House_Price.pdf                # Proje brief dökümanı
├── 📄 submission.csv                 # Kaggle submission dosyası
└── 📄 README.md                      # Proje açıklaması
```

---

## 🔧 Yöntem

### 1. Keşifçi Veri Analizi (EDA)
- Train ve test veri setleri birleştirildi
- Numerik ve kategorik değişkenler ayrıştırıldı
- Dağılım analizi, aykırı değer ve eksik değer tespiti yapıldı
- Kategorik değişkenler ile hedef değişken ilişkisi incelendi

### 2. Feature Engineering
- **Eksik değer doldurma:** Yapısal eksiklikler `No Garage`, `No Basement` vb. ile dolduruldu
- **Aykırı değer baskılama:** IQR yöntemiyle capping uygulandı
- **Rare Encoding:** %1 altındaki nadir kategoriler `Rare` etiketi ile birleştirildi
- **29 yeni değişken** türetildi:
  - Kompozit kalite skoru (`NEW_TotalQual`)
  - Alan değişkenleri (`NEW_TotalHouseArea`, `NEW_TotalSqFeet`)
  - Oran değişkenleri (`NEW_LotRatio`, `NEW_RatioArea`)
  - Yaş değişkenleri (`NEW_HouseAge`, `NEW_GarageSold`)
  - Etkileşim değişkenleri (`NEW_GarageGrLiv`, `NEW_1stGrLiv`)
- **Label Encoding** ve **One-Hot Encoding** uygulandı

### 3. Model Kurma
- 8 farklı model karşılaştırıldı (Ridge, Lasso, KNN, CART, RF, GBM, XGBoost, LightGBM)
- Hedef değişkene `log1p` dönüşümü uygulandı
- GridSearchCV ile hiperparametre optimizasyonu yapıldı
- GBM ve XGBoost **ensemble** ile final tahmin üretildi

---

## 📊 Sonuçlar

| Model | RMSE (log) |
|:---|:---:|
| Ridge | 0.2000 |
| Lasso | 0.1763 |
| KNN | 0.2356 |
| CART | 0.2026 |
| Random Forest | 0.1378 |
| Gradient Boosting | 0.1248 |
| LightGBM | 0.1307 |
| XGBoost | 0.1367 |
| **GBM + XGBoost Ensemble (Final)** | **0.1229** |

### En Önemli Değişkenler
1. `OverallQual` — Genel kalite puanı
2. `NEW_TotalQual` — Kompozit kalite skoru (türetilmiş)
3. `NEW_GarageGrLiv` — Garaj × Yaşam alanı etkileşimi (türetilmiş)
4. `NEW_TotalHouseArea` — Toplam ev alanı (türetilmiş)
5. `NEW_HouseAge` — Evin yaşı (türetilmiş)

> 🌟 Top 5'in 4'ü feature engineering ile türetilen değişkenler!

---

## ⚙️ Kurulum

```bash
# Repoyu klonla
git clone https://github.com/kullaniciadi/house-price-prediction.git
cd house-price-prediction

# Gerekli kütüphaneleri yükle
pip install pandas numpy matplotlib seaborn scikit-learn xgboost lightgbm
```

---

## 🚀 Kullanım

```bash
# Jupyter Notebook ile aç
jupyter notebook house_price_prediction.ipynb
```


## 🛠️ Kullanılan Teknolojiler

| Kütüphane | Kullanım Amacı |
|:---|:---|
| `pandas` | Veri manipülasyonu |
| `numpy` | Sayısal işlemler |
| `matplotlib` & `seaborn` | Görselleştirme |
| `scikit-learn` | Model kurma & değerlendirme |
| `xgboost` | XGBoost modeli |
| `lightgbm` | LightGBM modeli |

---

## 👤 Yazar

**[Çağla Üzümcü]**  
[LinkedIn](https://linkedin.com/in/çağla-üzümcü-809605202/) · [GitHub](https://github.com/caglauzumcuu) 

---


