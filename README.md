# Proyek Capstone: Klasifikasi Kalimat Sentimen dengan IBM Granite

## Judul Proyek  
**Klasifikasi Sentimen dan Area Fokus dari Kalimat Sentimen Menggunakan IBM Granite (granite-3.3-8b-instruct)**

## Ringkasan Proyek 
Proyek ini bertujuan untuk membangun sistem klasifikasi sentimen berbasis kecerdasan buatan (AI) dengan menggunakan model bahasa besar (Large Language Model / LLM) dari IBM, yaitu Granite 3.3-8b-instruct. Sistem ini dirancang untuk mengelompokkan kalimat ke dalam tiga kategori sentimen utama: Positif, Negatif, dan Netral. Selain klasifikasi, sistem juga mengekstrak area fokus utama dari setiap kalimat, seperti: kualitas produk, layanan, harga, cuaca, atau aspek kehidupan sehari-hari.

Dataset yang digunakan adalah jbeno/sentiment_merged yang bersumber dari platform Hugging Face. Dataset ini berisi berbagai kalimat ulasan atau pernyataan dalam konteks umum maupun pengalaman pengguna. Data ini tidak spesifik terhadap satu domain (misalnya e-commerce), sehingga model dituntut untuk bekerja secara general dan kontekstual.

Proyek ini menggunakan pendekatan few-shot prompting, yaitu dengan memberikan beberapa contoh kalimat dan label sebagai referensi di dalam prompt. Teknik ini memandu model untuk mengenali pola klasifikasi yang diharapkan, tanpa melakukan pelatihan ulang pada dataset tertentu (tanpa fine-tuning). Model Granite diakses melalui Replicate API dan diintegrasikan ke dalam pipeline Python menggunakan Langchain.

Eksperimen dilakukan dalam dua pendekatan:
- Prompt Default: instruksi dasar tanpa struktur atau penekanan emosional
- Prompt Refined: instruksi disempurnakan dengan format tetap, penekanan interpretasi emosional implisit, dan contoh referensi

Model diuji terhadap 20 data ulasan kemudian diuji lagi terhadap 50 data ulasan, dan hasil klasifikasinya dibandingkan dengan label aktual. Evaluasi dilakukan berdasarkan akurasi serta kualitas penjelasan yang dihasilkan oleh AI.

Hasil evaluasi menunjukkan bahwa:
- Default Prompt menghasilkan akurasi sebesar 60%
- Refined Prompt menghasilkan akurasi sebesar 84%
- Refined prompt juga menghasilkan output yang lebih konsisten, lengkap (dengan focus area), dan mudah dianalisis

## Link dari Dataset yang Digunakan
- **Nama**: `jbeno/sentiment_merged`
- **Sumber**: [Hugging Face Dataset](https://huggingface.co/datasets/jbeno/sentiment_merged)
- **Jumlah data**: ±100.000 baris
- **Fitur utama**: `sentence` (teks ulasan), `label` (0 = Negative, 1 = Neutral, 2 = Positive)

## Output Akurasi
Awalnya model diuji terhadap 20 data, kemudian diperluas menjadi 50 data untuk evaluasi yang lebih representatif. Akurasi akhir yang dijadikan acuan adalah hasil dari pengujian 50 data.
### Hasil Klasifikasi Default   
- Total Prediksi: 20  
- Benar: 15  
- **Akurasi**: 75.00%
### Hasil Klasifikasi Refined
- Total Prediksi: 20  
- Benar: 18  
- **Akurasi**: 90.00%
Setelah dilakukan pengujian 20 kali, dilakukan pengujian 50 kali.
### Hasil Klasifikasi Default   
- Total Prediksi: 50  
- Benar: 30  
- **Akurasi**: 60.00%
### Hasil Klasifikasi Refined
- Total Prediksi: 50  
- Benar: 36  
- **Akurasi**: 84.00%

## Insight & Findings
- Model default sudah cukup akurat, tetapi belum optimal dalam mendeteksi sentimen netral.
- Dengan refinement (top_k, top_p, max_tokens, repetition_penalty), hasil lebih seimbang dan akurat.
- Penambahan struktur prompt memberi output yang lebih jelas dan bernilai analitis.

## Penjelasan AI Support
Dalam proyek ini, AI yang digunakan adalah model IBM Granite 3.3-8b-instruct, yaitu model Large Language Model (LLM) dari IBM yang dirancang untuk merespons instruksi secara natural dan kontekstual.
AI ini digunakan untuk mengklasifikasikan sentimen dari kalimat-kalimat dalam dataset (positif, negatif, atau netral), serta mengidentifikasi area fokus utama seperti kualitas produk, harga, layanan, atau topik kehidupan sehari-hari.
Dataset yang digunakan diambil dari Hugging Face dan diproses menggunakan Python. Model Granite dihubungkan melalui platform Replicate menggunakan API Key pribadi, dan diintegrasikan ke dalam proyek dengan bantuan library Langchain.
Proses kerjanya adalah: setiap kalimat dikirim ke model Granite dalam bentuk prompt instruksional. AI kemudian mengembalikan hasil klasifikasi lengkap dengan label sentimen, area fokus (jika ada), dan penjelasan logis berdasarkan makna kalimat. 
**Contoh output refined:**
```
Actual: Neutral | Predicted: Positive | Focus: Service/Support
Explanation: Sentiment: Positive
Focus Area: Service/Support
Explanation: The sentence expresses a positive sentiment by highlighting the visibility and presence of helpers behind the scenes, implying a supportive and attentive service. This statement suggests appreciation for the effort and work done, which is not possible without a positive focus on the service or support aspect.
```

Dengan adanya output berisi penjelasan dari AI maka akan sangat membantu untuk memahami alasan prediksi — bukan hanya hasil akhirnya.

## Rekomendasi
1. Gunakan **prompt yang terstruktur** agar output konsisten dan mudah dianalisis.
2. Selalu lakukan evaluasi antara model default dan refined.
3. Untuk ulasan/kalimat pendek, prioritaskan **ekstraksi informasi** (sentimen + fokus area utama), bukan hanya hasil prediksi dari kalimat sentimennya seperti hanya(positive/negative/neutral).
4. Gunakan hasil klasifikasi untuk visualisasi, dashboard, atau pelaporan bisnis.
## Kesimpulan
Proyek ini menunjukkan bahwa dengan pendekatan prompt engineering yang tepat, model AI seperti IBM Granite dapat menghasilkan klasifikasi sentimen yang cukup akurat tanpa perlu pelatihan ulang. Penggunaan prompt refined terbukti meningkatkan akurasi sekaligus memberikan nilai tambah berupa interpretasi dan area fokus, yang berguna untuk aplikasi nyata seperti analisis opini pelanggan, pelaporan layanan, atau pemetaan persepsi publik.

## Tools yang Digunakan
- Python (Google Colab)
- Langchain + Replicate
- Hugging Face Datasets
- Matplotlib (untuk visualisasi opsional)
