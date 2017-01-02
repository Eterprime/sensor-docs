# Konfiguracja metod

- [Podstawowe informacje](#introdution)
- [Wysłanie wiadomości prywatnej](#private-message)
  - [Dostępne zmienne](#private-message-vars)
- [Wysłanie zaczepki](#poke)
  - [Dostępne zmienne](#poke-vars)
  - [Ważna uwaga](#poke-info)
- [Zapis zdarzeń na kanale](#channel-log)
  - [Dostępne zmienne](#channel-log-vars)
- [Powiadomienie użytkowników](#group-message)
  - [Dostępne zmienne](#group-message-vars)
- [Wykonanie polecenia systemowego](#shell-command)
  - [Dostępne zmienne](#shell-command-vars)
- [Wyrzucenie z serwera](#kick)
- [Blokada dostępu do serwera](#ban)

<a name="introdution"></a>
## Podstawowe informacje

Metodą nazywamy czynność stosowaną przez program na użytkowniku, który został oznaczony jako wykorzystujący niedozwolone oprogramowanie do maskowania prawdziwego adresu IP. Wszystkie metody są wykonywane w odpowiedniej hierarchii i mogą być aktywne jednocześnie.

```ini
; W tym miejscu możesz włączyć lub wyłączyć tą metodę.
; true - włączone / false - wyłączona
; @default false
enabled = false
```

Opcja dostępna dla każdej metody pozwala zdecydować o jej statusie podczas działania aplikacji. Należy również pamiętać, że do poprawnego uruchomienia programu wymagana jest aktywna przynajmniej jedna metoda.

<a name="private-message"></a>
## Wysłanie wiadomości prywatnej

```ini
; Metoda "message" umożliwia wysłanie wiadomości prywatnej do użytkownika
; który został oznaczony przez aplikację jako posiadający VPN.
[method:message]
```

Kiedy wysyłanie wiadomości prywatnej jest aktywne, zaraz po pomyślnej detekcji, użytkownik otrzyma od programu powiadomienie.

```ini
; Wiadomość wysyłana do użytkownika.
; Można używać zmiennych:
;  %client.ip    -> zawiera numeryczny adres IP użytkownika
;  %client.name  -> zawiera aktualną nazwę użytkownika
;  %client.uid   -> zawiera unikalny identyfikator użytkownika
;  %client.dbid  -> zawiera database ID użytkownika
;  %client.link  -> odnośnik do użytkownika
;  %channel.link -> odnośnik do kanału na którym przebywa użytkownik
message = "Zostałeś oznaczony jako użytkownik VPN, wyłącz tą aplikację ponieważ maskowanie adresu IP jest niezgodne z regulaminem."
```

<a name="private-message-vars"></a>
### Dostępne zmienne

- `%client.ip` — Zawiera adres IPv4 użytkownika
- `%client.name` — Zawiera nazwę użytkownika
- `%client.uid ` — Zawiera unikalny identyfikator użytkownika
- `%client.dbid` — Zawiera identyfikator z bazy danych użytkownika
- `%client.link` — Zawiera odnośnik do użytkownika
- `%channel.link` — Zawiera odnośnik do kanału, na którym przebywa użytkownik

<a name="poke"></a>
## Wysłanie zaczepki

```ini
; Metoda "poke" wysyła do oznaczonych użytkowników wiadomości
; poke z ustaloną informacją.
[method:poke]
```

Podobnie jak w wiadomości prywatnej, włączenie tej metody spowoduje wysłanie wiadomości za pośrednictwem "poke" do niezaufanego użytkownika.

```ini
; Wiadomość wysyłana do użytkownika.
; Można używać zmiennych:
;  %client.ip    -> zawiera numeryczny adres IP użytkownika
;  %client.name  -> zawiera aktualną nazwę użytkownika
;  %client.uid   -> zawiera unikalny identyfikator użytkownika
;  %client.dbid  -> zawiera database ID użytkownika
;  %client.link  -> odnośnik do użytkownika
;  %channel.link -> odnośnik do kanału na którym przebywa użytkownik
; UWAGA: Maksymalna długość wiadomości to 255 znaków!
message = "Zostałeś oznaczony jako użytkownik VPN, wyłącz tą aplikację ponieważ maskowanie adresu IP jest niezgodne z regulaminem."
```

<a name="poke-vars"></a>
### Dostępne zmienne

- `%client.ip` — Zawiera adres IPv4 użytkownika
- `%client.name` — Zawiera nazwę użytkownika
- `%client.uid ` — Zawiera unikalny identyfikator użytkownika
- `%client.dbid` — Zawiera identyfikator z bazy danych użytkownika
- `%client.link` — Zawiera odnośnik do użytkownika
- `%channel.link` — Zawiera odnośnik do kanału, na którym przebywa użytkownik

<a name="poke-info"></a>
### Ważna uwaga
Aby wiadomość mogła zostać wysłana, musi spełniać odpowiednie warunki zgodne ze standardem TeamSpeak3. Długość wiadomości nie może przekraczać 255 znaków, należy pamiętać, że umieszczenie zmiennych we wiadomości po wyzwoleniu ich wartości może w rzeczywistości znacznie zwiększyć długość wiadomości końcowej.

<a name="channel-log"></a>
## Zapis zdarzeń na kanale

```ini
; Metoda "channellog" pozwala na umieszczenie informacji o ostatnich
; detekcjach w opisie kanału.
[method:channellog]
```

Metoda pozwala na zapisywanie zdarzeń z wykonywanych czynności przez aplikację w opisie wyznaczonego kanału na serwerze TeamSpeak3.

```ini
; Identyfikator kanału na którym ma być zapisywany log aktualnych
; połączeń z maskowaniem prawdziwego adresu IP
channel_id = 0
```

W tym miejscu definujemy identyfikator kanału, w którego opisie mają być umieszczane powiadomienia.

```ini
; Format wpisu, który zostanie użyty dla każdego oznaczonego
; użytkownika. Można używać zmiennych:
;  %client.ip    -> zawiera numeryczny adres IP użytkownika
;  %client.name  -> zawiera aktualną nazwę użytkownika
;  %client.uid   -> zawiera unikalny identyfikator użytkownika
;  %client.dbid  -> zawiera database ID użytkownika
;  %client.link  -> odnośnik do użytkownika
;  %channel.link -> odnośnik do kanału na którym przebywa użytkownik
;  %comment      -> detection comment
;  %time         -> zawiera czas detekcji użytkownika
entry = "(%time) %client.link [%client.ip] @ %channel.link [b]%client.uid[/b] [%comment]"
```

Wartość pola `entry` zawiera format pojedynczego zdarzenia, które będzie zapisywane w opisie kanału.

```ini
; Maksymalna ilość wpisów w opisie kanału, wartość nie może być
; większa od 40.
max_entries = 20
```

Maksymalna ilość wpisów jakie będą zapisane w opisie kanału. Wartość ta nie może być zbyt wysoka, ponieważ oprogramowanie TeamSpeak3 nie zezwala na umieszczanie opisów kanałów dłuższych niż 65536 znaków.

<a name="channel-log-vars"></a>
### Dostępne zmienne

- `%client.ip` — Zawiera adres IPv4 użytkownika
- `%client.name` — Zawiera nazwę użytkownika
- `%client.uid ` — Zawiera unikalny identyfikator użytkownika
- `%client.dbid` — Zawiera identyfikator z bazy danych użytkownika
- `%client.link` — Zawiera odnośnik do użytkownika
- `%channel.link` — Zawiera odnośnik do kanału, na którym przebywa użytkownik
- `%comment` — Zawiera informacje na wykrytej sieci
- `%time` — Zawiera datę detekcji użytkownika

<a name="group-message"></a>
## Powiadomienie użytkowników

```ini
; Metoda "grouplog" umożliwia wysyłanie wiadomości do użytkowników
; z określonych grup.
[method:grouplog]
```

Aktywacja tej metody pozwala na zdefiniowanie listy grup, do których przynależni użytkownicy będą otrzymywali powiadomienia w razie pozytywnych detekcji.

```ini
; Lista grup do których przynależący użytkownicy będą 
; otrzymywali wiadomości. Grupy należy wpisać po przecinku.
groups = ""
```
Lista identyfikatorów grup serwerowych oddzielonych przecinkiem, do których przynależni użytkownicy mają otrzymywać powiadomienia.

Przykładowe ustawienie opcji:

```ini
groups = "1,2,3"
```

```ini
; Typ wiadomości wysyłanej do użytkowników.
;   * private - wiadomość prywatna
;   * poke - poke (max 255 znaków)
type = "private"
```

Forma stosowana podczas wysyłania wiadomości do użytkowników.
- `private` — wysłanie wiadomości prywatnej
- `poke` — wysłanie wiadomości "poke"

```ini
; Wiadomość wysyłana do użytkownika.
; Można używać zmiennych:
;  %client.ip    -> zawiera numeryczny adres IP użytkownika
;  %client.name  -> zawiera aktualną nazwę użytkownika
;  %client.uid   -> zawiera unikalny identyfikator użytkownika
;  %client.dbid  -> zawiera database ID użytkownika
;  %client.link  -> odnośnik do użytkownika
;  %channel.link -> odnośnik do kanału na którym przebywa użytkownik
message = "Użytkownik %client.link [%client.ip] @ %channel.link aktualnie jest połączony z serwerem i używa maskowania adresu IP."
```

Format wiadomości wysyłanej do użytkowników w odpowiednich grupach.

<a name="group-message-vars"></a>
### Dostępne zmienne

- `%client.ip` — Zawiera adres IPv4 użytkownika
- `%client.name` — Zawiera nazwę użytkownika
- `%client.uid ` — Zawiera unikalny identyfikator użytkownika
- `%client.dbid` — Zawiera identyfikator z bazy danych użytkownika
- `%client.link` — Zawiera odnośnik do użytkownika
- `%channel.link` — Zawiera odnośnik do kanału, na którym przebywa użytkownik

<a name="shell-command"></a>
## Wykonanie polecenia systemowego

```ini
; Metoda "shell" umożliwia wykonanie polecenia bezpośrednio w systemie
; kiedy zostanie wykryty użytkownik z połączeniem VPN.
[method:shell]
```

Uruchomienie tej opcji spowoduje wykonanie polecenia systemowego podczas prawidłowej detekcji maskowania adresu IP przez użytkownika.

```ini
; W tym miejscu możesz zdefiniować jaka komenda zostanie wykonana
; podczas detekcji VPN dla danego użytkownika. W ciągu komendy
; można używać zmiennych:
;  %client.ip    -> zawiera numeryczny adres IP użytkownika
;  %client.name  -> zawiera aktualną nazwę użytkownika
;  %client.uid   -> zawiera unikalny identyfikator użytkownika
;  %client.dbid  -> zawiera database ID użytkownika
;  %client.link  -> odnośnik do użytkownika
;  %channel.link -> odnośnik do kanału na którym przebywa użytkownik
command = "iptables -A INPUT -p udp -s %client.ip -dport 9987 -j DROP"
```

Definicja polecenia systemowego, które zostanie wykonane przy prawidłowej detekcji.

```ini
; Ten parametr decyduje czy program ma wstrzymać skanowanie do czasu
; aż nie zakończy się wykonywać zdefiniowane polecenie.
; true - oczekiwanie / false - uruchamianie w tle
wait = false
```

W przypadku włączenia parametru `wait`, program będzie oczekiwał na zakończenie wykonywania zleconego polecenia systemowego, zanim przejdzie do dalszego skanowania użytkowników. W przeciwnym wypadku polecenia będą wykonywane asynchronicznie.

<a name="shell-command-vars"></a>
### Dostępne zmienne

- `%client.ip` — Zawiera adres IPv4 użytkownika
- `%client.name` — Zawiera nazwę użytkownika
- `%client.uid ` — Zawiera unikalny identyfikator użytkownika
- `%client.dbid` — Zawiera identyfikator z bazy danych użytkownika
- `%client.link` — Zawiera odnośnik do użytkownika
- `%channel.link` — Zawiera odnośnik do kanału, na którym przebywa użytkownik

<a name="kick"></a>
## Wyrzucenie z serwera

```ini
; Metoda "kick" pozwala wyrzucać z serwera użytkowników, którzy
; zostali oznaczeni jako użytkownicy VPN.
[method:kick]
```

Kiedy ta metoda zostanie włączona, użytkownik po prawidłowej detekcji zostanie natychmiastowo wyrzucony z serwera z odpowiednim powodem.

```ini
; W tym miejscu możesz zdefiniować powód jaki zostanie wpisany
; podczas kickowania użytkownika z serwera.
reason = "Używanie oprogramowania do maskowania prawdziwego adresu IP."
```

Wiadomość umieszczana przez program jako powód wyrzucenia użytkownika z serwera.

<a name="ban"></a>
## Blokada dostępu do serwera

```ini
; Metoda "ban" pozwala zbanować od razu użytkownika który posługuje
; się oprogramowaniem do maskowania swojego prawdziwego adresu
; IP.
[method:ban]
```

Po prawidłowej detekcji maskowania adresu IP przez użytkownika zostanie on zbanowany, gdy ta opcja jest włączona.

```ini
; Rodzaj bana nadawanego przez aplikację:
;  * ip - zbanowanie adresu IP użytkownika na serwerze
;  * uid - zbanowanie unikalnego identyfikatora użytkownika
;  * all - zbanowanie wszystkich informacji o danym użytkowniku (ip, uid)
type = "ip"
```

Serwer TeamSpeak3 umożliwia różne rodzaje blokowania użytkowników, w tym miejscu należy zdefiniować, z którego rodzaju ma skorzystać oprogramowanie.

Dostępne rodzaje blokad:
- `ip` — Zablokowanie adresu IP użytkownika na serwerze
- `uid` — Zablokowanie publicznego unikalnego identyfikatora użytkownika na serwerze
- `all` — Zastosowanie obu metod jednocześnie

```ini
; Czas na jaki zostanie przyznany użytkownikowi ban.
; Wartość określana w sekundach, dla wartości 0 - ban na zawsze.
time = 0
```

Czas nakładanej blokady określany w sekundach. W przypadku podania wartości `0` blokada jest nakładana permanentnie.

```ini
; Powód banicji użytkownika.
reason = "Używanie oprogramowania do maskowania prawdziwego adresu IP."
```

Powód blokady użytkownika umieszczany przez program.

