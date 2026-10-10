# Obliczenie wskaźnika NDVI z danych Sentinel-2 w QGIS

Projekt realizowany w ramach zajęć/ćwiczeń z przetwarzania danych teledetekcyjnych z użyciem oprogramowania **QGIS** na systemie Linux (Ubuntu / Linux Mint).

## Opis zadania
Celem ćwiczenia było pobranie danych satelitarnych z platformy Copernicus, zaimportowanie odpowiednich pasm spektralnych do QGIS, a następnie obliczenie i wizualizacja zróżnicowanego wskaźnika wegetacji **NDVI** (Normalized Difference Vegetation Index).

---

## Przebieg realizacji krok po kroku

### 1. Przygotowanie środowiska (Linux)
Przed rozpoczęciem pracy w QGIS upewniono się, że system posiada niezbędne pakiety narzędziowe. Instalacja QGIS oraz wtyczek wspierających język Python przebiegła pomyślnie za pomocą menedżera pakietów `apt`:
```bash
sudo apt update
sudo apt install qgis qgis-plugin-grass
```

### 2. Pobieranie danych (Copernicus Browser)
1. Dokonano rejestracji i logowania w serwisie [Copernicus Browser](https://browser.dataspace.copernicus.eu/).
2. Wyszukano odpowiednią lokalizację oraz dobrano bezchmurny dzień (data: **2026-08-27**).
3. W zakładce *Download* (dane analityczne dla *Sentinel-2 L2A*) wybrano i pobrano pasma:
   * **B04** (Red – pasmo czerwone)
   * **B08** (NIR – bliska podczerwień)
4. Pobierane archiwum ZIP zostało rozpakowane na dysku lokalnym.

### 3. Przetwarzanie w QGIS
1. Wypakowane pliki pasm zaimportowano bezpośrednio do projektu QGIS metodą "przeciągnij i upuść".
2. Uruchomiono **Kalkulator rastera** (*Raster > Raster Calculator*).
3. Wprowadzono standardowy wzór matematyczny dla wskaźnika NDVI:
   $$\text{NDVI} = \frac{\text{NIR} - \text{RED}}{\text{NIR} + \text{RED}}$$
   W środowisku QGIS dla konkretnych warstw wyrażenie przybrało postać:
   ```text
   ( "2026-08-27-00_00_2026-08-27-23_59_Sentinel-2_L1C_B08_(Raw)@1" - "2026-08-27-00_00_2026-08-27-23_59_Sentinel-2_L1C_B04_(Raw)@1" ) / ( "2026-08-27-00_00_2026-08-27-23_59_Sentinel-2_L1C_B08_(Raw)@1" + "2026-08-27-00_00_2026-08-27-23_59_Sentinel-2_L1C_B04_(Raw)@1" )
   ```
4. Zdefiniowano ścieżkę wyjściową pliku rastrowego na dysku (`ndvi.tif`) i wygenerowano warstwę wynikową.


