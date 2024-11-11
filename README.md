# Tugas 3: Aplikasi Perhitungan Diskon

### Pembuat
- **Nama**: Ferdhyan Dwi Rangga Saputra
- **NPM**: 2210010171

---

## 1. Deskripsi Program
Aplikasi ini memungkinkan pengguna untuk:
- Memasukkan harga asli barang.
- Memilih persentase diskon yang ingin diterapkan.
- Menghitung harga akhir setelah diskon serta jumlah penghematan yang diperoleh.

## 2. Komponen GUI
- **JFrame**: Window utama aplikasi.
- **JPanel**: Panel untuk menampung komponen.
- **JLabel**: Label untuk menunjukkan harga asli, persentase diskon, dan hasil.
- **JTextField**: Input untuk memasukkan harga asli barang.
- **JComboBox**: Dropdown untuk memilih persentase diskon.
- **JButton**: Tombol untuk melakukan perhitungan diskon.

## 3. Logika Program
- Melakukan perhitungan aritmatika untuk menentukan harga akhir dan penghematan berdasarkan persentase diskon yang dipilih.
- Penanganan eksepsi untuk validasi input, memastikan pengguna memasukkan angka untuk harga asli.

## 4. Events
Menggunakan **ActionListener** dan **ItemListener** untuk menangani interaksi pengguna:

### A. Tombol Hitung
Menghitung harga akhir setelah diskon diterapkan dan menampilkan hasil.
```java
private void btnHitungActionPerformed(java.awt.event.ActionEvent evt) {//GEN-FIRST:event_btnHitungActionPerformed
      try {
        // Mengambil nilai dari input pengguna
        double hargaAsli = Double.parseDouble(txtHargaAsli.getText());
        int diskonPersen = sldDiskon.getValue();
        String kuponMasukkan = txtKupon.getText().trim();
        double kuponDiskon = 0;

        // Validasi kode kupon
        if (kuponMasukkan.equalsIgnoreCase("SAVE10")) {
            kuponDiskon = 10; // Diskon tambahan 10%
        } else if (kuponMasukkan.equalsIgnoreCase("SAVE20")) {
            kuponDiskon = 20; // Diskon tambahan 20%
        } else if (!kuponMasukkan.isEmpty()) {
            // Jika kupon tidak valid dan bukan kosong
            JOptionPane.showMessageDialog(this, "Kode kupon tidak valid!");
            return; // Keluar dari metode jika kupon tidak valid
        }

        // Hitung total diskon
        double totalDiskon = hargaAsli * (diskonPersen + kuponDiskon) / 100;
        double hargaAkhir = hargaAsli - totalDiskon;

        // Format hasil
        String hasil = String.format("Harga Asli: %.2f\nDiskon: %d%%\nKupon: %.2f%%\nPenghematan: %.2f\nHarga Akhir: %.2f\n\n",
                hargaAsli, diskonPersen + (int)kuponDiskon, kuponDiskon, totalDiskon, hargaAkhir);

        // Tampilkan hasil di taHistory
        taHistory.append(hasil);
    } catch (NumberFormatException e) {
        JOptionPane.showMessageDialog(this, "Input tidak valid! Pastikan harga asli dan kupon berupa angka.");
    } 
```
### B. ItemListener pada JComboBox
Memilih persentase diskon yang akan diterapkan pada harga asli.
```java
rivate void addComboBoxListener() {
    cbDiskon.addItemListener(new java.awt.event.ItemListener() {
        @Override
        public void itemStateChanged(java.awt.event.ItemEvent evt) {
            if (evt.getStateChange() == java.awt.event.ItemEvent.SELECTED) {
                String selectedDiscount = (String) cbDiskon.getSelectedItem();
                int discountValue = Integer.parseInt(selectedDiscount.replace("%", "")); // Menghapus tanda persen dan mengonversi ke integer
                sldDiskon.setValue(discountValue); // Set nilai slider diskon sesuai pilihan di JComboBox
            }
        }
    });
}
```

## 5. Variasi
Aplikasi ini memiliki variasi tambahan berikut:

### A. Kode Kupon Diskon Tambahan
Menambahkan opsi untuk memasukkan kode kupon diskon tambahan agar pengguna bisa mendapatkan diskon ekstra.
```java
// Validasi kode kupon
        if (kuponMasukkan.equalsIgnoreCase("SAVE10")) {
            kuponDiskon = 10; // Diskon tambahan 10%
        } else if (kuponMasukkan.equalsIgnoreCase("SAVE20")) {
            kuponDiskon = 20; // Diskon tambahan 20%
        } else if (!kuponMasukkan.isEmpty()) {
            // Jika kupon tidak valid dan bukan kosong
            JOptionPane.showMessageDialog(this, "Kode kupon tidak valid!");
            return; // Keluar dari metode jika kupon tidak valid
        }
```
### B. JSlider
Menggunakan **JSlider** sebagai alternatif untuk memilih persentase diskon.
```java
    private void addSliderListener() {
        sldDiskon.addChangeListener(new javax.swing.event.ChangeListener() {
            public void stateChanged(javax.swing.event.ChangeEvent evt) {
                // Hanya jika nilai slider telah diubah (dan tidak sedang diatur)
                JSlider source = (JSlider) evt.getSource();
                if (!source.getValueIsAdjusting()) {
                    int value = source.getValue();
                    cbDiskon.setSelectedItem(value + "%"); // Update JComboBox sesuai dengan nilai slider
                }
            }
        });
    }
```

### C. Riwayat Perhitungan Diskon
Menyediakan riwayat perhitungan diskon yang telah dilakukan untuk membantu pengguna melihat diskon yang sudah diterapkan sebelumnya.
```java
// Tampilkan hasil di taHistory
        taHistory.append(hasil);
    } catch (NumberFormatException e) {
        JOptionPane.showMessageDialog(this, "Input tidak valid! Pastikan harga asli dan kupon berupa angka.");
    }
```
## 6. Tampilan Aplikasi Saat di Run

![image](https://github.com/user-attachments/assets/1d90f146-5197-4369-af91-e88e34e25c04)

## 7. Indikator Penilaian

| No  | Komponen          | Persentase |
| :-: | ------------------ | :--------: |
|  1  | Komponen GUI      |     20%    |
|  2  | Logika Program    |     20%    |
|  3  | Events            |     15%    |
|  4  | Kesesuaian UI     |     15%    |
|  5  | Memenuhi Variasi  |     30%    |
|     | **TOTAL**         |  **100%**  |

--- 
