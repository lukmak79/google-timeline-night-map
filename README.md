# Google Timeline – Mapa Nocnych Punktów i Kempingów 🗺️⛺

> **Autor:** [CampMedia](https://campmedia.pl) | **Wersja:** v1.0  
> **Licencja:** MIT | **Prywatność:** 100% Client-Side (Zero-Knowledge)

Aplikacja webowa typu **Single-File** (jeden plik `index.html`, bez backendu, bez instalacji i bez kompilacji), która z wyeksportowanej historii lokalizacji Google (**Google Timeline / Google Takeout**) wyciąga Twój **nocny punkt** z każdej doby i rysuje go na interaktywnej mapie jako chronologiczną trasę podróży.

Stworzona z myślą o kamperowiczach, podróżnikach, miłośnikach vanlife i globtroterach.

---

## 🔒 100% Prywatności (Wymóg Twardy)

* **Przetwarzanie wyłącznie w Twojej przeglądarce:** Wgrany plik `Timeline.json` jest odczytywany w pamięci RAM urządzenia przez JavaScript (`FileReader`).
* **Żadnych zapytań sieciowych z danymi:** Plik ani koordynaty nie są nigdzie wysyłane.
* **Brak ciasteczek śledzących i baz danych:** Zamknięcie karty usuwa dane z pamięci.
* **Bezpieczeństwo Open Source:** Cały kod jest w 100% jawny i możliwy do audytu (F12 w przeglądarce).

---

## 🧭 Jak aplikacja buduje mapę?

Dla każdej doby w wybranym zakresie dat (np. cały rok) i wybranej strefie czasowej aplikacja ustala, gdzie byłeś o wybranej **godzinie nocnej** (domyślnie `01:00`):

1. **Wizyta (`visit`):** Jeśli w tym czasie trwała zarejestrowana wizyta w miejscu (kemping, hotel, baza), używa jej współrzędnych.
2. **Punkt pomiarowy (`timelinePath`):** Jeśli nie było formalnej wizyty, szuka najbliższego rzeczywistego odczytu GPS z telefonu w oknie tolerancji (domyślnie ± 60 min).
3. **Reguła nocnej ciągłości (Wieczór – Rano):** Rozwiązuje problem uśpienia telefonu (tryb Doze w Androidzie/iOS): jeśli ostatni punkt wieczorem i pierwszy rano wskazują to samo miejsce (<= 250 m), aplikacja uzupełnia nocny punkt jako pewny nocleg.
4. **Grupowanie kempingów i baz:** Kolejne noce spędzone w tym samym miejscu (w promieniu suwaka, np. 350 m) są łączone w jeden czytelny marker z licznikiem nocy i zakresem dat.
5. **Obsługa wielokrotnych powrotów:** Jeśli wracasz w to samo miejsce w różnych miesiącach (np. dom lub ulubiony kemping), markery układają się obok siebie (mikro-offset), dzięki czemu wcześniejsze pobyty nie są zasłaniane przez późniejsze!

---

## ✨ Kluczowe Funkcje

* **Obsługa wszystkich formatów Google:**
  * Nowy format z telefonu (Android/iOS): `Timeline.json` (obiekty `semanticSegments`, `timelinePath`, `userLocationProfile`).
  * Klasyczny Google Takeout: `Records.json` (format współrzędnych E7).
  * Miesięczne pliki Takeout: `Semantic Location History` (katalogi z plikami typu `2024_JANUARY.json`).
* **Interaktywna mapa (Leaflet + Darmowe kafelki Esri / OSM):**
  * Działa od razu – **nie wymaga żadnych kluczy API** (brak limitów Google Maps API).
  * Wybór podkładów: Esri Ulice, Esri Topo, Esri Ciemna (Dark Gray), Esri Jasna oraz OSM Humanitarian.
  * Gradient kolorów odpowiadający porom roku (od zimy do jesieni).
* **Zakładka „⛺ Miejscówki / Kempingi”:**
  * Lista unikalnych baz noclegowych posortowana wg liczby nocy.
  * Narzędzie dociągania nazw kempingów z bazy **OpenStreetMap (OSM)**.
  * Możliwość własnej edycji nazw (ikonka ✏️) zapamiętywanej lokalnie.
* **Oś czasu i animacja podróży:**
  * Suwak chronologiczny ze skokami dzień po dniu.
  * Przycisk `▶ Odtwórz rok` z regulacją prędkości (od 0.5x do 5x).
* **Statystyki wyprawowe:**
  * Liczba nocy z danymi i pokrycie procentowe.
  * Liczba unikalnych baz i kempingów.
  * Łączny dystans przebyty w linii prostej między kolejnymi nocami.
  * Najdłuższy skok noc-w-noc oraz główna baza całoroczna.
* **Eksport danych:**
  * **CSV** (z polskimi znakami i kodowaniem UTF-8 BOM).
  * **GPX** (trasa gotowa do wgrania do Garmin / Locus / OsmAnd).
  * **GeoJSON** (do QGIS lub narzędzi GIS).
  * **PNG** (zrzut mapy z trasą wygenerowany w przeglądarce).
* **Tryb jasny / ciemny (Dark Mode)** oraz pełna responsywność (telefon, tablet, komputer).

---

## 🚀 Jak uruchomić?

Aplikacja nie wymaga instalacji Node.js, serwera ani kompilacji.

1. Pobierz repozytorium lub sam plik `index.html`.
2. Kliknij dwukrotnie w plik `index.html`, aby otworzyć go w dowolnej przeglądarce (Chrome, Edge, Firefox, Safari).
3. Kliknij **„Wgraj Timeline.json”** lub przeciągnij plik na okno przeglądarki.

### Publikacja na GitHub Pages (w 1 minutę):
1. Utwórz nowe repozytorium na GitHubie i wypchnij plik `index.html`.
2. Wejdź w **Settings** $\rightarrow$ **Pages**.
3. W sekcji *Branch* wybierz `main` i kliknij **Save**.
4. Twoja strona będzie natychmiast dostępna pod adresem: `https://<twoj-login>.github.io/<nazwa-repo>/`.

---

## 📱 Jak pobrać plik Timeline.json z telefonu?

1. Otwórz aplikację **Mapy Google** na telefonie.
2. Dotknij swojego zdjęcia profilowego w prawym górnym rogu i wybierz **„Twoja oś czasu”** (Timeline).
3. Dotknij trzech kropek (**⋮**) w prawym górnym rogu $\rightarrow$ **„Ustawienia i prywatność”**.
4. Zjedź na sam dół do sekcji *Ustawienia lokalizacji* i kliknij **„Eksportuj dane z Osi czasu”**.
5. Zapisz plik `Timeline.json` i wgraj go do aplikacji!

