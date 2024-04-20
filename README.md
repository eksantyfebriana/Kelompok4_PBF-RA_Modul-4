# Kelompok4_PBF-RA_Modul-4
# Manajemen Daftar Belanja dengan Scope Parameters as Local Variables
Tugas Praktikum Modul 4 Pemograman Berbasis Fungsi - RA

def TambahBarang(daftar_belanjaan, barang, harga, kuantitas, stok):
    if stok.get(barang, 0) >= kuantitas:
        daftar_belanjaan.append({"barang": barang, "harga": harga, "kuantitas": kuantitas})
        print(f"{kuantitas} {barang} telah ditambahkan ke dalam daftar belanjaan.")
        stok[barang] -= kuantitas  # Update stok barang setelah pembelian
    else:
        print(f"Stok {barang} tidak mencukupi untuk menambahkan ke dalam daftar belanjaan.")

def HitungTotal(daftar_belanjaan):
    total_jumlah = sum(item["kuantitas"] for item in daftar_belanjaan)
    total_harga = sum(item["harga"] * item["kuantitas"] for item in daftar_belanjaan)
    return total_jumlah, total_harga

daftar_belanjaan = []
stok_barang = {"Telur": 10, "Susu": 20, "Roti": 15}

TambahBarang(daftar_belanjaan, "Telur", 2.5, 1, stok_barang)
TambahBarang(daftar_belanjaan, "Susu", 3, 2, stok_barang)
TambahBarang(daftar_belanjaan, "Roti", 1.5, 3, stok_barang)

print("Daftar Belanjaan:")
print("=====================================")
print("| Barang | Harga | Kuantitas | Total |")
print("=====================================")
for item in daftar_belanjaan:
    total = item["harga"] * item["kuantitas"]
    print(f"| {item['barang']:^7} | Rp.{item['harga']:^5.2f} | {item['kuantitas']:^9} | Rp.{total:^5.2f} |")
print("=====================================")

total_jumlah, total_harga = HitungTotal(daftar_belanjaan)
print(f"Total Jumlah Barang: {total_jumlah}")
print(f"Total Harga: Rp.{total_harga}")

print("\nStok Barang:")
print("==================")
print("| Barang |  Stok  |")
print("==================")
for barang, jumlah in stok_barang.items():
    print(f"| {barang:^7} | {jumlah:^6} |")
print("==================")

print("\nStok Barang Setelah Pembelian:")
print("=============================")
print("| Barang |   Stok Setelah   |")
print("|        |    Pembelian     |")
print("=============================")
for barang, jumlah in stok_barang.items():
    stok_setelah_pembelian = jumlah - sum(item["kuantitas"] for item in daftar_belanjaan if item["barang"] == barang)
    print(f"| {barang:^7} | {stok_setelah_pembelian:^16} |")
print("=============================")
