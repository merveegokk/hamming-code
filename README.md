# Hamming Kod Simülatörü

Bu proje, 8, 16 veya 32 bitlik veri için Hamming kodu hesaplayan, belleğe kaydeden, yapay hata ekleyebilen ve hatayı bulup düzeltebilen basit bir görsel arayüz uygulamasıdır.

## Özellikler

- 8/16/32 bitlik veri girişini kabul eder.
- Hamming kodunu hesaplar ve belleğe kaydeder.
- Bellekteki koda rastgele veya belirli pozisyonda 1 bitlik hata ekler.
- Hatalı biti sendrom kelimesi yardımıyla bulur ve düzeltir.
- Kullanıcı dostu Tkinter tabanlı grafik arayüz.
- Hata ekleme ve düzeltme işlemleri adım adım takip edilebilir.

## Kullanım

1. Veri giriş kutusuna 8, 16 veya 32 bitlik bir ikili sayı girin (örnek: `10101010`).
2. **Hamming Kod Hesapla** butonuna basarak Hamming kodunu hesaplayın ve belleğe kaydedin.
3. **Hatalı Bit Ekle** butonuyla bellekte rastgele bir biti bozabilirsiniz.
4. **Kontrol Et ve Düzelt** butonuna basarak hatayı tespit edip düzeltebilirsiniz.
5. Bellekteki kod ve sonuçlar alt kısımdaki metin kutularında görüntülenir.

![Ekran görüntüsü 2025-05-19 151619](https://github.com/user-attachments/assets/89c90f47-629b-4047-a1e2-be2fcaf53448)

![Ekran görüntüsü2 2025-05-19 151658](https://github.com/user-attachments/assets/2a6f6c84-5600-4dc6-a9ab-2e87f56c9c63)

![Ekran görüntüsü3 2025-05-19 151737](https://github.com/user-attachments/assets/5cbaf45a-ae2f-4d6b-9adc-8182553f64b1)


## Gereksinimler

- Python 3.x
- Tkinter (Python ile birlikte gelir)

## Çalıştırma


```bash
python hamming_simulator.py
