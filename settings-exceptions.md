# Konfiguracja wyjątków

- [Podstawowe informacje](#introdution)
- [Biała lista](#whitelist)
- [Czarna lista](#blacklist)
- [Formatowanie wpisów](#format)
  - [Format IPv4](#format-ipv4)
    - [Przykładowy wpis](#format-ipv4-example)
  - [Format CIDR](#format-cidr)
    - [Przykładowy wpis](#format-cidr-example)
  - [Maska](#format-mask)
    - [Przykładowy wpis](#format-mask-example)
  - [Wyrażenie regularne](#format-regex)
    - [Przykładowy wpis](#format-regex-example)
- [Komentarze](#comments)

<a name="introdution"></a>
## Podstawowe informacje

Program podczas uruchamiania  interpretuje dwa pliki:

- eter_sensor_whitelist.txt
- eter_sensor_blacklist.txt

Umożliwiają one zdefiniowanie własnych reguł filtrowania adresów IP lub umieszczenie wyjątków, które nie będą poddawane metodom stosowanych przez aplikację podczas prawidłowej detekcji.

<a name="whitelist"></a>
## Biała lista

Wpisy, które będą obsługiwane przez białą listę należy umieścić w pliku `eter_sensor_whitelist.txt`. Wszystie filtry zawarte na tej liście będą wykluczały określone adresy IP ze spektrum skanowania wykonywanego przez program.

<a name="blacklist"></a>
## Czarna lista

Wpisy czarnej listy należy umieszczać w pliku `eter_sensor_blacklist.txt`. Adresy IP określone przez filtry w czarnej liście spowodują poszerzenie spektrum skanowania aplikacji.

<a name="format"></a>
## Formatowanie wpisów

Każdy wpis powinien zostać odpowiednio sformatowany, aby program mógł go prawidłowo zinterpretować. Pojedyncze wpisy do odpowiedniego pliku umieszczamy w oddzielnych liniach. Każdy wpis musi zawierać oddzielone białymi znakami:
- Rodzaj formatu wpisu
- Parametr formatu wpisu
- Komentarz

Przykładowy wpis:

```
addr 127.0.0.1 Home exception
```

Rodzaj formatu | Parametr formatu | Komentarz
-------------- | ---------------- | ---------
addr           | 127.0.0.1        | Home exception

Dostępne formaty wpisów:
- `addr` - Format adresu IPv4
- `cidr` - Format bezklasowej metody przydzielania adresów IP
- `mask` - Format z zastosowaniem maskowania
- `regex` - Format z zastosowaniem wyrażenia regularnego

Należy pamiętać, że parametr komentarza umieszczany na samym końcu każdego pliku, jest przechowywany w zmiennej `%comment`, która ma zastosowanie przy niektórych metodach podczas formatowania tekstu.

<a name="format-ipv4"></a>
### Format IPv4

Zastosowanie tej metody porównywania pozwala na filtrowanie konkretnie określonych adresów IP przez program. Tę metodę można ustawić np. w przypadku ignorowania serwerów, na których jest hostowane oprogramowanie takie jak boty muzyczne, aby nie zostały one wyrzucone w wyniku pozytywnej detekcji sieci serwerowni (która nie jest siecią dostępną dla przeciętnych użytkowników).

<a name="format-ipv4-example"></a>
#### Przykładowy wpis

```
addr 127.0.0.1 Home exception
```

Rodzaj formatu | Parametr formatu | Komentarz
-------------- | ---------------- | ---------
addr           | 127.0.0.1        | Home exception

Więcej o IPv4: [https://pl.wikipedia.org/wiki/IPv4](https://pl.wikipedia.org/wiki/IPv4)

<a name="format-cidr"></a>
### Format CIDR

Format bezklasowej metody przydzielania adresów IP pozwala na określenie całych zakresów sieci filtrowanych przez program.

<a name="format-cidr-example"></a>
#### Przykładowy wpis

```
cidr 192.168.0.1/24 Example network exception
```

Rodzaj formatu | Parametr formatu | Komentarz
-------------- | ---------------- | ---------
cidr           | 192.168.0.1/24   | Example network exception

Przykład spowoduje filtrowanie adresów IP o masce podsieci `255.255.255.0`, czyli zakres od `192.168.0.1` do `192.168.0.254`.

Więcej o CIDR: [https://pl.wikipedia.org/wiki/Classless_Inter-Domain_Routing](https://pl.wikipedia.org/wiki/Classless_Inter-Domain_Routing)

<a name="format-mask"></a>
### Maska

Znakiem maskującym jest `*`, który pozwala wskazać fragmenty parametru, jakie mogą przyjąć dowolną wartość. Dzięki temu jesteśmy w stanie stworzyć filtr mający zastosowanie dla określonych zakresów.

<a name="format-mask-example"></a>
#### Przykładowy wpis

```
mask 192.168.*.0 Example mask exception
```

Rodzaj formatu | Parametr formatu | Komentarz
-------------- | ---------------- | ---------
mask           | 192.168.\*.0   | Example mask exception

Zastosowanie przykładu spowoduje filtrowanie adresów IP w zakresie od `192.168.0.0` do `192.168.255.0`, gdzie końcówka `.0` pozostaje stała (zmienia się tylko trzeci oktet).

<a name="format-regex"></a>
### Wyrażenie regularne

Wyrażenia regularne to potężne narzędzie do budowania filtrów dla zaawansowanych użytkowników. Pozwalają one bardzo precyzyjnie określić filtrowany zakres, który normalnie wymagałby zastosowania kilku lub kilkunastu reguł.

<a name="format-regex-example"></a>
#### Przykładowy wpis

```
regex 192\.168\.[1]{1,2}\.0 Example regex exception
```

Rodzaj formatu | Parametr formatu | Komentarz
-------------- | ---------------- | ---------
regex          | 192\\.168\\.[1]{1,2}\\.0 | Example regex exception

Zastosowanie wpisu z przykładu spowoduje filtrowanie adresów IP: `192.168.1.0` oraz `192.168.11.0`.

Więcej o wyrażeniach regularnych: [https://pl.wikipedia.org/wiki/Wyrażenie_regularne](https://pl.wikipedia.org/wiki/Wyrażenie_regularne)

<a name="comments"></a>
## Komentarze
Pliki zawierające wpisy określające filtry dla programu obsługują umieszczanie w nich własnych komentarzy. Każdy komentarz należy poprzedzić znakiem `#`, pozostała część linii będzie ignorowana podczas interpretacji pliku.

Przykład:
```
# To jest przykładowy komentarz
regex 192\.168\.[1]{1,2}\.0 Example regex exception
# regex 192\.168\.[1]{1,2}\.0 Example regex exception <-- ta reguła nie będzie działać
```
