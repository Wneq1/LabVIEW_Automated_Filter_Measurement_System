# LabVIEW_Automated_Filter_Measurement_System

## 📋 Opis projektu
Projekt przedstawia system do zautomatyzowanego pomiaru charakterystyk częstotliwościowych filtrów aktywnych. Sercem układu jest autorska płytka PCB zaprojektowana w programie **KiCad**, zawierająca 6 różnych wariantów filtrów analogowych. System został stworzony z myślą o współpracy z aplikacją pomiarową w środowisku **LabVIEW**, co pozwala na automatyczne wykreślanie charakterystyk amplitodowo-fazowych.

## 🛠️ Architektura Sprzętowa (Hardware)

### 1. Sekcja Filtrów (Topologia Sallen-Key)
Na płytce znajduje się 6 filtrów aktywnych drugiego rzędu (2nd order). Wykorzystanie różnych wartości dobroci ($Q$) pozwala na demonstrację trzech klasycznych aproksymacji:

* **Bufory wejściowe (Wtórniki):** Zapewniają wysoką impedancję wejściową, eliminując wpływ impedancji źródła na parametry filtracji.
* **Filtry Dolnoprzepustowe (LPF) i Górnoprzepustowe (HPF):**
    * **$Q = 0.5$ (Bessel):** Filtr o najlepszej odpowiedzi impulsowej (brak przeregulowań) i liniowej fazie. Idealny do sygnałów prostokątnych i impulsowych.
    * **$Q = 0.707$ (Butterworth):** Filtr o maksymalnie płaskiej charakterystyce amplitudowej w paśmie przepustowym. Stanowi kompromis między szybkością opadania a odpowiedzią czasową.
    * **$Q = 2.0$ (Czebyszew):** Filtr o bardzo stromym zboczu opadania, ale kosztem pojawienia się pofalowań (ripple) i wzmocnienia w okolicy częstotliwości odcięcia.

<img width="840" height="780" alt="image" src="https://github.com/user-attachments/assets/fb7ec75d-9701-4431-a5f4-34ac9d3ae39a" />

Wybór konkretnej charakterystyki odbywa się poprzez przepięcie zworki na selektorze wyjściowym, co pozwala na natychmiastowe porównanie różnic w sygnale na oscyloskopie lub w programie LabVIEW.


### 2. Sekcja Filtrów Górnoprzepustowych (High-Pass)
Sekcja ta służy do tłumienia składowych o niskich częstotliwościach i przepuszczania sygnałów powyżej częstotliwości odcięcia ($f_c$). Zastosowano topologię Sallen-Key 2. rzędu, co pozwala na demonstrację wpływu dobroci ($Q$) na kształt "kolana" charakterystyki:

* **$Q = 0.5$ (Bessel )** 
* **$Q = 0.707$ (Butterworth)**
* **$Q = 2.0$ (Czebyszew)** 
     
<img width="900" height="798" alt="image" src="https://github.com/user-attachments/assets/3ded94e1-a627-43d8-a1bc-855a529c00fa" />

### Porównanie parametrów konstrukcyjnych (HPF)
Wszystkie filtry oparte są na wzmacniaczu **OP07**, a różne typy odpowiedzi uzyskano poprzez precyzyjny dobór elementów biernych (zgodnie ze schematem):
* Kondensatory wejściowe (np. $C_{17}$, $C_{18}$) o wartości $10nF$.
* Rezystory ustalające dobroć (np. $R_{13} = 22k\Omega$, $R_{14} = 11k\Omega$).
### 3. Sekcja Zasilania (Power Supply)
Układ posiada zaawansowany blok zasilania, który umożliwia pracę z sygnałem zmiennym dzięki zasilaniu symetrycznemu:
* **Przetwornica DC-DC:** Użycie modułu **MGJ2D051515SC** pozwala na uzyskanie izolowanego napięcia symetrycznego $\pm 5V$  z pojedynczego wejścia DC.
* **Filtrowanie LC:** Zastosowanie dławika $L_1$ oraz kondensatorów $C_3$, $C_4$ minimalizuje tętnienia napięcia z przetwornicy impulsowej.
* **Zabezpieczenia:** Dioda chroniąca przed odwrotną polaryzacją oraz diody LED sygnalizujące obecność napięcia na szynach dodatniej i ujemnej.
* 
<img width="945" height="292" alt="image" src="https://github.com/user-attachments/assets/316ca8f9-eb68-4fde-949f-09c96520dae3" />


### 4. Schemat całego układu

<img width="1073" height="729" alt="image" src="https://github.com/user-attachments/assets/f32f13ef-76d7-4820-bcf1-dcaea04c1c58" />



## 🎨 Galeria Projektu i Wizualizacja PCB

W tej sekcji przedstawiono fizyczną strukturę projektu oraz finalny wygląd urządzenia po montażu. Projekt został zoptymalizowany pod kątem minimalizacji szumów oraz przejrzystości serwisowej.

### 1. Wizualizacja 3D (Render)
Dzięki narzędziom programu KiCad, wygenerowano realistyczny model 3D płytki **Active Filters Test Board**.
* **Layout:** Komponenty zostały rozmieszczone blokowo, co ułatwia diagnostykę sygnału od wejścia (Input) do wyjścia (Output).
* **Oznaczenia:** Na warstwie opisowej (silkscreen) umieszczono logotypy Politechniki Rzeszowskiej oraz KMiSD, a także czytelne etykiety dla zworek selekcyjnych dobroci $Q$.
* **Montaż:** Wykorzystano mieszaną technologię montażu (SMT dla układów scalonych i rezystorów, THT dla kondensatorów i złączy), co zapewnia kompromis między miniaturyzacją a łatwością modyfikacji.
  
<img width="1010" height="700" alt="image" src="https://github.com/user-attachments/assets/1a221ec9-fb6e-46f1-bde8-7535b701d71a" />

### 2. Widok Warstwy Górnej (Top Layer)
Warstwa górna odpowiada głównie za prowadzenie sygnałów o wysokiej impedancji oraz zasilania wzmacniaczy operacyjnych:
* **Separacja Sygnałów:** Ścieżki sygnałowe są prowadzone w sposób możliwie najkrótszy, aby uniknąć zbierania zakłóceń elektromagnetycznych (EMI).
* **Blok Zasilania:** Wyraźnie wydzielona sekcja z przetwornicą **MGJ2D051515SC** i filtrem LC, która zasila całą płytkę napięciem symetrycznym $\pm 5V$.
* **Pola Masowe:** Wolne przestrzenie zostały wypełnione wylewką masy (Ground Plane), co poprawia stabilność pracy filtrów o wysokiej dobroci $Q=2.0$.
  
<img width="375" height="754" alt="image" src="https://github.com/user-attachments/assets/34ce44f3-3409-4d47-b7bc-0c71e3d9f2ba" />

### 3. Widok Warstwy Dolnej (Bottom Layer)
Warstwa dolna pełni kluczową rolę w zapewnieniu integralności sygnałowej:
* **Ekranowanie:** Ciągła płaszczyzna masy na dolnej warstwie minimalizuje pętle masy i redukuje szumy przenoszone z sekcji zasilania impulsowego do czułych sekcji filtrów analogowych.
* **Przelotki (Vias):** Strategicznie rozmieszczone przelotki zapewniają niską impedancję połączeń między warstwami zasilania.
  
<img width="866" height="806" alt="image" src="https://github.com/user-attachments/assets/e82039ec-ea89-4bfd-a65b-c1c9f220117f" />

## 💻 Integracja z LabVIEW
W przyszłości projekt zostanie rozbudowy o automatyzacjie. Program w LabVIEW będzie obejmował:
1.  Sterowanie generatorem sygnałowym (częstotliwość sweep).
2.  Akwizycję danych przez kartę DAQ lub oscyloskop.
3.  Przetwarzanie danych i wizualizację charakterystyki amplitudowo-częstotliwościowej w czasie rzeczywistym.

## 🗂️ Struktura Repozytorium
* `/KiCad` - Pliki projektu PCB (schemat, layout, biblioteki).
* `/LabVIEW` - Pliki źródłowe programu pomiarowego (.vi).
* `/Documentation` - Dokumentacja techniczna i obliczenia filtrów.

---
*Projekt zrealizowany na Politechnice Rzeszowskiej (Katedra Metrologii i Systemów Diagnostycznych).*










