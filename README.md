# LabVIEW_Automated_Filter_Measurement_System
# LabVIEW Automated Filter Measurement System

## 📋 Opis projektu
Projekt przedstawia system do zautomatyzowanego pomiaru charakterystyk częstotliwościowych filtrów aktywnych. Sercem układu jest autorska płytka PCB zaprojektowana w programie **KiCad**, zawierająca 6 różnych wariantów filtrów analogowych. System został stworzony z myślą o współpracy z aplikacją pomiarową w środowisku **LabVIEW**, co pozwala na automatyczne wykreślanie wykresów Bodego.

## 🛠️ Architektura Sprzętowa (Hardware)

### 1. Sekcja Filtrów (Topologia Sallen-Key)
Na płytce znajduje się 6 filtrów aktywnych drugiego rzędu (2nd order) opartych na precyzyjnych wzmacniaczach operacyjnych **OP07**. 



Struktura układu obejmuje:
* **Bufory wejściowe (Wtórniki):** Zapewniają wysoką impedancję wejściową i separację sygnału.
* **Filtry Dolnoprzepustowe (Low-Pass):** Trzy układy o różnych współczynnikach dobroci:
    * $Q = 0.5$
    * $Q = 0.707$ (Butterworth)
    * $Q = 2.0$
* **Filtry Górnoprzepustowe (High-Pass):** Trzy układy o analogicznych wartościach dobroci:
    * $Q = 0.5$ / $Q = 0.707$ / $Q = 2.0$

Wybór konkretnego filtra odbywa się za pomocą zintegrowanych zworek (selekcja wyjścia).

### 2. Sekcja Zasilania (Power Supply)
Układ posiada zaawansowany blok zasilania, który umożliwia pracę z sygnałem zmiennym dzięki zasilaniu symetrycznemu:
* **Przetwornica DC-DC:** Użycie modułu **MGJ2D051515SC** pozwala na uzyskanie izolowanego napięcia symetrycznego $\pm 5V$ (lub $\pm 15V$ zależnie od wersji) z pojedynczego wejścia 5V.
* **Filtrowanie LC:** Zastosowanie dławika $L_1$ oraz kondensatorów $C_3$, $C_4$ minimalizuje tętnienia napięcia z przetwornicy impulsowej.
* **Zabezpieczenia:** Dioda chroniąca przed odwrotną polaryzacją oraz diody LED sygnalizujące obecność napięcia na szynach dodatniej i ujemnej.

## 💻 Integracja z LabVIEW
Projekt został zaprojektowany pod kątem automatyzacji. Program w LabVIEW realizuje:
1.  Sterowanie generatorem sygnałowym (częstotliwość sweep).
2.  Akwizycję danych przez kartę DAQ lub oscyloskop.
3.  Przetwarzanie danych i wizualizację charakterystyki amplitudowo-częstotliwościowej w czasie rzeczywistym.

## 🗂️ Struktura Repozytorium
* `/KiCad` - Pliki projektu PCB (schemat, layout, biblioteki).
* `/LabVIEW` - Pliki źródłowe programu pomiarowego (.vi).
* `/Documentation` - Dokumentacja techniczna i obliczenia filtrów.

---
*Projekt zrealizowany na Politechnice Rzeszowskiej (Katedra Metrologii i Systemów Diagnostycznych).*

<img width="945" height="292" alt="image" src="https://github.com/user-attachments/assets/316ca8f9-eb68-4fde-949f-09c96520dae3" />

<img width="840" height="780" alt="image" src="https://github.com/user-attachments/assets/fb7ec75d-9701-4431-a5f4-34ac9d3ae39a" />

<img width="900" height="798" alt="image" src="https://github.com/user-attachments/assets/3ded94e1-a627-43d8-a1bc-855a529c00fa" />

<img width="1073" height="729" alt="image" src="https://github.com/user-attachments/assets/f32f13ef-76d7-4820-bcf1-dcaea04c1c58" />

<img width="375" height="754" alt="image" src="https://github.com/user-attachments/assets/34ce44f3-3409-4d47-b7bc-0c71e3d9f2ba" />

<img width="1010" height="700" alt="image" src="https://github.com/user-attachments/assets/1a221ec9-fb6e-46f1-bde8-7535b701d71a" />

<img width="866" height="806" alt="image" src="https://github.com/user-attachments/assets/e82039ec-ea89-4bfd-a65b-c1c9f220117f" />
