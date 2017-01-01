# Konfiguracja podstawowych funkcji

- [Sprawdzanie połączeń do ServerQuery](#query-connections-checker)
- [Lista ignorowanych grup użytkowników](#ignored-groups)
- [Wysyłanie powiadomień](#notifications)
- [System oznaczeń](#mark-vpn-client)
  
<a name="query-connections-checker"></a>
## Sprawdzanie połączeń do ServerQuery
```ini
; Opcja decyduje o tym czy aplikacja ma sprawdzać użytkowników
; ServerQuery. true - włączone / false - wyłączone
server_query_clients = false
```
Możemy zdecydować, czy oprogramowanie ma wykonywać swoje czynności detekcyjne na połączeniach nawiązywanych z protokołem ServerQuery. Kiedy ta opcja jest włączona, należy pamiętać o umieszczeniu w wyjątkach adresu IP innych usług wykorzystujących protokół ServerQuery takich jak: publiczne list serwerów, boty itp.

<a name="ignored-groups"></a>
## Lista ignorowanych grup użytkowników
```ini
; Lista grup do których przynależący użytkownicy są ignorowani
; podczas skanowania. Grupy należy wpisać po przecinku.
ignored_groups = ""
```
Za pomocą tego parametru konfiguracyjnego możemy wykluczyć osoby przynależące do określonych grup ze spektrum skanowania dokonywanego przez program. W tym celu należy wpisać oddzielone przecinkiem identyfikatory grup, które mają zostać ignorowane.

Przykładowe ustawienie:
```ini
ignored_groups = "1,2,3"
```

<a name="notifications"></a>
## Wysyłanie powiadomień
```ini
; Funkcja uruchamia powiadomienia o wykonywanych przez dane
; metody czynnościach np. o wysłaniu wiadomości do użytkownika.
; true - włączone / false - wyłączne
method_messages = true
```
W tym miejscu możemy globalnie zablokować wszystkie powiadomienia wysyłane przez program do użytkowników, niezależnie od zastosowanej metody ograniczenia dostępu.

<a name="mark-vpn-client"></a>
## System oznaczeń
```ini
; Włączenie tej opcji spowoduje detekcję użytkownika raz na jego
; połączenie do serwera. Metody na takim użytkowniku będą wykonywane
; tylko raz na aktualną sesję połączenia do serwera.
mark_vpn_client = true
```
Kiedy ta opcja jest włączona, użytkownicy serwera głosowego poddawani są procedurą weryfikacyjnym raz na aktualnie trwające połączenie. Należy jednak pamiętać, że w kilku przypadkach zastosowania usługi VPN adres IP może zostać zmieniony podczas trwającego połączenia z serwerem TeamSpeak3.
