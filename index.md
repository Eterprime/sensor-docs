# Eter Sensor

- [Wstęp](#introdution)
- [Licencja](#license)
- [Zasada działania](#about)
  - [Baza danych](#about-database)
  - [Chmura detekcyjna](#about-database)
  - [Czarna lista](#about-blacklist)
  
<a name="introdution"></a>
## Wstęp
Autor aplikacji: [Łukasz Adamski](mailto:lukasz.adamski@eterprime.eu)

Oprogramowanie zostało stworzone dla serwerów TeamSpeak3 w celu skutecznej detekcji i ochrony przeciwko osobom, które maskują swoje prawdziwe adresy IP.

Program został napisany w języku PHP w wersji 5.6 z zastosowaniem autorskich bibliotek i rozwiązań. Dostarczany jest do użytkownika w postaci zaszyfrowanego kodu wymagającego autoryzowanej licencji do jego uruchomienia.

<a name="license"></a>
## Licencja
W celu użytkowania niniejszego oprogramowania wymagana jest licencja Eterprime, którą można uzyskać po zalogowaniu się na [naszej stronie internetowej](https://eterprime.eu) w panelu użytkownika.

<a name="about"></a>
## Zasada działania
Oprogramowanie Eter Sensor w swoim działaniu wykorzystuje specjalny algorytm określający poziom zaufania danego użytkownika, gdy poziom zaufania nie jest dostateczny, wykonywane są działania diagnostyczne.

<a name="about-database"></a>
### Baza danych
Przez lata stworzyliśmy ogromną bazę adresów IP organizacji zajmujących się dostarczaniem usług serwerów Proxy/VPN oraz zakresów serwerowni i lokalizacji, które nie są sieciami dostępnymi dla standardowych użytkowników.

<a name="about-cloud"></a>
### Chmura detekcyjna
Kiedy dany użytkownik uzyska zbyt niski stopień zaufania określany przez nasze algorytmy, jego adres IP przekazywany jest do naszej chmury, która bada jego autentyczność i zwraca odpowiedź do aplikacji w celu określenia dalszych procedur postępowania z użytkownikiem. Dzięki zastosowaniu tej technologii baza naszych detekcji stale rośnie i są one przeprowadzane coraz szybciej, zachowując przy tym precyzję.

<a name="about-blacklist"></a>
### Czarna lista
Zastosowanie rozwiązania czarnej listy umożliwia własnoręczne definiowanie filtrów stosowanych przez program w czasie jego działania w celu uzupełnienia ochrony lub zdefiniowania wyjątków.
