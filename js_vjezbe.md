---
description: Programsko inženjerstvo - JS - Zadaci za vježbanje
author: Toni Starčić, Nikola Tanković
license: CC BY-SA
---

<img src="art/fipu.png" alt="fipu" style="zoom:24%;" />



1. Implementiraj funkciju koja iterira kroz jedan JSON objekt i sumira elemente samo ako je element cijeli broj:

  ```javascript
  INPUT = {
    "prvi": 122,
    "drugi: 18,
    "treci": "NotAnInteger",
          "cetvrti": -2,
    "peti": 322,
    "sesti": 32.0
  }
  OUTPUT = f(INPUT) //462
  ```

  

1. Nadogradi funkciju iz zadaće **302** na nacin da se obrišu suvišni uzastopni znakovi:

  ```javascript
  INPUT = ["banaana, jabuukka", "j1agoda", ""]
  OUTPUT = f(INPUT) //["banana", "jabuka", "j1agoda", ""]
  ```

  

1. Nadogradi funkciju 403 na nacin da se obrisu suvisne zagrade, odnosno da funkcija vrati string u kojemu su zagrade valjane

  ```javascript
  INPUT = "({[([)]})"
  OUTPUT = f(INPUT) // "({[()]})"
  ```

4. Napisite rekurzivnu funkciju koja racuna sumu kvadrata s time da su elementi clanovi polja
INPUT => [1,2,3,4]
OUTPUT => 25

11.11

1. Implementirajte funkciju koja prima polje stringova i vraća najkraći string.
INPUT => ["aaa", "bbbb", "cc", ""]
OUTPUT => "cc"

2. Implementirajte funkciju koja racuna manhattanDistance s time da su tocke x1, y1, x2 i y2 članovi polja.
INPUT => ([5,4],[3,2])
OUTPUT => 4

3. Implementirajte funkciju unique koja prima polje i vraća polje u kojemu se nalaze podaci koji se pojavljuju točno jednom
INPUT => [1, 2, 1 3 1 4 1 5 a a b c"]
OUTPUT => [1, 2, 3, 4, 5, a, b, c]

4. Implementirajte rekurzivnu funkciju koja prima polje podataka i prirodni broj n, a vraća polje elemenata koji se pojavljuju barem n puta.
INPUT => ([1, 2, 1, 3, a, 1, 4, 1, 5, a, a, b, c], 2)
OUTPUT => [1, a]
DODATNO POJAŠNJENJE: 1 i a se pojavljuju 3 puta.

18.11

1. Implementirajte funkciju koja prima polje binarnih znamenki s time da je broj indeksa fiksan
INPUT => [0, 0, 0, 0, 0, 0, 1, 0]
OUTPUT => 2

2. Implementirajte funkciju koja prima string, a vraća broj koji nedostaje u tom stringu/nizu brojeva.
INPUT => "1235678";
OUTPUT => 4;
INPUT => "9091929495";
OUTPUT => 93;

3. Implementirajte rekurzivnu funkciju koja racuna produkt fibonaccijevih brojeva s time da ne uzima u obzir pocetnu iteraciju. Napisite ju na nacin da prima argument n.
INPUT => 6
OUTPUT => 30
DODATNO POJAŠNJENJE: 0 - 1 - 1 - 2 - 3 - 5 (preskace 0)

4. Implementirajte rekurzivnu funkciju koristeći inbuilt funkcije map i filter, koja prima prirodni broj n i vraća polje trojki čiji je opseg maksimalno n.
INPUT => 12
OUTPUT => [3,4,5]
DODATNO POJAŠNJENJE: Elementi liste su stranice trokuta "a", "b" i "c". Moraju biti pitagorine trojke i opseg tih stranica mora biti manji ili jednak n.