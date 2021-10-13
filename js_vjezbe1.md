---
description: Programsko inženjerstvo - JS - Zadaci za vježbanje
author: Toni Starčić, Nikola Tanković
license: CC BY-SA
---

<img src="art/fipu.png" alt="fipu" style="zoom:24%;" />



1. Implementiraj funkciju koja iterira kroz jedan *Javascript* objekt i sumira elemente samo ako je element cijeli broj:

  ```javascript
  INPUT = {
    "prvi": 122,
    "drugi": 18,
    "treci": "NotAnInteger",
    "cetvrti": -2,
    "peti": 322,
    "sesti": 32.0
  }
  OUTPUT = f(INPUT) //492
  ```

2. Nadogradi funkciju iz zadaće **JS-302** na način da se obrišu suvišni uzastopni znakovi:

  ```javascript
  INPUT = ["banaana, jabuukka", "j1agoda", ""]
  OUTPUT = f(INPUT) //["banana", "jabuka", "j1agoda", ""]
  ```

3. Nadogradi funkciju **JS-403** na način da se obrišu suvišne zagrade, odnosno da funkcija vrati *string* u kojemu su zagrade valjane:

  ```javascript
  INPUT = "({[([)]})"
  OUTPUT = f(INPUT) //"({[()]})"
  ```

4. Napišite rekurzivnu funkciju koja računa sumu kvadrata elemenata s time da su elementi članovi *polja*:

```javascript
INPUT = [1,2,3,4]
OUTPUT = f(INPUT) //25
```

