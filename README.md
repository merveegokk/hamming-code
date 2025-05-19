# hamming-code
import tkinter as tk
from tkinter import messagebox
import random

class HammingSimulator:
    def __init__(self, root):
        self.root = root
        self.root.title("Hamming Kod Simülatörü")

        self.data_bits = tk.StringVar()
        self.code_bits = []
        self.hamming_code = []
        self.memory = []

        # Veri Girişi
        tk.Label(root, text="8/16/32 bitlik veri girin (örnek: 10101010):").pack()
        self.entry = tk.Entry(root, textvariable=self.data_bits, width=40)
        self.entry.pack()

        # Butonlar
        tk.Button(root, text="Hamming Kod Hesapla", command=self.calculate_hamming).pack(pady=5)
        tk.Button(root, text="Hatalı Bit Ekle", command=self.add_error).pack(pady=5)
        tk.Button(root, text="Kontrol Et ve Düzelt", command=self.check_and_correct).pack(pady=5)

        # Bellek kutusu
        tk.Label(root, text="Bellek:").pack()
        self.memory_box = tk.Text(root, height=4, width=50)
        self.memory_box.pack()

        # Sonuç alanı
        tk.Label(root, text="Sonuç:").pack()
        self.result_box = tk.Text(root, height=4, width=50)
        self.result_box.pack()

    def is_power_of_two(self, x):
        return (x != 0) and (x & (x-1) == 0)

    def calculate_hamming(self):
        data = self.data_bits.get().strip()
        if len(data) not in [8, 16, 32] or any(c not in '01' for c in data):
            messagebox.showerror("Hata", "Lütfen 8, 16 veya 32 bitlik sadece 0 ve 1'lerden oluşan veri girin.")
            return

        # Veriyi listeye çevir
        data_bits = list(map(int, data))
        m = len(data_bits)

        # Parite bitlerinin sayısını hesapla
        r = 0
        while 2**r < m + r + 1:
            r += 1

        n = m + r  # Toplam bit sayısı
        hamming = [0] * n

        # Parite bitleri dışındaki yerlere veri bitlerini yerleştir
        j = 0
        for i in range(1, n+1):
            if self.is_power_of_two(i):
                continue
            hamming[i-1] = data_bits[j]
            j += 1

        # Parite bitlerini hesapla
        for i in range(r):
            pos = 2**i
            parity = 0
            for k in range(1, n+1):
                if k & pos == pos:
                    parity ^= hamming[k-1]
            hamming[pos-1] = parity

        self.hamming_code = hamming
        self.memory = hamming.copy()
        self.memory_box.delete('1.0', tk.END)
        self.memory_box.insert(tk.END, ''.join(map(str, self.memory)))
        self.result_box.delete('1.0', tk.END)
        self.result_box.insert(tk.END, f"Hamming kodu hesaplandı ve belleğe kaydedildi.\nKod: {''.join(map(str, hamming))}")

    def add_error(self):
        if not self.memory:
            messagebox.showerror("Hata", "Önce Hamming kodunu hesaplayın.")
            return
        error_pos = random.randint(0, len(self.memory)-1)
        self.memory[error_pos] ^= 1  # Bit'i tersine çevir
        self.memory_box.delete('1.0', tk.END)
        self.memory_box.insert(tk.END, ''.join(map(str, self.memory)))
        self.result_box.delete('1.0', tk.END)
        self.result_box.insert(tk.END, f"Hata eklendi! Bozulan bit pozisyonu: {error_pos+1}")

    def check_and_correct(self):
        if not self.memory:
            messagebox.showerror("Hata", "Önce Hamming kodunu hesaplayın.")
            return

        n = len(self.memory)
        r = 0
        while 2**r < n + 1:
            r += 1

        error_pos = 0
        for i in range(r):
            pos = 2**i
            parity = 0
            for k in range(1, n+1):
                if k & pos == pos:
                    parity ^= self.memory[k-1]
            if parity != 0:
                error_pos += pos

        self.result_box.delete('1.0', tk.END)
        if error_pos == 0:
            self.result_box.insert(tk.END, "Veride hata yok.")
        elif error_pos > n:
            self.result_box.insert(tk.END, "Hata pozisyonu hatalı tespit edildi (pozisyon bellekte yok).")
        else:
            self.result_box.insert(tk.END, f"Hata bulundu! Hatalı bit pozisyonu: {error_pos}\n")
            # Hatalı biti düzelt
            self.memory[error_pos - 1] ^= 1
            self.memory_box.delete('1.0', tk.END)
            self.memory_box.insert(tk.END, ''.join(map(str, self.memory)))
            self.result_box.insert(tk.END, "Hata düzeltildi.")

if __name__ == "__main__":
    root = tk.Tk()
    app = HammingSimulator(root)
    root.mainloop()
