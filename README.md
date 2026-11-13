# IoT/IIoT Ağlarında Siber Saldırı Tespiti ve Sınıflandırılması

**Ders:** Veri Madenciliği  
**Öğrenci:** Eljan Hajiiyev — 26220903014  
**Üniversite:** İstanbul Topkapı Üniversitesi  
**Dersin öğretim üyesi:** Dr. Öğr. Üyesi Yıldız Karadayı  
**Veri kümesi:** Edge-IIoTset (2022)

## Proje hakkında

Bu proje, IoT ve IIoT ağlarındaki normal trafiği siber saldırı trafiğinden ayırt etmeyi ve saldırı türlerini sınıflandırmayı amaçlamaktadır. Veri kümesindeki 24 ham CSV dosyası incelenmiş; yaklaşık 20,94 milyon kayıttan azınlık sınıflarını koruyan tabakalı örnekleme ile 400.000 kayıt seçilmiştir. Temizleme sonrasında **399.992 kayıt** üzerinde çalışılmıştır.

Çok sınıflı sınıflandırma için **Logistic Regression, Decision Tree, Random Forest ve XGBoost** modelleri karşılaştırılmıştır. Modelleme için eğitim/test ayrımı ve ek olarak üç model için tabakalı beş katlı çapraz doğrulama kullanılmıştır.

## Deney özeti

| Ölçüt | Sonuç |
|---|---:|
| Temizleme sonrası kayıt | 399.992 |
| Eğitim kayıtları | 319.993 |
| Test kayıtları | 79.999 |
| Trafik sınıfları | 15 (Normal + 14 saldırı) |
| Seçilen giriş özniteliği | 20 |
| XGBoost test accuracy (15 sınıf) | %99,39 |
| XGBoost test macro F1 (15 sınıf) | %90,37 |
| XGBoost 5-fold validation accuracy (80.000 eğitim alt örneklemi) | %99,28 |
| XGBoost 5-fold validation macro F1 | %88,03 |
| Random Forest ikili test hataları | 3 yanlış alarm, 0 kaçırılan saldırı |
| Eğitimdeki özniteliklerle eşleşen test kayıtları | 26.169 / 79.999 (%32,71) |

**Yorum ve sınırlılıklar:** Çok yüksek skorlar yalnızca kullanılan veri ayrımı ve örneklem için geçerlidir. Test kayıtlarının %32,71'i seçilmiş 20 öznitelik bakımından eğitim kümesindeki en az bir kayıtla eşleşmektedir. Bu, ham kayıtların bire bir aynı olduğunu kanıtlamaz; ancak oturum bağımlılığı ve genelleme riskleri dikkate alınmalıdır. K-katlı doğrulama da bağımsız bir ağ ortamı doğrulamasının yerine geçmez. Örnekleme, gerçek üretim ağlarındaki saldırı sıklığını temsil etmek zorunda değildir.

## Depo yapısı

```text
notebooks/    # Dokuz Jupyter Notebook (kod + Türkçe Markdown + kayıtlı çıktılar)
results/      # Model karşılaştırmaları ve tahmin CSV dosyaları
figures/      # Grafikler (PNG vb.)
reports/      # IEEE biçimindeki Türkçe ve İngilizce PDF raporları
data/         # Ham verilerin bağlantısı ve indirme notu; büyük veri dosyaları burada tutulmaz
requirements.txt
README.md
.gitignore
```

## Notebook modülleri

1. `ELJAN_HAJIIYEV_26220903014_dataset_overview.ipynb`
2. `ELJAN_HAJIIYEV_26220903014_exploratory_data_analysis.ipynb`
3. `ELJAN_HAJIIYEV_26220903014_data_sampling.ipynb`
4. `ELJAN_HAJIIYEV_26220903014_data_preprocessing.ipynb`
5. `ELJAN_HAJIIYEV_26220903014_data_visualization.ipynb`
6. `ELJAN_HAJIIYEV_26220903014_feature_engineering.ipynb`
7. `ELJAN_HAJIIYEV_26220903014_feature_selection.ipynb`
8. `ELJAN_HAJIIYEV_26220903014_model_training.ipynb`
9. `ELJAN_HAJIIYEV_26220903014_model_evaluation.ipynb`

## Kurulum ve yeniden çalıştırma

```bash
python -m pip install -r requirements.txt
jupyter lab
```

Notebook'lar veri setinin yerel klasör yoluna ve önceki aşamaların ürettiği dosyalara başvurabilir. Farklı bir bilgisayarda çalıştırmadan önce `proje` / veri yolu tanımlarını yerel klasörünüze uyarlayın ve modülleri sırasıyla çalıştırın. Kaydedilmiş çıktılar, ilgili ortamda yeni bir çalıştırmanın yerine geçmez.

## Veri kaynağı

Edge-IIoTset makalesi: Mohamed Amine Ferrag ve diğerleri, *Edge-IIoTset: A New Comprehensive Realistic Cyber Security Dataset of IoT and IIoT Applications for Centralized and Federated Learning*, IEEE Access, 2022. DOI: https://doi.org/10.1109/ACCESS.2022.3165809

Veri kümesi: https://ieee-dataport.org/8939

Ham veriler büyük boyutları nedeniyle bu depoda doğrudan barındırılmamaktadır. İndirme ve kullanım koşulları veri kaynağından kontrol edilmelidir.

## Proje raporu

IEEE konferans makalesi biçiminde hazırlanmış Türkçe/İngilizce raporlar `reports/` klasöründe yer alır.
