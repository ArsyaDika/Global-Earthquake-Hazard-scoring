# Global Earthquake Hazard Scoring

Where should planners worry most? This project turns a global record of significant earthquakes into a simple, transparent hazard score, so that the zones that deserve attention first are easy to see and easy to explain.

## How the score works

1. Load the Significant Earthquakes dataset (Kaggle) and convert each event to a point (EPSG:4326).
2. Reproject to EPSG:3857 and draw a **100 km hazard buffer** around every event.
3. Intersect the buffers, which gives 112,185 records in the notebook run.
4. Classify each event on three factors and add up the points (low = 1, medium = 2, high = 3):

| Factor | High (3) | Medium (2) | Low (1) |
|---|---|---|---|
| Magnitude | 6 or more | 5 to 5.9 | below 5 |
| Depth (shallow is more dangerous) | 70 km or less | 71 to 300 km | deeper than 300 km |
| Frequency (events recorded for the same place) | 50 or more | 20 to 49 | fewer than 20 |

5. Convert the total score (3 to 9) into a hazard class: **Low** (4 or less), **Medium** (5 to 6), **High** (7 to 9).
6. Plot the class distributions and export the result as GeoJSON.

## Files

- `Task Day 6.ipynb`: the full workflow, from loading data to export.
- `significant-earthquakes-metadata.json`: metadata of the source dataset.

## Run it yourself

Requires Python with `pandas`, `geopandas`, `shapely` and `matplotlib`. Download `Significant_Earthquakes.csv` from Kaggle, then save it as `data/Significant_Earthquakes.csv`, which is the path the notebook reads. The dataset is not included in this repository.

## Limitations

Frequency is counted per place name, so it reflects how often an event was recorded there and not a physical recurrence rate. Classes use fixed thresholds and equal weights, which makes the score easy to read but is a simplification of real seismic hazard.

------------------

# Penilaian Bahaya Gempa Global

Di mana perencana perlu paling waspada? Proyek ini mengubah catatan global gempa signifikan menjadi skor bahaya yang sederhana dan transparan, sehingga zona yang perlu diperhatikan lebih dulu mudah dilihat dan mudah dijelaskan.

## Cara kerja skor

1. Muat dataset Significant Earthquakes (Kaggle) dan ubah setiap kejadian menjadi titik (EPSG:4326).
2. Proyeksikan ke EPSG:3857 dan buat **buffer bahaya 100 km** di sekeliling setiap kejadian.
3. Lakukan intersect pada buffer, yang menghasilkan 112.185 rekaman pada proses di notebook.
4. Klasifikasikan setiap kejadian berdasarkan tiga faktor lalu jumlahkan poinnya (rendah = 1, sedang = 2, tinggi = 3):

| Faktor | Tinggi (3) | Sedang (2) | Rendah (1) |
|---|---|---|---|
| Magnitudo | 6 atau lebih | 5 sampai 5,9 | di bawah 5 |
| Kedalaman (dangkal lebih berbahaya) | 70 km atau kurang | 71 sampai 300 km | lebih dalam dari 300 km |
| Frekuensi (jumlah kejadian tercatat di tempat yang sama) | 50 atau lebih | 20 sampai 49 | kurang dari 20 |

5. Ubah total skor (3 sampai 9) menjadi kelas bahaya: **Rendah** (4 ke bawah), **Sedang** (5 sampai 6), **Tinggi** (7 sampai 9).
6. Tampilkan distribusi kelas dan ekspor hasilnya sebagai GeoJSON.

## Berkas

- `Task Day 6.ipynb`: alur kerja lengkap, dari memuat data sampai ekspor.
- `significant-earthquakes-metadata.json`: metadata dataset sumber.

## Menjalankan sendiri

Membutuhkan Python dengan `pandas`, `geopandas`, `shapely`, dan `matplotlib`. Unduh `Significant_Earthquakes.csv` dari Kaggle, lalu simpan sebagai `data/Significant_Earthquakes.csv`, yaitu path yang dibaca notebook. Dataset tidak disertakan di repositori ini.

## Keterbatasan

Frekuensi dihitung per nama tempat, jadi menggambarkan seberapa sering kejadian tercatat di sana dan bukan laju pengulangan fisik. Kelas memakai ambang tetap dan bobot yang sama, sehingga skor mudah dibaca tetapi merupakan penyederhanaan dari bahaya seismik yang sebenarnya.
