# Konfiguracja

- [Wstęp](#introdution)
- [Połączenie z TeamSpeak3 ServerQuery](#connection)
  - [Host i port serwera](#connection-host-and-port)
  - [Nazwa użytkownika i hasło](#connection-auth)
  - [Instancja serwera TeamSpeak3](#connection-instance)
    - [Identyfikator instancji](#connection-instance-id)
    - [Port komunikacyjny](#connection-instance-port)
  - [Nadanie nazwy połączenia](#connection-name)
  
<a name="introdution"></a>
## Wstęp
Konfiguracja oprogramowania znajduje się w pliku `config.ini`, jest to jedyny plik wymagający edycji użytkownika w celu poprawnego działania programu.

W paczce dystrybucyjnej plik dostarczany jest jako `config.ini.dist`, jego nazwę należy zmienić na `config.ini`.
```sh
mv config.ini.dist config.ini
```
<a name="connection"></a>
## Połączenie z TeamSpeak3 ServerQuery
Oprogramownie do poprawnego działania wymaga stałego połączenia z protokołem ServerQuery. Ustawienia te definiujemy w pliku konfiguracyjnym — sekcji `serverquery`.
```ini
[serverquery]

    ; Nazwa hosta niezbędna do połączenia z serwerem TeamSpeak3
    ; @default "localhost:10011"
    hostname = "localhost:10011"
    
    ; Nazwa użytkownika ServerQuery  
    ; @default "serveradmin"
    username = "serveradmin"
    
    ; Hasło użytkownika ServerQuery
    ; @default "secret"
    password = "secret"
    
    ; Sposób wyboru instancji serwera TeamSpeak3.
    ;   * za pomocą virtuaserver_id - "id:<virtualserver_id>" np. "id:1"
    ;   * za pomocą portu UDP - "port:<virtualserver_port>" np. "port:9987"
    ; @default "id:1"
    instance = "id:1"
    
    ; Nazwa połączenia Query (nazwa użytkownika)
    ; @default "Eter Sensor"
    nickname = "Eter Sensor"
```
<a name="connection-host-and-port"></a>
### Host i port serwera
```ini
; Nazwa hosta niezbędna do połączenia z serwerem TeamSpeak3
; @default "localhost:10011"
hostname = "localhost:10011"
```
Aby połączenie mogło zostać poprawnie nawiązane, należy tutaj podać host serwera docelowego oraz port, na którym jest dostępny protokół ServerQuery (`TCP` domyślnie 10011). W przypadku kiedy aplikacja nie może nawiązać połączenia z serwerem mimo poprawnej konfiguracji w tej sekcji, należy sprawdzić, czy adres serwera, na którym jest ona uruchomiona, został dodany do pliku 'query_ip_whitelist.txt' w katalogu głównym serwera TeamSpeak3.

<a name="connection-auth"></a>
### Nazwa użytkownika i hasło
```ini
; Nazwa użytkownika ServerQuery  
; @default "serveradmin"
username = "serveradmin"

; Hasło użytkownika ServerQuery
; @default "secret"
password = "secret"
```
W tej sekcji definiujemy nazwę użytkownika oraz hasło wykorzystywane przez program podczas autoryzacji połączenia z ServerQuery. Należy pamiętać, że do poprawnego działania wymagane są odpowiednie uprawnienia, szczególnie:
- b_client_ignore_antiflood
- b_virtualserver_client_list
- b_serverinstance_info_view
- b_serverquery_login

<a name="connection-instance"></a>
### Instancja serwera TeamSpeak3
```ini
; Sposób wyboru instancji serwera TeamSpeak3.
;   * za pomocą virtuaserver_id - "id:<virtualserver_id>" np. "id:1"
;   * za pomocą portu UDP - "port:<virtualserver_port>" np. "port:9987"
; @default "id:1"
instance = "id:1"
```
Ponieważ serwer TeamSpeak3 wspiera możliwość uruchomienia wielu instancji na jednej licencji w tej sekcji musimy zdefiniować, na której instancji serwera program ma wykonywać swoje czynności.

<a name="connection-instance-id"></a>
#### Identyfikator instancji
W celu wskazania instancji za pomocą identyfikatora należy zastosować format z przedrostkiem 'id:' a następnie podać numer instancji serwera. Domyślnie dla serwerów, które nigdy nie posiadały dodatkowych instancji liczba określająca podstawowy serwer to '1'.
```
id:1
```

<a name="connection-instance-port"></a>
#### Port komunikacyjny
Drugą możliwością określenia instancji docelowej jest podanie portu komunikacyjnego (`UDP`), którym domyślnie jest numer `9987` z przedrostkiem `port:`.
```
port:9987
```

<a name="connection-name"></a>
### Nadanie nazwy połączenia
```ini
; Nazwa połączenia Query (nazwa użytkownika)
; @default "Eter Sensor"
nickname = "Eter Sensor"
```
W tym miejscu możemy zdefiniować nazwę połączenia oprogramowania Eter Sensor, jaka będzie widoczna na liście kanałów serwera TeamSpeak3.
