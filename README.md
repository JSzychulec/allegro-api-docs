# Allegro Account Manager

Prywatna aplikacja do zarządzania własnym kontem sprzedażowym Allegro, odrębna od istniejącej integracji z systemem fakturowym.

**[Otwórz pełną dokumentację aplikacji](https://jszychulec.github.io/allegro-api-docs/)**

Dokumentacja opisuje planowane wdrożenie. Uruchomienie funkcji zależy od implementacji, testów i uprawnień przyznanych przez Allegro. Aktualizacja: 18 listopada 2026 r.

## Funkcje

- Odczyt i edycja ofert, cen, stanów magazynowych i ustawień sprzedaży.
- Obsługa zamówień, przesyłek i etykiet.
- Wiadomości, oceny, komentarze i dyskusje.
- Odczyt opłat, historii płatności i własnego profilu.
- Kampanie i programy specjalne oraz afiliacja.
- Zmiany wykonywane po zatwierdzeniu konkretnej operacji przez właściciela.

## Zatwierdzony zakres — 17 uprawnień

- `allegro:api:sale:offers:read`
- `allegro:api:sale:offers:write`
- `allegro:api:sale:settings:read`
- `allegro:api:sale:settings:write`
- `allegro:api:campaigns`
- `allegro:api:orders:read`
- `allegro:api:orders:write`
- `allegro:api:ratings`
- `allegro:api:disputes`
- `allegro:api:billing:read`
- `allegro:api:payments:read`
- `allegro:api:profile:read`
- `allegro:api:messaging`
- `allegro:api:shipments:read`
- `allegro:api:shipments:write`
- `allegro:api:affiliate:read`
- `allegro:api:affiliate:write`

## Wykluczenia

Aplikacja nie będzie żądać ani udostępniać następujących zakresów:

- `allegro:api:profile:write` — zmiana danych osobowych.
- `allegro:api:payments:write` — wykonywanie zwrotów pieniędzy.
- `allegro:api:bids` — składanie ofert kupna w licytacjach.
- `allegro:api:fulfillment:read` i `allegro:api:fulfillment:write` — One Fulfillment.
- `allegro:api:ads` — stare Allegro Ads.

Odczyt istniejących zwrotów w historii płatności pozostaje dostępny. Zakresy afiliacji pozostają w uzgodnionej liście.

## Plan techniczny

Bezstanowy MCP w Node.js na AWS Lambda, endpoint HTTPS przez API Gateway i oddzielne logowanie OAuth dla klientów ChatGPT/Claude. Allegro OAuth Authorization Code flow z PKCE i weryfikacją state. Tokeny przechowywane trwale w szyfrowanej tabeli DynamoDB, sekret aplikacji w Secrets Manager; automatyczne odświeżanie w EventBridge. Role IAM ograniczone do zasobów integracji. Sekrety i dane klientów nie trafiają do publicznego repozytorium ani do logów.

WooCommerce pozostaje na osobnym hostingu.

## Dokumentacja i publikacja

Plik [index.html](index.html) jest publikowany przez GitHub Pages z gałęzi `main` (katalog główny). To stronę GitHub Pages należy podać w formularzu Allegro jako link do dokumentacji.

[Oficjalna dokumentacja Allegro REST API](https://developer.allegro.pl/documentation/)

To narzędzie prywatne; nie jest oficjalną aplikacją Allegro.
