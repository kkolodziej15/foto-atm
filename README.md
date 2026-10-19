# Foto ATM

Aplikacja na telefon do dokumentacji fotograficznej bankomatów. Wgrywasz listę z Excela, robisz zdjęcia przy każdej pozycji, a aplikacja sama nazywa pliki numerem bankomatu. Na koniec eksportujesz wszystko do ZIP.

Działa w przeglądarce jako aplikacja instalowana na ekranie głównym (Android i iPhone), także bez internetu. Nie ma serwera, kont ani bazy danych. Zdjęcia i listy zostają na Twoim telefonie.

**Adres aplikacji:** `https://kkolodziej15.github.io/foto-atm/`

## Instalacja na telefonie

**Android (Chrome):** otwórz adres. Pojawi się pasek „Zainstaluj”. Jeśli go nie ma, wybierz z menu ⋮ „Zainstaluj aplikację”.

**iPhone / iPad (Safari, nie Chrome):** otwórz adres, dotknij „Udostępnij”, potem „Do ekranu początkowego”. Pracuj później tylko z ikony na ekranie początkowym, bo Safari i zainstalowana aplikacja mają osobną pamięć na zdjęcia.

Po instalacji otwórz aplikację raz z internetem. W Ustawieniach powinien pojawić się napis „Tryb offline: gotowy”. Od tej chwili możesz pracować bez zasięgu.

## Jak używać

1. **Lista.** Dotknij „Pobierz wzór Excela”, uzupełnij go i wgraj przyciskiem „Importuj Excel”. Wskaż kolumnę z numerem bankomatu i, jeśli chcesz, kolumny z adresem.
2. **Zdjęcia.** Wejdź w pozycję i dotknij „Zrób zdjęcie”. Zdjęć może być tyle, ile trzeba.
3. **Uszkodzenia.** Włącz „Uszkodzenie”, wybierz rodzaj i zrób zdjęcie. Rodzaje możesz zmienić w Ustawieniach.
4. **Kopia.** Po pracy dotknij „Eksport ZIP”. Na Androidzie paczki trafiają do „Pobrane”. Na iPhonie dotknij „Zapisz paczkę”, potem „Zachowaj w Plikach”.

Zdjęcia są tylko na telefonie. Usunięcie aplikacji lub wyczyszczenie danych przeglądarki kasuje je, dlatego rób eksport po każdym dniu pracy.

## Nazwy plików

- zwykłe zdjęcie: `ATM-0001_01.jpg`, `ATM-0001_02.jpg`, …
- uszkodzenie: `ATM-0001_03_USZ2-1.jpg` (rodzaj uszkodzenia nr 2, pierwsze takie zdjęcie w pozycji)
- znaki niedozwolone w nazwach plików i spacje zamieniane są na `-`, np. `ATM/0004` → `ATM-0004`
- po usunięciu zdjęcia numeracja przelicza się sama

W paczce ZIP jest też `manifest.csv`: tabela do otwarcia w Excelu z nazwami plików, datami i rodzajami uszkodzeń.

## Wdrożenie

Wszystkie pliki są statyczne, więc wystarczy dowolny hosting z HTTPS. Bez HTTPS nie działa instalacja ani tryb offline.

**GitHub Pages:** wgraj zawartość tego folderu do repozytorium (`index.html` w korzeniu), potem Settings → Pages → Branch `main`, folder `/ (root)`.

**Zwykły hosting (np. Hostinger):** wgraj pliki do `public_html` strony albo subdomeny i włącz SSL. Plik `.htaccess` wymusza HTTPS i pilnuje, żeby telefony dostawały aktualizacje.

### Aktualizacje

Po każdej zmianie plików zmień wersję cache w `sw.js` (`atm-foto-v3` → `atm-foto-v4`). Telefony pokażą wtedy pasek „Dostępna nowa wersja”, a po dotknięciu „Odśwież” wczytają nową.

## Pliki

| Plik | Do czego |
| --- | --- |
| `index.html` | cała aplikacja |
| `sw.js` | praca offline i aktualizacje |
| `manifest.webmanifest`, `icon-*.png`, `apple-touch-icon.png` | instalacja na ekranie głównym |
| `.htaccess` | ustawienia serwera Apache (nie dotyczy GitHub Pages) |
| `lib/xlsx.full.min.js` | SheetJS 0.18.5, odczyt i zapis Excela |
| `lib/jszip.min.js` | JSZip 3.10.1, tworzenie paczek ZIP |

## Test lokalny

```
python3 -m http.server 8765
```

Uruchom w tym folderze i otwórz http://localhost:8765 w Chrome.
