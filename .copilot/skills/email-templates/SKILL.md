# Email Templates Skill

## Cel
Skill wspiera projektowanie, implementowanie i testowanie szablonów emaili dla projektu Mailer. Obejmuje zarówno template inheritance, jak i podstawową obsługę zmiennych, dzięki czemu ten sam system może generować wiadomości HTML i plain text bez duplikowania logiki.

## Kontekst Projektu
- Projekt: Mailer
- Obszar: wiadomości transakcyjne i marketingowe
- Technologie: Flask templates, Python, pytest
- Założenie: szablon ma być czytelny, prosty w utrzymaniu i łatwy do testowania

## Template Inheritance
Stosuj dziedziczenie szablonów, aby wspólne elementy, takie jak nagłówek, stopka i układ, nie były powielane w wielu plikach. Bazowy layout powinien zawierać wspólną strukturę HTML, a szablony potomne powinny wypełniać bloki przeznaczone na treść właściwą dla konkretnego typu wiadomości.

Przykład założenia:
- `base_email.html` zawiera nagłówek, stopkę i styl bazowy.
- `welcome_email.html` rozszerza layout i wstawia sekcję powitalną.
- `newsletter_email.html` używa tego samego układu, ale renderuje listę artykułów.

## Variable Substitution
Szablony powinny korzystać z podstawowej substytucji zmiennych, takich jak `recipient_name`, `unsubscribe_url`, `confirmation_link`, `subject` i `preview_text`. Zmiennych nie należy sklejać ręcznie w Pythonie, jeśli można je przekazać do renderera. Dzięki temu logika prezentacji pozostaje w szablonie, a warstwa aplikacji odpowiada tylko za dostarczenie danych.

Zasady:
- wymagane dane przekazuj jawnie,
- wartości opcjonalne obsługuj bez błędów renderowania,
- dla brakujących pól stosuj sensowne fallbacki,
- unikaj logiki biznesowej w HTML.

## HTML and Plain Text Templates
Każda ważna wiadomość powinna mieć wersję HTML i plain text. HTML może zawierać styl, sekcje i CTA, natomiast wersja plain text ma być możliwa do odczytania w każdym kliencie pocztowym. Obie wersje muszą przekazywać ten sam sens i tę samą treść biznesową.

W praktyce oznacza to:
- oddzielne pliki dla HTML i tekstu,
- spójny subject line,
- ten sam zestaw danych wejściowych,
- brak zależności od JavaScript.

## Template Testing
Szablony należy testować na trzech poziomach. Pierwszy poziom to sprawdzenie, czy renderer przyjmuje poprawne dane i zwraca poprawny string. Drugi to weryfikacja, czy konkretne wartości pojawiają się w wygenerowanym HTML. Trzeci to testy regresji, które potwierdzają, że istotne elementy, takie jak linki, przyciski i sekcje specjalne, nie znikają po zmianach.

Przykładowe asercje:
- render zawiera nazwę odbiorcy,
- link potwierdzający jest obecny,
- newsletter wyświetla listę pozycji,
- brak danych nie powoduje wyjątku.

## Examples

### Welcome
Szablon powitalny powinien krótkim wstępem informować użytkownika, że zapis został potwierdzony, a następnie kierować go do kolejnego kroku. Dobry przykład to wiadomość z imieniem odbiorcy, prostym CTA i lekkim tonem komunikacji.

### Confirmation
Szablon potwierdzenia powinien zawierać wyraźny link akcji oraz alternatywny tekst na wypadek problemów z kliknięciem. Wersja plain text musi zawierać sam adres URL i krótką instrukcję.

### Newsletter
Szablon newslettera powinien pozwalać na listę wielu elementów: tytuł, opis, link, meta dane i ewentualny obrazek. Dla czytelności warto wydzielić sekcję powtarzalną i renderować ją iteracyjnie.

## Reguły
- Używaj dziedziczenia szablonów zamiast kopiowania markup.
- Testuj zarówno HTML, jak i plain text.
- Trzymaj logikę prezentacji w szablonach, a nie w kodzie Pythona.
- Zapewnij fallbacki dla opcjonalnych zmiennych.
- Utrzymuj szablony proste, czytelne i zgodne z responsywnym email design.
