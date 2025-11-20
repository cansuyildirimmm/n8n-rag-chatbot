# 🤖 n8n RAG Chatbot

Bu proje RepoCloud altyapısı üzerinde barındırılan n8n otomasyon platformu kullanılarak geliştirilmiş, Retrieval-Augmented Generation (RAG) mimarisine sahip bir yapay zeka chatbot uygulamasıdır.

Proje belirli bir teknik dokümantasyonu (PDF) analiz eder, verileri vektörel hale getirerek **Supabase** üzerinde saklar ve kullanıcıların bu dokümanla ilgili sorularını **Google Gemini** dil modeli aracılığıyla cevaplar.

Proje iki ana iş akışından (workflow) oluşmaktadır:

### 1. Veri Yükleme ve İşleme (ETL Pipeline)
Bu akış, ham PDF verisini yapay zekanın anlayabileceği vektörlere dönüştürür.
1.  **Data Ingestion:** PDF dosyası Google Drive üzerinden çekilir.
2.  **Text Extraction:** Dosya içeriği metin formatına çevrilir.
3.  **Custom Chunking (JavaScript):** Metin, anlamsal bütünlüğü korumak adına özel bir JavaScript algoritması ile (nokta ve büyük harf duyarlı) küçük parçalara ayrılır.
4.  **Embedding:** Her parça Google Gemini Embedding modeli ile sayısal vektörlere dönüştürülür.
5.  **Storage:** Vektörler ve metin verileri Supabase veritabanına kaydedilir.

### 2. Chatbot ve Sorgulama (Inference Pipeline)
Kullanıcının soru sorduğu canlı sistemdir.
1.  **User Query:** Kullanıcıdan gelen soru alınır.
2.  **Vector Search:** Soru vektöre çevrilir ve Supabase üzerindeki verilerle "Cosine Similarity" kullanılarak karşılaştırılır.
3.  **Context Retrieval:** Soruyla en alakalı metin parçaları veritabanından çekilir.
4.  **Generation:** Bulunan içerik ve kullanıcının sorusu Google Gemini'ye gönderilir ve nihai cevap üretilir.

<img width="756" height="570" alt="Ekran görüntüsü 2025-11-21 013749" src="https://github.com/user-attachments/assets/4f703aff-0689-42c5-85ba-38fa654880b7" />


<img width="575" height="437" alt="Ekran görüntüsü 2025-11-21 013835" src="https://github.com/user-attachments/assets/c2c5ecd0-8a18-4e00-ba67-703b6b4d00d8" />



