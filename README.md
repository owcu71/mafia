# Mafia

Przeglądarkowa gra imprezowa inspirowana klasyczną Mafią.

Projekt działa jako prosty frontend bez bundlera i backendu. Cała logika gry znajduje się po stronie klienta.

## Stack

- `index.html`
- `styles.css`
- `app.js`

## Jak uruchomić

Najprościej otworzyć `index.html` w przeglądarce.

Jeśli chcesz uruchamiać projekt przez lokalny serwer, możesz użyć dowolnego prostego static server, np.:

```bash
python3 -m http.server 8080
```

Potem otwórz:

```text
http://localhost:8080
```



## Co już działa

- lobby dla graczy
- dodawanie graczy
- ustawienia partii
- role: obywatel, mafiozo, lekarz, detektyw
- fazy gry: ujawnienie roli, noc, dzień, głosowanie, koniec gry
- podstawowy system kart specjalnych
- ekran kart gracza
- przekazywanie karty po eliminacji
- mobilny układ interfejsu

## Ustawienia gry

Obecnie można zmieniać:

- liczbę mafiozów
- liczbę kart na start
- czas dnia
- czas nocy
- czas głosowania
- włączenie kart
- włączenie lekarza
- włączenie detektywa
- aktywne typy kart

## Aktualny stan projektu

To jest działający prototyp, ale nie finalna wersja gry.

Najważniejsze ograniczenia na teraz:

- gra działa lokalnie, bez synchronizacji między urządzeniami
- część kart specjalnych jest jeszcze tylko przygotowana w UI i danych
- brak backendu, kont graczy i trwałego zapisu

## Struktura plików

- `index.html` - szkielet aplikacji
- `styles.css` - layout i styl UI
- `app.js` - logika gry i renderowanie ekranów

## Plan rozwoju

- wdrożenie efektów kart specjalnych
- dalsze dopracowanie UI i UX
- porządniejsza struktura kodu
- przygotowanie wersji z backendem lub multiplayerem

## Firebase sync (jedno lobby na wiele urządzeń)

Aplikacja ma opcjonalną synchronizację przez **Firebase Realtime Database** (REST, bez SDK).

1. W swoim projekcie Firebase włącz Realtime Database.
2. Na czas testów ustaw reguły read/write dla ścieżki lobby.
3. Przed `app.js` ustaw konfigurację globalną, np. w konsoli lub w `index.html`:

```html
<script>
  window.MAFIA_SYNC = {
    firebaseDbUrl: "https://TWOJ-PROJEKT-default-rtdb.europe-west1.firebasedatabase.app",
    lobbyId: "main"
  };
</script>
```

Po ustawieniu `firebaseDbUrl`, każdy klient pod tym samym `lobbyId` współdzieli stan gry (zegary/fazy/akcje).

